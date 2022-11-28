---
title: script 문자열 모두 치환하기 
author: surfharu
date: 2022-11-28 14:00:00 +0800
categories: [javascript]
tags: [javascript, replace, replaceAll] # TAG names should always be lowercase
---

script 에서 문자열 모두를 치환하기 위해서는 주로 2가지 방법을 쓴다.

## 1. replace + 정규표현식
`g` : 모든 값에 대한 검사  
`i` : 대소문자 구분 안함  
```js
let str = 'apple orange apple mango';
console.log(str.replace(/apple/gi, 'mango')); // 결과: mango orange mango mango
```

## 2. replaceAll
```js
let str = 'apple orange apple mango';
console.log(str.replaceAll('apple', 'mango')); // 결과: mango orange mango mango
```

단, `replaceAll` 함수는 아래 브라우저 버전 이상에서만 동작한다. 
![](/assets/images/script-8-0.png)

