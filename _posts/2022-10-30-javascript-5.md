---
title: Object에 해당 key값의 존재 여부 확인
author: surfharu
date: 2022-10-30 14:00:00 +0800
categories: [javascript]
tags: [javascript, key] # TAG names should always be lowercase
---

`Object.hasOwnProperty` 를 활용한다.

```js

let obj1 = {name: 'tony', age: '18'}

console.log(obj1.hasOwnProperty('name')) // true
console.log(obj1.hasOwnProperty('age')) // true
console.log(obj1.hasOwnProperty('phone')) // false
```