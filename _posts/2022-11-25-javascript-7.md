---
title: 객체를 직렬화(Serialization), 역직렬화(Deserialization) 하기
author: surfharu
date: 2022-11-25 14:00:00 +0800
categories: [javascript]
tags: [javascript, object, serialization] # TAG names should always be lowercase
---

## 직렬화(Serialization)란 ?
객체에 저장된 데이터를 스트림에 쓰거나 네트워크에 전송하기 위해서는 연속적인 serial 데이터로 변환이 필요한데 이것을 직렬화라고 한다.  
즉, `Object`형태를 `String`형태로 바꾸는 작업을 말한다.

## 예제 
`JSON`을 활용하여 직렬화와 역직렬화를 해본다.
```js
let book = { name: 'sky', pages: 500 };
let serialize_book = JSON.stringify(book);  // 직렬화
let deserialzie_book = JSON.parse(serialize_book);  // 역직렬화

console.log('type: ', typeof serialize_book); // type: string
console.log('type: ', typeof deserialzie_book); // type: object
```