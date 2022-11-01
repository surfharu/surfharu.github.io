---
title: 클로져(Closure)
author: surfharu
date: 2022-10-30 14:00:00 +0800
categories: [javascript]
tags: [javascript, closure] # TAG names should always be lowercase
---


## 클로져(Closure)란 ?
외부함수보다 내부함수가 더 오래 유지되는 경우, 외부 함수 밖에서 내부함수가 호출되더라도 외부함수의 지역 변수에 접근할 수 있는데 이러한 함수를 클로저(Closure)라고 한다.

## 활용
주로 현재 상태를 기억하고 유지하기 위해 사용한다.  
기존에 전역변수로 상태 관리를 하던 것들을 클로저를 통해 관리 할 수 있다.

## 예제
지역 변수 x 의 상태 값이 유지되는 것을 확인 할 수 있다. 
```js
const outerFunc = () => {
  var x = 0;
  const innerFunc = () => {
    return x++;
  }
  return innerFunc;
}

let mFunc = outerFunc();
console.log(mFunc()); // 0
console.log(mFunc()); // 1
console.log(mFunc()); // 2
```