# async/await

async/await は Promise のシンタックスシュガー
Promise を利用した非同期処理を同期的な見た目で記述できる

```js
async function someFunc() {
  const foo = await // Promiseを返す式;
  const bar = await // Promiseを返す式;
  // 前のawaitが完了するまで実行されない
  await // Promiseを返す式;
}
```

```js
const someFuncArrow = async () => {
  await // Promiseを返す式;
};
```
