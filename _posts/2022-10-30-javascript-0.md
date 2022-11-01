---
title: Convert between image and base64
author: surfharu
date: 2022-10-30 14:00:00 +0800
categories: [javascript]
tags: [javascript, convert, base64, image] # TAG names should always be lowercase
---

## Convert image to base64
```html
<img id="image" src="/image.png">
<canvas id="canvas"></canvas>
```

```js
const canvas = document.getElementById('canvas');
const ctx = canvas.getContext('2d');
const image = document.getElementById('image');

ctx.drawImage(image, 0, 0);

console.log(canvas.toDataURL()); //return base64
```

## Convert base64 to image
```js
const img = await readAsImage(signData);
```

```js
export function readAsImage(src) {
  return new Promise((resolve, reject) => {
    const img = new Image();
    img.onload = () => resolve(img);
    img.onerror = reject;
    if (src instanceof Blob) {
      const url = window.URL.createObjectURL(src);
      img.src = url;
    } else {
      img.src = src;
    }
  });
}
```