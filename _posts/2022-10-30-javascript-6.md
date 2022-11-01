---
title: 한글 자소 분리 문제 해결하기
author: surfharu
date: 2022-10-30 14:00:00 +0800
categories: [javascript]
tags: [javascript, nfc, nfd] # TAG names should always be lowercase
---

## Problem
Mac 에서 등록한 파일들의 한글 DB 검색이 되지 않았다.
1. 한글 파일명으로 된 파일 업로드 
2. 파일명을 추출하여 DB에 저장
3. DB에서 한글 검색이 안됨   

## Cause
Mac과 Windows의 한글 정규화 방식이 다름으로 인해 나타난 현상이다.

| **구분** | **사용** | **설명** | **예제** |
| --- | --- | --- |
| Mac | **NFD** | 모든 음절을 분해하여 자모 코드를 이용하여 저장하는 방식 | 한 => ㅎㅏㄴ |
| Windows | **NFC** | 모든 음절을 분해하고 다시 결합하여 저장하는 방식 | 한 => 한 |
| Html | **NFC(default)** | | |

한글을 변수에 저장하면 NFC 방식으로 정규화되는 것을 볼 수 있다.  
하지만 Mac 에서 등록한 첨부파일명을 추출하면 NFD 방식으로 되어 있으므로 NFC 로 방식 변환이 필요하다.
```js
let a = '사과';
let b = a.normalize('NFC');
let c = a.normalize('NFD');

console.log(a===b); // true
console.log(a===c); // false
```

## Solution
db 저장 전에 `normalize`를 통해 `NFC`로 변경해 준다. 
```js
let documentTitle = fileName.normalize('NFC');
```