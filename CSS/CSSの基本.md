# CSS の基本

## CSS の文字コード

CSS ファイルの 1 行目には文字コードを書きます。

```css
@charset "utf-8";
```

## ブラウザの既定のスタイルを解除

ブラウザによってデフォルトのスタイルが独自に設定されています。  
ブラウザによって見た目が変わったり、不要な余白ができたりしないようにデフォルトのスタイルを解除した方がコーディングがしやすくなります。

各要素にはデフォルトで余白(margin、padding など)が設定されているのですべての要素(\*)と疑似要素(::before、::after)に対して余白を 0 にします。

```css
*,
::before,
::after {
  padding: 0;
  margin: 0;
}
```

## 要素の幅と高さの計算方法を指定する

デフォルトだと要素のサイズは padding や border などの値を含めない設定になっています。  
box-sizing で border-box を指定することで padding や border のサイズを計算に含め、計算方法をシンプルにできます。

```css
*,
::before,
::after {
  box-sizing: border-box;
}
```

## テキストのフォントを指定する

ページ全体のフォントは body 要素に対して指定します。

```css
body {
  font-family: sans-serif;
}
```

## HTML で使用する画像のサイズ

大きな画像をそのまま配置すると親要素から飛び出してしまうので img 要素の最大幅を親要素の範囲内で収まるように指定します。  
最大幅の指定は max-width を 100%にします。

```css
img {
  max-width: 100%;
}
```

## %と vw の違い

%は親が基準  
vw はブラウザの横幅が基準
