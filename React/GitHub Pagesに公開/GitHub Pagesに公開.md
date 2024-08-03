# react-vite-github-pages

## Vite で作成した React のプロジェクトを GitHub Pages で公開するまでの手順

1. Vite で React のプロジェクトを作成

下記のコマンドを実行し、FW は React、構成は TypeScript + SWC を選択する

```sh
npm create vite@latest .
```

2. ローカル環境で動作確認

```sh
npm install
npm run dev
```

3. vite.config.ts を編集

process.env を使うので下記のライブラリをインストール

```sh
npm i --save-dev @types/node
```

vite.config.ts

```ts
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react-swc";

export default defineConfig({
  base: process.env.GITHUB_PAGES ? "react-vite-github-pages" : "./", // この行を追加
  plugins: [react()],
});
```

4. プロジェクトをビルド

```sh
npm run build
cp -r dist docs
```

5. ソースコードを push

6. GitHub Pages で公開
   1. GitHub の Settings タブをクリックし、Pages を開く
   2. Branch で公開するブランチとディレクトリは/docs を選択し、Save する
   3. Actions でデプロイが始まるので完了するとアクセスできるようになる
