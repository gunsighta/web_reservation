# Web Reservation Manager

ナイト系ポータルサイトの予約一元管理システム

## 概要

複数のナイト系ポータルサイトの予約情報を一元管理し、効率的な予約管理を実現するWebアプリケーションです。

## 主な機能

- 🔐 **ログイン認証** - セキュアなユーザー認証
- 📋 **ID・PASS登録** - 外部サイトの認証情報管理
- 📅 **予約状況表示** - 時間軸での予約状況一覧
- 📊 **エラーログ管理** - カテゴリ別エラー表示・管理
- ⚙️ **システム設定** - 自動取得・スケジュール設定
- 🤖 **自動データ取得** - 外部サイトからの情報自動同期

## 技術スタック

### フロントエンド
- React 18
- JavaScript (ES6+)
- Bootstrap 5
- Axios (HTTP client)

### バックエンド
- Node.js
- Express.js
- MySQL 8.0
- JWT認証
- Puppeteer (スクレイピング)

### 開発・運用
- Docker & Docker Compose
- npm
- Jest (テスト)

## クイックスタート

### 前提条件
- Node.js 16以上
- npm 8以上
- Docker & Docker Compose (推奨)

### 1. リポジトリのクローン
```bash
git clone https://github.com/gunsighta/web_reservation.git
cd web_res_manager
```

### 2. 依存関係のインストール
```bash
npm run install:all
```

### 3. 環境変数の設定
```bash
cp .env.example .env
# .envファイルを編集して設定を調整
```

### 4. データベースの起動（Docker使用）
```bash
npm run docker:up
```

### 5. 開発サーバーの起動
```bash
npm run dev
```

### 6. アクセス
- **フロントエンド**: http://localhost:3000
- **バックエンドAPI**: http://localhost:3001
- **phpMyAdmin**: http://localhost:8080

## デフォルトログイン情報

```
ユーザー名: admin
パスワード: admin123
```

## スクリプト一覧

| スクリプト | 説明 |
|------------|------|
| `npm run dev` | フロントエンド・バックエンド同時起動 |
| `npm run client:dev` | フロントエンドのみ起動 |
| `npm run server:dev` | バックエンドのみ起動 |
| `npm run build` | 本番用ビルド |
| `npm run test` | テスト実行 |
| `npm run docker:up` | Docker環境起動 |
| `npm run docker:down` | Docker環境停止 |
| `npm run install:all` | 全依存関係インストール |

## API エンドポイント

### 認証
- `POST /api/auth/login` - ログイン
- `POST /api/auth/logout` - ログアウト
- `GET /api/auth/me` - ユーザー情報取得

### 認証情報管理
- `GET /api/credentials` - 認証情報一覧
- `POST /api/credentials` - 認証情報登録
- `PUT /api/credentials/:id` - 認証情報更新
- `POST /api/credentials/:id/verify` - 認証情報検証

### 予約管理
- `GET /api/bookings` - 予約一覧
- `GET /api/bookings/:date` - 指定日の予約
- `POST /api/sync/women` - 女性情報同期
- `POST /api/sync/bookings` - 予約情報同期

### エラーログ
- `GET /api/errors` - エラーログ一覧
- `GET /api/errors/:type` - タイプ別エラー
- `PUT /api/errors/:id/resolve` - エラー解決

### システム設定
- `GET /api/settings` - 設定一覧
- `PUT /api/settings` - 設定更新

## ディレクトリ構造

```
web_res_manager/
├── client/                 # React フロントエンド
│   ├── public/
│   ├── src/
│   │   ├── components/     # Reactコンポーネント
│   │   ├── services/       # API通信
│   │   └── styles/         # スタイルシート
├── server/                 # Node.js バックエンド
│   ├── src/
│   │   ├── controllers/    # ルートハンドラー
│   │   ├── models/         # データモデル
│   │   ├── routes/         # ルート定義
│   │   ├── services/       # ビジネスロジック
│   │   └── middleware/     # ミドルウェア
├── database/               # データベース関連
└── docs/                   # ドキュメント
```

## 開発ワークフロー

### 1. 新機能開発
```bash
# 新しいブランチを作成
git checkout -b feature/new-feature

# 開発
# ...

# コミット・プッシュ
git add .
git commit -m "Add new feature"
git push origin feature/new-feature
```

### 2. テスト実行
```bash
npm run test
```

### 3. 本番ビルド
```bash
npm run build
```

## データベース管理

### バックアップ
```bash
docker exec web_res_manager_db mysqldump -u root -ppassword web_res_manager > backup.sql
```

### リストア
```bash
docker exec -i web_res_manager_db mysql -u root -ppassword web_res_manager < backup.sql
```

## トラブルシューティング

### よくある問題

1. **ポートが使用中の場合**
   ```bash
   # ポート確認
   lsof -i :3000
   lsof -i :3001

   # プロセス終了
   kill -9 <PID>
   ```

2. **Docker関連の問題**
   ```bash
   # コンテナリセット
   npm run docker:down
   docker system prune -f
   npm run docker:up
   ```

3. **依存関係の問題**
   ```bash
   # node_modules削除・再インストール
   rm -rf node_modules client/node_modules server/node_modules
   npm run install:all
   ```

## ライセンス

PROPRIETARY - 独占的ライセンス
Copyright (c) 2025 gunsighta. All rights reserved.
このソフトウェアおよび関連文書ファイル（以下「ソフトウェア」）は、著作権法および国際条約によって保護されています。無断での使用、複製、配布、改変、逆アセンブル、逆コンパイル、リバースエンジニアリングを禁止します。

## サポート

問題が発生した場合は、GitHubのIssuesに報告してください。