---
tags: [Notebooks/FullStack]
title: "React\U0001F919Template"
created: '2019-09-16T01:38:40.197Z'
modified: '2019-09-23T02:59:02.657Z'
---

# React:call_me_hand:Template

## 头文件
```jsx
import React, { Component } from 'react';
import ReactDOM from 'react-dom';
```

## setState接收一个参数
```jsx
  handleClickOnLikeButton () {
    this.setState((prevState) => {
      return { count: 0 }
    })
    this.setState((prevState) => {
      return { count: prevState.count + 1 } // 上一个 setState 的返回是 count 为 0，当前返回 1
    })
    this.setState((prevState) => {
      return { count: prevState.count + 2 } // 上一个 setState 的返回是 count 为 1，当前返回 3
    })
    // 最后的结果是 this.state.count 为 3
  }
...
```
