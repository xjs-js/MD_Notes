---
title: Boost TCP Tutorial
created: '2020-03-08T10:16:03.096Z'
modified: '2020-03-08T14:24:15.939Z'
---

# Boost TCP Tutorial

最近要写一个TCP的服务，所以又重新学习了一遍[boost官网](https://www.boost.org/doc/libs/1_63_0/doc/html/boost_asio/tutorial.html)的教程

## [Daytime.1 - A synchronous TCP daytime client](https://www.boost.org/doc/libs/1_63_0/doc/html/boost_asio/tutorial.html#boost_asio.tutorial.tutdaytime1)

这是一个简单的TCP Client，连接到TCP Server之后，会收到一个TCP Server发来的时间，一直等待TCP Server发送。

```cpp
#include <QCoreApplication>

#include <iostream>
#include <boost/array.hpp>
#include <boost/asio.hpp>
#include <string>
#include <iostream>

using boost::asio::ip::tcp;

int main(int argc, char *argv[])
{
    QCoreApplication a(argc, argv);

    // io_service
    boost::asio::io_service io_service;

    // 建立一个socket
    tcp::socket socket(io_service);

    // 服务端的地址和端口
    std::string address = "192.168.0.102";
    unsigned short port = 8898;
    tcp::endpoint endpoint(boost::asio::ip::address::from_string(address), port);

    // socket连接到endpoint
    socket.connect(endpoint);

    for(;;)
    {
        boost::array<char, 128> buf;
        boost::system::error_code error;

        // 同步读取Server发来的消息，如果没有，会一直阻塞在此
        size_t len = socket.read_some(boost::asio::buffer(buf), error);

        // 在命令行输出收到的消息
        std::cout.write(buf.data(), len);
    }

    return a.exec();
}
```
从上面👆的代码我们知道，一个简单的TCP Client程序需要一个io_service，一个socket，一个endpoint。

## [Daytime.2 - A synchronous TCP daytime server](https://www.boost.org/doc/libs/1_63_0/doc/html/boost_asio/tutorial.html#boost_asio.tutorial.tutdaytime2)

这是一个简单的TCP Server，等待一个客户端的连接，然后发送当前时间，继续等待下一个连接。 

```cpp
#include <QCoreApplication>
#include <ctime>
#include <iostream>
#include <string>
#include <boost/asio.hpp>

using boost::asio::ip::tcp;

// 返回当前的时间
std::string make_daytime_string()
{
  using namespace std; // For time_t, time and ctime;
  time_t now = time(0);
  return ctime(&now);
}

int main(int argc, char *argv[])
{
    QCoreApplication a(argc, argv);
  
    // io_service
    boost::asio::io_service io_service;
    
    // acceptor
    tcp::acceptor acceptor(io_service, tcp::endpoint(tcp::v4(), 8898));

    for (;;)
    {
      // socket
      tcp::socket socket(io_service);

      // 首先会阻塞在这里
      acceptor.accept(socket);

      // 当前时间
      std::string message = make_daytime_string();

      boost::system::error_code ignored_error;
      boost::asio::write(socket, boost::asio::buffer(message), ignored_error);
    }


    return a.exec();
}

```
从上面👆的代码我们知道，如果要写一个TCP Server，除了和TCP Client之后，还需要一个acceptor。

## Daytime Client 和 Daytime Server Improved
上面的程序最终跑出来的结果是，先启动一个TCP Server，接着运行一个TCP Client，接着TCP Client会收到一个时间；再启动给一个TCP Client还是同样的结果。可以同时存在多个TCP Client，但是不能存在多个TCP Server，因为每个TCP Server都要占用一个TCP的端口。

现在我们修改TCP Server的程序，让TCP Server能够向Client发送多次时间。

```cpp
#include <QCoreApplication>
#include <ctime>
#include <iostream>
#include <string>
#include <boost/asio.hpp>

using boost::asio::ip::tcp;

std::string make_daytime_string()
{
  using namespace std; // For time_t, time and ctime;
  time_t now = time(0);
  return ctime(&now);
}

int main(int argc, char *argv[])
{
    QCoreApplication a(argc, argv);
    try {
        boost::asio::io_service io_service;
        tcp::acceptor acceptor(io_service, tcp::endpoint(tcp::v4(), 8898));

        tcp::socket socket(io_service);
        // 没有Client连接时，会先阻塞在这里
        acceptor.accept(socket);

        int i;
        printf("breakpoint\n");
        // 有了Client连接之后，会阻塞在这里
        while (scanf("%d", &i) != -1)
        {
            printf("make day time\n");
            std::string message = make_daytime_string();
            boost::system::error_code ignored_error;
            socket.write_some(boost::asio::buffer(message), ignored_error);
        }
    } catch (std::exception& e) {
        std::cerr << e.what() << std::endl;
    }

    return a.exec();
}
```
当TCP Server改成上面的代码之后，Server端随便输入什么，都会向客户端发送一个时间。但是上面的代码只能维持一个连接，一旦有TCP Client连接上之后，就不能有其他的Client连接了。

我们最终的目标是Server一直启动在那里，然后客户端发送一个请求之后，会立即收到当前时间，再请求之后，还是会收到时间；如果同时再启动一个Client还是会有同样的效果。显然，根据上面的代码，我们无法改写实现这样的功能，所以我们继续学习官网的教程，接下来应该到异步发送和接收了。


## [Daytime.3 - An asynchronous TCP daytime server](https://www.boost.org/doc/libs/1_63_0/doc/html/boost_asio/tutorial.html#boost_asio.tutorial.tutdaytime3)

```cpp
#include <QCoreApplication>

#include <ctime>
#include <iostream>
#include <string>
#include <boost/bind.hpp>
#include <boost/shared_ptr.hpp>
#include <boost/enable_shared_from_this.hpp>
#include <boost/asio.hpp>
#include <boost/make_shared.hpp>

using boost::asio::ip::tcp;

// retrun current time
std::string make_daytime_string()
{
  using namespace std; // For time_t, time and ctime;
  time_t now = time(0);
  return ctime(&now);
}

// each connection containing a socket
class tcp_connection
        : public boost::enable_shared_from_this<tcp_connection>
{
public:
    typedef boost::shared_ptr<tcp_connection> pointer;

    tcp_connection(boost::asio::io_service& io_service)
        : socket_(io_service)
    {

    }

    // GET接口，返回socket
    tcp::socket& socket()
    {
        return socket_;
    }

    // public 接口，用socket接口给对方发送当前时间
    void start()
    {
        std::cout << "handle write" << std::endl;
        message_ = make_daytime_string();

        socket_.async_write_some(boost::asio::buffer(message_),
                           boost::bind(&tcp_connection::handle_write,
                                       this,
                                       boost::asio::placeholders::error,
                                       boost::asio::placeholders::bytes_transferred));
    }


private:
    // async_write_some的回掉函数
    void handle_write(const boost::system::error_code& ec, size_t bytes_transferred)
    {
        std::cout << "handle write" << std::endl;
    }

    tcp::socket socket_;
    std::string message_;
};


// TCP Server类
class tcp_server
{
public:
    tcp_server(boost::asio::io_service& io_service)
        : acceptor_(io_service, tcp::endpoint(tcp::v4(), 8898))
    {
        start_accept();
    }


private:
    // 构造函数调用，acceptor异步接收连接
    void start_accept()
    {
        std::cout << "start accept" << std::endl;
        tcp_connection::pointer connection_ptr = boost::make_shared<tcp_connection>(acceptor_.get_io_service());
        acceptor_.async_accept(connection_ptr->socket(),
                         boost::bind(&tcp_server::handle_accept,
                                     this,
                                     connection_ptr,
                                     boost::asio::placeholders::error));
    }

    // acceptor异步接收的回掉函数
    void handle_accept(tcp_connection::pointer connection,
                       const boost::system::error_code& ec)
    {
        std::cout << "start handle accept" << std::endl;
        if (!ec)
        {
            // 发送
            connection->start();
        }
        start_accept();
    }

    // acceptor
    tcp::acceptor acceptor_;
};

int main(int argc, char *argv[])
{
    QCoreApplication a(argc, argv);

    try {
        boost::asio::io_service io_service;
        tcp_server server(io_service);
        io_service.run();
    } catch (std::exception& e) {
        std::cout << e.what() << std::endl;
    }

    return a.exec();
}

```

第一次看上面👆的代码的话，可能会感觉比较困难，毕竟以前明明只有一个类的啊，而且直接跳到了Server，Client为什么没有实现的例子。
首先tcp_server是主要的类，维护了一个acceptor；tcp_connection表示每一个连接，里面维护了一个scoket。acceptor每次accept之前都会new 一个tcp_connection，然后在handle_accept里用tcp_connection操作socket发送或者接收。

