# ループ処理で async/await

```js
const main = async () => {
  for (let i = 0; i < 10; i++) {
    const flag = await asyncFunction();
    if (flag) {
      break;
    }
  }
};
```
