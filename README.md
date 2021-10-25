## はじめに

このリポジトリを自分のリポジトリにforkします。その後、自分のリポジトリでcloneを実行し作業PCでコーディングができるようにしてください。

## 準備

このプロジェクトのルートディレクトリまで移動してください。

```bash
cd hogehoge/laravel-study
```

## Dockerの使い方

### Dockerイメージのビルド

```bash
docker compose build --no-cache
```

このコマンドで開発に必要なサーバー環境をビルドすることができます。

### Dockerコンテナの起動

```bash
docker compose up -d
```

ビルドしたコンテナを起動します。起動することで、PHPが実行されるサーバーが作業PCで稼働するので、このコマンドを実行してから開発作業することを忘れないでください。

### Dockerコンテナ上でPHPコマンドを実行する

```bash
docker compose exec app php -v
```

主に`artisan`コマンドを実行するときに利用します。
Laravelのインストールについては後述。

### Dockerコンテナ上でComposerコマンドを実行する

```bash
docker compose exec app composer --version
```

主に`composer`コマンドを実行するときに利用します。
Laravelのインストールや、PHPの外部パッケージのインストールに利用されます。
Laravelのインストールについては後述。

### Dockerコンテナ上でNodeコマンドを実行する

```bash
docker compose run --rm node --version
```

```bash
docker compose run --rm node npm -v
```

主にNodeパッケージのインストールや、ReactやVue.jsなどJavaScriptやSassのコンパイル時に利用します。

### Dockerコンテナの停止

```bash
docker compose down
```

### Dockerボリュームの削除

```bash
docker compose down --volumes
```

コンテナの停止時にMySQLのデータを削除します。

### その他

Dockerの公式ページなどを参照してください。

---

## Laravelのインストールについて

このプロジェクトではLaravelのバージョンアップ時の環境修正を考慮して**Laravelをインストールしていない状態**で作成されています。

Laravelのインストールについて学習しながら環境の構築を進めていきましょう。

[Laravelの日本語訳された公式ページ](https://readouble.com/)も読んで理解を深めることを推奨します。

また、バージョンアップによって動作が変更されることもあります。バージョン情報のキャッチアップも積極的に行いましょう。

### Dockerイメージのビルド（初回 or 環境設定変更時）

```bash
docker compose build --no-cache
```

### Dockerコンテナの起動

```bash
docker compose up -d
```

開発するときは必ずコンテナを起動してください。

### Laravelのインストール

Laravelのインストールには`composer`を利用します。

```bash
docker compose exec app composer create-project laravel/laravel .
```

### ブラウザで起動確認

http://localhost/

### データベース設定

`/backend/.env`の書き部分を変更してください。

```
DB_CONNECTION=mysql
DB_HOST=db
DB_PORT=3306
DB_DATABASE=app
DB_USERNAME=root
DB_PASSWORD=root
```

`artisan`コマンドでDBマイグレーションをしてください。

```bash
docker compose exec app php artisan migrate
```

### その他、言語/時間設定

レクチャーにてご説明します。

