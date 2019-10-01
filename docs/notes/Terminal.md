---
tags: [Notebooks/no_one]
title: Terminal
created: '2019-09-18T00:59:50.173Z'
modified: '2019-09-25T02:34:34.812Z'
---

# Terminal

#### 杀掉占用某个端口的进程

```bash
lsof -i:8000
kill -9 pid
```


#### MD5、SHA1、SHA256
Windows
```bash
certutil -hashfile <filename> MD5
certutil -hashfile <filename> SHA1
certutil -hashfile <filename> SHA256
```
---
Mac
```
md5           <filename>  
shasum -a 1   <filename> # SHA1
shasum -a 256 <filename> # SHA256
```
