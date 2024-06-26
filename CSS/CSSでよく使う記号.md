# CSSでよく使われる記号

## 「#」(シャープ)と「.」(ドット)の使い方

「#」と「.」の使い分けは下記になります。  
「#」: 指定したidにCSSスタイルを適用する場合  
「.」: 指定したclassにCSSスタイルを適用する場合

```css
/* id="sample1"の要素にスタイルを適用 */
#sample1 {
    color: #000000;
}

/* class="sample2"の要素にスタイルを適用 */
.sample2 {
    color: #000000
}
```

## 「,」（カンマ）の使い方

複数の要素に同じCSSスタイルを適用するときに使います。  

「,」を使わない場合

```css
.sample1 {
    color: #000000;
}

.sample2 {
    color: #000000;
}
```

「,」を使う場合

```css
.sample1, .sample2 {
    color: #000000;
}
```

## 「*」の使い方

すべての要素にスタイルを適用するときに使います。

```css
/* 全ての要素に適用 */
* {
    color: #000000;
}

/* divタグの配下の要素全てに適用 */
div * {
    color: #000000;
}
```

## 「>」の使い方

指定した要素の直下にある要素にスタイルを適用するときに使います。  
※子要素にのみ適用するので孫要素には適用されません。

```css
/* divタグの直下のpタグにスタイルを適用 */
div > p {
    color: #000000;
}
```

## 「+」(プラス)の使い方

指定した要素に隣接する要素にスタイルを適用するときに使います。  
※手前の要素は対象外になる。

```css
/* class="sample1"に隣接するpタグにスタイルを適用 */
.sample1 + p {
    color: #000000;
}
```

## 「~」(チルダ)の使い方

指定した要素の後ろにある要素全てに適用するときに使います。

```css
/* class="sample1"の後ろにあるpタグ要素全てに適用 */
.sample1 ~ p {
    color: #000000;
}
```
