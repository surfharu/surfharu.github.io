---
title: Object copy (shallow vs deep)
author: surfharu
date: 2022-10-30 14:00:00 +0800
categories: [javascript]
tags: [javascript, object, copy, lodash] # TAG names should always be lowercase
---

## shallow copy (얕은 복사)
참조값(주소값)의 복사를 의미한다.

```js
const obj1 = { no: 1 };
const obj2 = obj1;

obj2.no = 2;

console.log(obj1.no); // 2
console.log(obj1 === obj2); // true
```

## deep copy (깊은 복사)
값 자체를 새로운 메모리에 할당하여 복사한다.

### assign 활용
- 1 depth : O
- more than 2 depths : X

```js
const obj1 = { no: 1, position: {x: 0, y: 0} };
const obj2 = Object.assign({}, obj1);

obj2.no = 2;
obj2.position.x = 1;

console.log(obj1); // { no: 1, position: {x: 1, y: 0} }
console.log(obj2); // { no: 2, position: {x: 1, y: 0} }
console.log(obj1 === obj2); // false
```

### 스프레드 연산자 활용
- 1 depth : O
- more than 2 depths : X

```js
const obj1 = { no: 1, position: {x: 0, y: 0} };
const obj2 = { ...obj1 };

obj2.no = 2;
obj2.position.x = 1;

console.log(obj1); // { no: 1, position: {x: 1, y: 0} }
console.log(obj2); // { no: 2, position: {x: 1, y: 0} }
console.log(obj1 === obj2); // false
```

### JSON 활용
- 1 depth : O
- more than 2 depths : O

```js
const obj1 = { no: 1, position: {x: 0, y: 0} };
const obj2 = JSON.parse(JSON.stringify(obj1));

obj2.no = 2;
obj2.position.x = 1;

console.log(obj1); // { no: 1, position: {x: 0, y: 0} }
console.log(obj2); // { no: 2, position: {x: 1, y: 0} }
console.log(obj1 === obj2); // false
```

### 라이브러리(`loadash`) 활용
- 1 depth : O
- more than 2 depths : O

```js
import loadash from 'lodash';

const obj1 = { no: 1, position: {x: 0, y: 0} };
const obj2 = loadash.cloneDeep(obj1);

obj2.no = 2;
obj2.position.x = 1;

console.log(obj1); // { no: 1, position: {x: 0, y: 0} }
console.log(obj2); // { no: 2, position: {x: 1, y: 0} }
console.log(obj1 === obj2); // false
```