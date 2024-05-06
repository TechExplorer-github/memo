# HTMLの基本構造

## HTMLの基本

HTMLの1行目にはDOCTYPE宣言を記述します。  
DOCTYPEの次は一番外側の箱となるhtmlタグを記述します。  
続いてhtmlタグの中にheadタグとbodyタグを記述します。

```html
<!DOCTYPE html>
<html>
    <head></head>
    <body></body>
</html>
```

## head要素

HTMLで文字コードとタイトルは必須なのでhead要素の中に記述します。続いてページの概要文を記述します。  

スマートフォンで表示したときに正しく表示させるにはviewportを設定します。  
viewportで「width=device-width」を指定することで表示領域の幅を端末に合わせることができます。  
指定しなかった場合は、モバイルのとき表示が崩れるので必須になります。

```html
<head>
    <meta charset="UTF-8">
    <title>タイトル</title>
    <meta name="description" content="ページの概要文">
    <meta name="viewport" content="width=device-width">
</head>
```

## body要素

HTML5で新たに`<header><main><footer>`のタグが追加されました。  

headerタグ・・・セクション内におけるヘッダー情報(サイトのロゴの表示やナビゲーションの設置など)  
mainタグ・・・HTML文書内におけるメインコンテンツ  
footerタグ・・・セクション内のフッター情報(プライバシーポリシーや免責事項へのリンク、コピーライト)

```html
<body>
    <header class="header"></header>
    <main class="main"></main>
    <footer class="footer"></footer>
</body>
```

## コピーライトの書き方

コピーライトを表す「©」を表示するには「文字参照」という方法で記述します。  
「©」は「`&copy;`」になります。  
コピーライトは最初の発行の年と著作権者の氏名を記述します。  
(例)© 2023 Taro Yamada

```html
<p class="copyright">&copy; 2023 Taro Yamada</p>
```

## HTMLにコメントを記述する

HTMLにコメントを記述する場合は、「`<!--`」と「`-->`」で囲みます。

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>タイトル</title>
        <meta name="description" content="ページの概要文">
        <meta name="viewport" content="width=device-width">
    </head>
    <body>

        <!-- headerここから -->
        <header class="header"></header>
        <!-- headerここまで -->

        <!-- mainここから -->
        <main class="main"></main>
        <!-- mainここまで -->

        <!-- footerここから -->
        <footer class="footer"></footer>
        <!-- footerここまで -->

    </body>
</html>
```
