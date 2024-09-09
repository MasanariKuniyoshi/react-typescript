# Docker+React-Typescript

Docker Compose でのみの実装となっています。

# デフォルトのプロジェクトで作業を行う場合（sample-react）

## 初回構築

```bash
docker compose build
docker compose run --rm frontend sh -c  'cd sample-react && npm install'
```

## サーバーの起動

```bash
docker compose up -d
```

サーバー起動後、次のローカル URL で動けば完了です。 [http://localhost:8000/](http://localhost:8000/)<br>
サーバーを停止させるときは`docker compose stop`と実行します。

<br><br>

# 別名のプロジェクトで作業を行う場合

ここのリポジトリではコンテナー起動時に sample-react プロジェクトが自動で起動するようになっています。
別の名前でプロジェクトを作成したいときは以下の手順でお願いします。

## プロジェクトの作成

```bash
docker compose run --rm frontend sh -c 'npx create-react-app プロジェクト名 --template typescript'
```

## docker-compose.yml の修正

以下の部分を修正もしくわ削除してください。

```diff
services:
  frontend:
    ~
    volumes:
      - ./:/usr/src/app
-   command: sh -c 'cd sample-react && yarn start'
+   command: sh -c 'cd プロジェクト名 && yarn start'
    ~
```

## イメージの構築

```bash
docker compose build
```

## サーバーの起動

```bash
docker compose up -d
```

サーバー起動後、次のローカル URL で動けば完了です。 [http://localhost:8000/](http://localhost:8000/)<br>
サーバーを停止させるときは`docker compose stop`と実行します。
