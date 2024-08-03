# Node.js 環境構築

## Node.js をインストール(macOS)

macOS にも環境を構築したくなったので Node.js のインストールから実施。

1. curl でインストールスクリプトをダウンロードし、実行

```sh
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.5/install.sh | bash
```

2. nvm を利用できるように下記のコマンド実行

```sh
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
```

3. nvm のバージョンを確認し、表示されれば OK

```sh
nvm --version
```

[https://github.com/nvm-sh/nvm#installing-and-updating](https://github.com/nvm-sh/nvm#installing-and-updating)

## nvm のコマンド一覧

nvm-windows のコマンドと少し違う？余裕があれば nvm の詳細を勉強予定。

## 利用可能なバージョンの一覧表示

```sh
nvm ls-remote
```

## バージョンを指定してインストール

```sh
nvm install 20.10.0
```
