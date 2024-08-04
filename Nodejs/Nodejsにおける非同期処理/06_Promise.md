# Promise

Promise は Callback の下記の弱点を解消した非同期処理

- ネストが深くなりがち
- 包括的なエラーハンドリングを行えない

※従来のループや条件分岐と組み合わせづらい課題は残っているのでこの問題を解消するには async/await の方を利用

Promise は非同期処理が完了したタイミングで成功か失敗かを返すオブジェクト

- 成功した場合は then メソッドにセットされた成功時のハンドラーが呼び出される
- 失敗した場合は catch メソッドにセットされたハンドラーが呼び出される

```js
const promiseFunc = new Promise((resolve, reject) => {
    // --- 非同期で行う処理を記述する ---

    if (/* errorが起きた時 */) {
        // エラーが起きた時はrejectを呼び出す
        return reject(/* エラー内容 */);
    }

    // 成功した時はresolveを呼び出す
    resolve(/* 成功時の内容 */);
});

promiseFunc.then(
    /* 成功時に実行する関数 */
).catch(
    /* 失敗時に実行する関数 */
);
```
