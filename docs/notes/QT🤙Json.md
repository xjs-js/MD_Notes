---
tags: [Notebooks/QT_C++]
title: "QT\U0001F919Json"
created: '2019-09-18T03:00:19.022Z'
modified: '2019-09-22T14:14:35.661Z'
---

# QT:call_me_hand:Json

* QJsonObject
* QJsonArray

## 构造
```cpp
// 单个json对象
QJsonObject object
{
    {"property1", 1},
    {"property2", 2}
};
```
```json
{
  property1: 1,
  property2: 2
}
```
* QJsonArray
```cpp
QJsonArray flags   {
  QJsonObject{{"flag1", ui->checkBoxFlag1->isChecked()}},
  QJsonObject{{"flag4", ui->checkBoxFlag4->isChecked()}}
};
```

## 转换
* QJsonObject -> QString
```cpp
QJsonObject jsonObj; // assume this has been populated with Json data

QJsonDocument doc(jsonObj);
QString strJson(doc.toJson(QJsonDocument::Compact));
```

* QJsonArray -> QString
```cpp
QJsonArray data;
QJsonDocument doc;
doc.setArray(data);

QString dataToString(doc.toJson());
```

## Reference
### 解析
[Qt parsing JSON using QJsonDocument, QJsonObject, QJsonArray](https://stackoverflow.com/questions/19822211/qt-parsing-json-using-qjsondocument-qjsonobject-qjsonarray)

[Qt之JSON教程](https://zhuanlan.zhihu.com/p/71979650)
