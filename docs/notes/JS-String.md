---
tags: [Notebooks/FullStack]
title: JS-String
created: '2019-09-13T16:39:10.242Z'
modified: '2019-09-23T02:57:40.969Z'
---

# JS-String

## Props

1. .length
```js
"Nice!".length;
// 5
```

2. .includes(searchString)
```js
"Hello World".includes("World");  // true
"Hello World".includes("Potato"); // false
```

3. .toUpperCase()
```js
"hello".toUpperCase(); // "HELLO"
```

4. .toLowerCase()
```js
"NICe".toLowerCase(); // "nice";
```

5. substring(indexStart, indexEnd)
* indexStart:  the position of the first character you'd like to **include**
* indexEnd:  可省略，the position of the first character you'd like to **ignore**
```js
const language = "JavaScript";
language.substring(1, 4); //"ava"

language.substring(4); //"Script"
```

6. Template strings
```js
`This is a multiline
string that
just works!`
`I am learning ${language}`;
```

7. .startsWith(serchString) .endsWith(searchString)
```js
const phoneNumber = "+103123456";
phoneNumber.startsWith("+"); //true
phoneNumber.startsWith("10"); //false
phoneNumber.endsWith("56"); // true
```

8. .trim()
```js
var greeting = '   Hello world!   ';
console.log(greeting.trim());
// expected output: "Hello world!";
```

