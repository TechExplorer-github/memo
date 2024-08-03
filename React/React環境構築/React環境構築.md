# React 環境構築

## Vite を使った環境構築

1. Vite プロジェクトを生成

```sh
npm create vite@latest
```

カレントディレクトリに展開する場合

```sh
npm create vite@latest .
```

2. プロジェクトのフォルダに移動してライブラリインストール&実行

```sh
cd [Project name]
npm install
npm run dev
```

## Create React App はもう非推奨

実際に下記のコマンドで実行すると「8 vulnerabilities (2 moderate, 6 high)」の警告が出る。(2024/01 時点)

```sh
npx create-react-app {プロジェクト名}
```

github の方も 2023/06/15 で更新が止まっている

https://github.com/facebook/create-react-app

Next.js などのフレームワークを使わないで React 単体で開発するときは後継の Vite を使うのが良さそう。
