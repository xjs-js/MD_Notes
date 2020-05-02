---
tags: [Notebooks/IDE_Config]
title: boost
created: '2019-11-02T02:36:41.859Z'
modified: '2020-03-08T03:40:50.394Z'
---

# boost

## windows 7
安装目录`C:\boost_1_17_0`  
include`C:\boost_1_71_0`   
lib`C:\boost_1_71_0\stage\lib`   

## macOS
include `/usr/local/Cellar/boost/1.69.0_2/include`   
lib `/usr/local/Cellar/boost/1.69.0_2/lib`    


## QT .pro文件配置
```cpp
INCLUDEPATH += /usr/local/Cellar/boost/1.69.0_2/include
LIBS += -L/usr/local/Cellar/boost/1.69.0_2/lib -lboost_filesystem
```

