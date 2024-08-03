# JSX でマークアップを書く

上で見たマークアップ構文は、JSX と呼ばれるものでほとんどの React プロジェクトでは JSX が使用されています。

JSX の構文

- HTML タグは先頭小文字
- React のコンポーネントは先頭大文字
- タグは閉じる必要がある(例: `<br />`)
- コンポーネントは複数の JSX タグを return できない
- <div>...</div>や空の<>...</>ラッパのような共通の親要素で囲む必要がある

```diff javascript
function AboutPage() {
  return (
+    <>
      <h1>About</h1>
      <p>Hello there.<br />How do you do?</p>
+    </>
  );
}
```

- CSS クラスを className で指定(JavaScript で class は予約語なので)

```javascript
<img className="avatar" />
```
