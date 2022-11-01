---
title: JSDoc 활용하기
author: surfharu
date: 2022-10-30 14:00:00 +0800
categories: [javascript]
tags: [javascript, jsdoc] # TAG names should always be lowercase
---

## JSDoc 이란? 
Javascript 소스코드 파일에 주석을 달기위해 사용되는 마크업언어이다.
> [jsdoc](https://jsdoc.app/)

## JSDoc의 주요 기능
- 자동으로 API 문서 생성
- 타입 정의 및 추론

## 기본 문법
함수
```js
/** 
 * 정수의 합산
 * @function add
 * @param {number} a 0 이상의 정수
 * @param {number} b 0 이상의 정수
 * @returns {number} a + b
 */
const add = (a, b) => a + b;
```

변수
```js
/** @type {string} */
let str;

/** @type {number} */
let num;

/** @type {boolean} */
let bool;

/** @type {*} */
let any;

/** @type {?} */
let unknown;

/** @type {number[]} */
let nums;

/** @type { {id: number, content: string, completed: boolean} } */
let obj;

/** @type {string|number} */
let union;

/** @type {Array<{ id: number, content: string, completed: boolean }>} */
let generic;
```

## 문서화 하기
1. `jsdoc` 설치하기
```bash
npm install -g jsdoc
```

2. `jsdoc` 실행하기  
out 폴더에 api 문서가 생성된다.
```bash
jsdoc ./index.js
```

## 폴더 전체 문서화하기 
1. `jsdoc.config.json` 파일을 루트 경로에 추가
```yaml
{
    "plugins": [],
    "recurseDepth": 10,
    "source": {
        "includePattern": ".+\\.js(doc|x)?$",
        "excludePattern": "(^|\\/|\\\\)_",
        "exclude": [ "node_modules/" ]
    },
    "sourceType": "module",
    "tags": {
        "allowUnknownTags": true,
        "dictionaries": ["jsdoc","closure"]
    },
    "templates": {
        "cleverLinks": false,
        "monospaceLinks": false
    }
}
```

2. 실행하기 
src 폴더 아래 모든 파일들이 문서화 된다.
```bash
jsdoc -r -c jsdoc.config.json ./src
```

## 메인 화면에 README.md 추가하는 방법
- `jsdoc.config.json` 설정 

```yaml
    "plugins": [
        "plugins/markdown"
        ],
    "opts": {
        "encoding": "utf8",
        "readme": "README.md"
    }
```

- `README.md` 파일 편집  

```text
# 나의 문서

## [add](global.html#add)
## [subtraction](global.html#subtraction)
```

- 문서를 다시 생성  

```bash
jsdoc -r -c jsdoc.config.json ./src
```

메인 화면에 README.md 파일의 내용이 보인다.

![](/assets/images/javascript-1-1.png)
