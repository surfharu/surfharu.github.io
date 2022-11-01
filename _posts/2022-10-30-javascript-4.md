---
title: Script cache 갱신하기
author: surfharu
date: 2022-10-30 14:00:00 +0800
categories: [javascript]
tags: [javascript, cache] # TAG names should always be lowercase
---

## Problem
스크립트 내용을 수정 후 캐시로 인해 반영이 안되는 경우가 종종 발생한다.

## Solution
```html
<script language="JavaScript" src="js/myscript.js"></script>
```

스크립트 참조 주소에 파라미터를 추가(`?v=1`)하여 캐시가 갱신 되도록 해준다.
```html
<script language="JavaScript" src="js/myscript.js?v=1"></script>
```