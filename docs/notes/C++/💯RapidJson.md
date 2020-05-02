---
tags: [Notebooks/C++]
title: "\U0001F4AFRapidJson"
created: '2019-09-20T01:41:43.796Z'
modified: '2020-03-08T03:20:12.539Z'
---

# :100:RapidJson 

#### :+1:中文字符串


![Image](../attachments/code/050cc95f-0bce-41d5-bb3c-2bbeaee17764.png)
<details>
<summary>Code</summary>
<markdown>
```cpp
std::string hello = "你好";
// 编码转换可省略
hello = CodeToCode::GBKToUTF8(QString::fromStdString(hello)).toStdString();

Value strContent(kStringType);
strContent.SetString(hello.c_str(), allocator);

root.AddMember("Status", strContent, allocator);
```
</markdown>
</details>




