---
title: "[javascript] 변수값 서로 교환하기" 
author: surfharu
date: 2023-01-03 09:00:00 +0800
categories: [javascript]
tags: [javascript, destructing] # TAG names should always be lowercase
---

script 에서 `변수값을 서로 교환`하기 위해서는 주로 `temp` 변수를 활용하였으나 `구조 분해 할당`시 조금 더 편리하게 이용할 수 있다.

## 1. temp 변수
```js
let a = 'hello';
let b = 'world';

let temp = a;
a = b;
b = temp;

console.log(a, b); // world hello
```

## 2. 구조 분해 할당(Destructing assignment)
```js
let a = 'hello';
let b = 'world';

[a, b] = [b, a];

console.log(a, b); // world hello
```

교환하려는 변수가 3개 이상인 경우도 사용 가능하다.
```js
let a = 'hello';
let b = 'world';
let c = 'korea';

[a, b, c] = [b, c, a];

console.log(a, b, c); // world korea hello
```