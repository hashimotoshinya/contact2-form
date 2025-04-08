# 確認テスト（基礎講座）

Laravel + Docker を使った基礎的なWebアプリケーション開発環境です。  
お問い合わせの管理画面機能を実装しており、検索・詳細モーダル・削除機能などを含んでいます。

---

## 📦 使用技術

- PHP (Laravel)
- MySQL 8.0
- Nginx
- Docker / Docker Compose
- phpMyAdmin

---

## 🛠 セットアップ方法
- Dockerの環境構成
```
services:
  nginx:
    image: nginx:1.21.1
    platform: linux/amd64
    ports:
      - "80:80"
    volumes:
      - ./docker/nginx/default.conf:/etc/nginx/conf.d/default.conf
      - ./src:/var/www/
    depends_on:
      - php

  php:
    build: ./docker/php
    volumes:
      - ./src:/var/www/

  mysql:
    image: mysql:8.0.26
    platform: linux/amd64
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: laravel_db
      MYSQL_USER: laravel_user
      MYSQL_PASSWORD: laravel_pass
    command:
      mysqld --default-authentication-plugin=mysql_native_password
    volumes:
      - ./docker/mysql/data:/var/lib/mysql
      - ./docker/mysql/my.cnf:/etc/mysql/conf.d/my.cnf

  phpmyadmin:
    image: phpmyadmin/phpmyadmin
    environment:
      - PMA_ARBITRARY=1
      - PMA_HOST=mysql
      - PMA_USER=laravel_user
      - PMA_PASSWORD=laravel_pass
    depends_on:
      - mysql
    ports:
      - 8080:80
```
- ファイルの作成
```
views/
  ├── admin.blade.php
  ├── auth/
  │   ├── login.blade.php
  │   └── register.blade.php
  ├── confirm.blade.php
  ├── find.blade.php
  ├── index.blade.php
  ├── layouts/app.blade.php
  ├── thanks.blade.php
  └── welcome.blade.php
Controllers
  ├── AuthController.php
  ├── ContactController.php
  └── Controller.php
```
- Fortifyのインストール
 
## 🧩 編集ファイル

- コントローラー
  - `AuthController`
  - `ContactController`
  - `AdminController`
- ルーティング
  - `routes/web.php`
- マイグレーション
  - `contacts_table.php`
- シーディング
  - `Contactceeder.php`
- モデル
  - `Contact.php`


---
## 🧪 実装機能
- ユーザー登録、ログイン(Fortify使用)
- お問合せフォーム(バリテーション機能)
- 管理画面から検索、絞り込み、詳細からモーダル表示と削除
---
## 🏃 アクセス
|                 |          |
|-----------------|----------|
| お問合せ入力ページ | /        |
| お問合せ確認ページ | /confirm |
| サンクスページ    | /thanks   |
| 管理画面         | /admin    |
| ユーザ登録ページ  | /register |
| ログインページ    | /login    |
---
## 👤 作成者
橋本　伸也
