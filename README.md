# Livewire スターターキット  

<img alt="Static Badge" src="https://img.shields.io/badge/wsl2-w?style=plastic&logo=linux&logoColor=000000&labelColor=%23FCC624&color=%23FCC624"> <img alt="Static Badge" src="https://img.shields.io/badge/ubuntu-u?style=plastic&logo=ubuntu&logoColor=%23ffffff&labelColor=%23E95420&color=%23E95420"> <img alt="Static Badge" src="https://img.shields.io/badge/debian-l?style=plastic&logo=debian&logoColor=ffffff&labelColor=A81D33&color=A81D33">  
<img alt="Static Badge" src="https://img.shields.io/badge/Docker-d?style=plastic&logo=docker&logoColor=%23ffffff&labelColor=%232496ED&color=%232496ED">
<img alt="Static Badge" src="https://img.shields.io/badge/NGINX-n?style=plastic&logo=nginx&logoColor=%23ffffff">
<img alt="Static Badge" src="https://img.shields.io/badge/MySQL-m?style=plastic&logo=mysql&logoColor=%23ffffff&labelColor=%234479A1&color=%234479A1">
<img alt="Static Badge" src="https://img.shields.io/badge/php-p?style=plastic&logo=php&logoColor=%23ffffff&labelColor=%23777BB4&color=%23777BB4">
<img alt="Static Badge" src="https://img.shields.io/badge/livewire-w?style=plastic&logo=livewire&logoColor=%23ffffff&labelColor=%234E56A6&color=%234E56A6">  
<img alt="Static Badge" src="https://img.shields.io/badge/Laravel12-l?style=plastic&logo=laravel&logoColor=%23ffffff&labelColor=%23FF2D20&color=%23FF2D20">
<img alt="Static Badge" src="https://img.shields.io/badge/bun-b?style=plastic&logo=bun&logoColor=%23ffffff&labelColor=%23000000&color=%23000000">
<img alt="Static Badge" src="https://img.shields.io/badge/bootstrap-b?style=plastic&logo=bootstrap&logoColor=%23ffffff&labelColor=%237952B3&color=%237952B3">
<img alt="Static Badge" src="https://img.shields.io/badge/vite-v?style=plastic&logo=vite&logoColor=%23ffffff&labelColor=%23646CFF&color=%23646CFF">  

## プロジェクト概要  
本リポジトリは Laravel 公式 Starter Kits（Jetstream / Livewire）で
生成される構成をベースに、Docker 環境でそのまま動作するよう整えた
学習・検証用のサンプルアプリケーションです。

※ Starter Kit をローカル環境に直接インストールするのではなく、  
Docker コンテナ内で完結させる構成を検証目的で採用しています。

## 学習・検証目的
- bun / npm によるフロントエンド依存管理とビルド速度の差の検証  
- Laravel Starter Kit を利用した場合と、ゼロから構成する場合の
  初期開発効率・保守性の比較

## 主な機能

- ユーザー認証（Laravel の標準的な認証フロー）
- 投稿（Post）モデルと CRUD 操作（ユーザーに紐づく投稿）
- Livewire コンポーネント（Flux / Volt を利用）によるリアクティブな操作
- View コンポーネントと Blade テンプレート
- Vite + TailwindCSS によるモダンなフロントエンドビルド
- PHPUnit / Laravel テストでの自動テスト構成

## 使用技術
| カテゴリ | 使用技術 |
| :--- | :--- |
| **Backend** | Laravel 12, Jetstream, PHP_CodeSniffer |
| **Frontend** | Livewire, Tailwind CSS, flux, bun |
| **Infrastructure** | Docker Compose (App / Node / MySQL / Nginx) |
| **OS Environment** | Linux container based |
| **Database** | MySQL 8.x |

## セットアップ手順

### 1. インフラのビルドと起動
```
docker compose build
docker compose up -d
docker exec -it app bash
```

### 2. Laravel Starter Kit の構築
```
composer global require laravel/installer
export PATH=$HOME/.composer/vendor/bin:$PATH
source ~/.bashrc
laravel new project
# Starter Kit: Livewire
# Frontend tooling: bun（npm は使用しない）
php artisan migrate
chown -R www-data:www-data storage bootstrap/cache
chmod -R 775 storage bootstrap/cache
```
### 3. フロントエンド依存関係
```
bun install
bun run build
```

## ディレクトリ構成（主要部分）

ルート: `example/`

- `app/` - アプリの PHP ソース（コントローラ、モデル、プロバイダ、Livewire コンポーネントなど）
  - `Http/Controllers/` - コントローラ
  - `Livewire/` - Livewire コンポーネント（Actions / Auth / Settings など）
  - `Models/` - Eloquent モデル（例: `User.php`, `Post.php`）
- `bootstrap/` - フレームワーク初期化
- `config/` - 設定ファイル群
- `database/` - マイグレーション、ファクトリ、シーダー、SQLite ファイル
  - `migrations/` - テーブル定義（投稿テーブルや user_id を追加するマイグレーションあり）
- `public/` - 公開ディレクトリ（Vite のビルド成果物が `public/build` に配置されます）
- `resources/` - Blade テンプレート、JS/CSS ソース（`resources/js`, `resources/css`）
- `routes/` - ルーティング（`web.php`, `auth.php` など）
- `tests/` - PHPUnit / Laravel のテスト
- `vendor/` - Composer 管理の依存ライブラリ

## 設計・実装の特徴
- Livewire を使うことで、JavaScript を大量に書かずに「ページ上の小さなインタラクション（リアクティブ UI）」を実装できます。サーバー側で状態を持ち、部分的に DOM を差分更新します。
- Flux / Volt は Livewire エコシステムの拡張で、状態管理や UI コンポーネント化をより整然と行うための小さなレイヤーです。
- フロントエンドは Vite + Tailwind を採用しており、開発時のホットリロードや高速ビルドが可能です。
- データベースは開発用に SQLite を使いやすく設定しており、簡単にローカルで試せます。本番では MySQL / PostgreSQL 等に切り替えて使います。
- テストが最初から用意されているため、機能追加時に `php artisan test` で回帰をチェックできます。