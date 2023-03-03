---
title: How to return a value from an asynchronous callback function?
author: surfharu
date: 2023-03-02 09:00:00 +0800
categories: [javascript]
tags: [javascript, promise, asynchronous, stream] # TAG names should always be lowercase
---

The example below is a function that returns a value using a callback function at stream completion. After reading the file, the end callback function returns a value.
However, `totalBytes` is `undefined`. This is because `return totalBytes` is a value returned from the callback function of the `end` event.

```js
const fs = require('fs');

function getTotalBytes(filePath) {
  let totalBytes = 0;

  const readStream = fs.createReadStream(filePath);

  readStream.on('data', (chunk) => {
    totalBytes += chunk.length;
  });

  readStream.on('end', () => {
    return totalBytes;
  });
}

const filePath = 'example.txt';
const totalBytes = getTotalBytes(filePath);
console.log(totalBytes); // Output: undefined 
```

## Solution
If you modify it to return the `Promise` object, you can get the desired value.

```js
const fs = require('fs');

function getTotalBytes(filePath) {
  return new Promise((resolve, reject) => {
    let totalBytes = 0;

    const readStream = fs.createReadStream(filePath);

    readStream.on('data', (chunk) => {
      totalBytes += chunk.length;
    });

    readStream.on('end', () => {
      resolve(totalBytes);
    });

    readStream.on('error', (error) => {
      reject(error);
    });
  });
}

const filePath = 'example.txt';
getTotalBytes(filePath)
  .then((totalBytes) => console.log(totalBytes))
  .catch((error) => console.error(error));
```