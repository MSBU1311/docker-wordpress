# 🐳 Docker WordPress Template

**WordPress × Docker 開発環境**

---

## 概要

このリポジトリは、**Docker で WordPress をすぐに立ち上げられる開発用テンプレート**です。

WordPress 本体、MySQL、phpMyAdmin、MailHog を自動で構築します。

以下のような用途に最適です

- WordPress のテーマ／プラグイン開発
- ローカルでの検証環境構築
- 案件・学習用の再現性あるセットアップ

---

## 動作環境（推奨）

| ツール         | バージョン                   |
| -------------- | ---------------------------- |
| Docker Desktop | 4.x 以上                     |
| Git            | 2.40 以上                    |
| OS             | macOS / Windows / Linux 対応 |
| エディタ       | Visual Studio Code 推奨      |

---

## ディレクトリ構成

docker-wordpress-template/
├── docker-compose.yml # コンテナ設定
├── php.ini # PHP 設定ファイル
├── .env.sample # 環境変数サンプル
├── .gitignore # 除外設定
├── README.md # 本ドキュメント
 └── docker-data/
  └── wordpress/
   └── themes/
    └── your-theme/ # 自作テーマをここに配置

---

## 利用できるサービス

| サービス名     | URL                                            | 説明                   |
| -------------- | ---------------------------------------------- | ---------------------- |
| **WordPress**  | [http://localhost:8080](http://localhost:8080) | メインサイト           |
| **phpMyAdmin** | [http://localhost:8081](http://localhost:8081) | データベース管理ツール |
| **MailHog**    | [http://localhost:8025](http://localhost:8025) | メール送信テスト       |
| **MySQL**      | `db:3306`                                      | データベースコンテナ   |

---

## 使い方（初期セットアップ）

### ① リポジトリをクローン

```
git clone https://github.com/< your-username >/docker-wordpress-template.git <your-directoryname>
cd docker-wordpress-template
```

< your-directoryname >部分を任意の名前に変更してください。

② .env を作成

```
cp .env.sample .env
```

.env を開いて、必要に応じてパスワードなどを変更します。

③ コンテナを起動

```
docker-compose up -d
```

起動後、以下にアクセスできます

- WordPress → http://localhost:8080
- phpMyAdmin → http://localhost:8081
- MailHog → http://localhost:8025

④ コンテナを停止

```
docker-compose down
```

データベースを含めて完全に削除する場合 👇

```
docker-compose down -v
```

🧾 PHP 設定（php.ini）

```
upload_max_filesize = 64M

post_max_size = 64M

memory_limit = 512M

max_execution_time = 300

display_errors = On

error_reporting = E_ALL
```

💡 開発時は display_errors=On で OK。

本番運用時は Off に変更しましょう。

⭐️ 補足メモ

- .env は Git 管理対象外（.gitignore に登録済み）
- .env.sample は共有用テンプレートとしてリポジトリに含めます
- docker-data/wordpress/themes/ 以下に自作テーマを置くことで開発可能
- twentytwenty〜 系テーマは自動生成されるため、Git 管理不要

⚠️ 注意：テンプレートを自分のプロジェクトにコピーした後このテンプレートを自身のフォルダに構築したら、.gitignore の以下 4 行の コメントアウトを解除 してください

```
# docker-compose.yml

# php.ini

# .gitignore

# .env.sample
```
