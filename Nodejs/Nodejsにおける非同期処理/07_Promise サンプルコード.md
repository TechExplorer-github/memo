# Promise サンプルコード

then や catch はつなぐこと(チェイン)可能
ネストが深くなることを防ぎ、包括的なエラーハンドリングが可能

```js
const promiseX = (x) => {
  return new Promise((resolve, reject) => {
    if (typeof x === "number") {
      resolve(x);
    } else {
      reject(new Error("return error"));
    }
  });
};

const logAndDouble = (num) => {
  console.log(num);
  return num * 2;
};

// thenで成功時をつなげる、失敗時はcatchに飛ぶ
promiseX(1)
  .then((data) => logAndDouble(data))
  .then((data) => logAndDouble(data))
  .catch((error) => console.log(error));
```
