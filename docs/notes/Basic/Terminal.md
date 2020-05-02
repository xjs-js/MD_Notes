---
tags: [Notebooks/Basic]
title: Terminal
created: '2019-09-18T00:59:50.173Z'
modified: '2020-03-08T03:25:18.116Z'
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
CertUtil -hashfile <filename> MD5
CertUtil -hashfile <filename> SHA1
CertUtil -hashfile <filename> SHA256
```
---
Mac
```
md5           <filename>  
shasum -a 1   <filename> # SHA1
shasum -a 256 <filename> # SHA256
```
