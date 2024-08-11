# Express 環境構築

## 環境構築手順

Node.js のプロジェクトの初期化

```sh
npm init -y
```

Express.js と API の開発で利用するライブラリをインストール

```sh
npm i express dotenv cors helmet
```

TypeScript をインストール

```sh
npm i -D typescript
```

ライブラリの型定義をインストール

```sh
npm i -D @types/node @types/express @types/dotenv @types/cors @types/helmet
```

TypeScript プロジェクトの初期設定ファイル(tsconfig.json)を作成

```sh
npx tsc --init
```

.env ファイルを作成
PORT を記載

```sh
PORT=7000
```

エントリーポイントの src/index.ts を作成

```ts
import * as dotenv from "dotenv";
import express from "express";
import cors from "cors";
import helmet from "helmet";

/**
 * App Variables
 */
dotenv.config();

if (!process.env.PORT) {
  console.log(`Not Found PORT`);
  process.exit(1);
}

const PORT: number = parseInt(process.env.PORT as string, 10);

const app = express();

/**
 *  App Configuration
 */
app.use(helmet());
app.use(cors());
app.use(express.json());

/**
 * Server Activation
 */
app.listen(PORT, () => {
  console.log(`Listening on port ${PORT}`);
});
```

ts-node-dev のライブラリをインストール
ts ファイルを js ファイルにコンパイルすることなく、起動することができ、さらに監視モードで素早く再起動が使用できる

```sh
npm i -D ts-node-dev
```

package.json の scripts に下記を追加

```json
  "scripts": {
    "dev": "ts-node-dev --respawn --pretty --transpile-only src/index.ts"
  },
```

下記のコマンドで起動

```sh
npm run dev
```

## MySQL を追加する

mysql のコンテナを作成し、接続するようにするため docker-compose.yml を下記のように作成

```yml
services:
  backend:
    container_name: backend
    image: node:20
    working_dir: /app
    tty: true
    depends_on:
      - db
    ports:
      - 8000:8000
    volumes:
      - ./src:/app
    networks:
      - backend

  db:
    container_name: db
    image: mysql:8
    restart: always
    ports:
      - 3306:3306
    environment:
      - MYSQL_ROOT_PASSWORD=${MYSQL_ROOT_PASSWORD}
      - MYSQL_HOST=${MYSQL_HOST}
      - MYSQL_USER=${MYSQL_USER}
      - MYSQL_PASSWORD=${MYSQL_PASSWORD}
      - MYSQL_DATABASE=${MYSQL_DATABASE}
    volumes:
      - ./db/conf.d:/etc/mysql/conf.d
      - ./db/data:/var/lib/mysql
    networks:
      - backend

volumes:
  mysql:

networks:
  backend:
```

変数部分は.env から読み込まれるので.env を下記のように作成

```sh
MYSQL_ROOT_PASSWORD=password
MYSQL_HOST=localhost
MYSQL_USER=test
MYSQL_PASSWORD=password
MYSQL_DATABASE=test_database
```

db/conf.d/my.cnf は下記のように作成

```sh
[mysqld]
default-time-zone = 'Asia/Tokyo'
character-set-server = utf8mb4
collation-server = utf8mb4_bin

[client]
default-character-set = utf8mb4
```

docker のコンテナを起動

```sh
docker　compose up -d
```

backend のコンテナ内に入るには下記のコマンドを実行

```sh
docker　compose exec backend /bin/bash
```

後は同様に環境構築をしていけば OK
