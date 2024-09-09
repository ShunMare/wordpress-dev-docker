# WordPress Docker 開発環境 (Windows用)

このプロジェクトは、WindowsでWordPressのローカル開発環境をDocker上に簡単に構築するためのテンプレートです。

## 前提条件

- [Git for Windows](https://gitforwindows.org/)
- [Docker Desktop for Windows](https://www.docker.com/products/docker-desktop)

## セットアップ手順

1. **リポジトリのクローン**
   - GitHubの[wordpress-dev-docker](https://github.com/ShunMare/wordpress-dev-docker)ページに行き、「Code」ボタンをクリックし、「Download ZIP」を選択します。  
    (もしくは`git  clone`します。)
   - ダウンロードしたZIPファイルを任意の場所に解凍します。

2. **プロジェクト名の設定**
   - 解凍したフォルダ内の `project-name` フォルダを、あなたのプロジェクト名に変更します。
   - 例: `my-awesome-theme`

3. **環境変数の設定**
   - `.env.example` ファイルをコピーして `.env` という名前で保存します。
   - `.env` ファイルをテキストエディタ（メモ帳など）で開き、以下の変数を設定します。  
    `PROJECT_NAME`はあなたのプロジェクト名を設定します。  

    ```bash
    PROJECT_NAME=your-project-name
    WORDPRESS_DB_HOST=db
    DB_NAME=wordpressdb
    DB_USER=wordpressuser
    DB_PASSWORD=wordpresspass
    ```

4. **Docker Desktopの起動**
   - Docker Desktopを起動し、右下のタスクトレイでDockerアイコンが緑色になるのを待ちます。（デスクトップアプリ起動すれば基本的に良いはずです。）

5. **Dockerコンテナの起動**
   - プロジェクトフォルダ内で右クリックし、「ここでPowerShellウィンドウを開く」を選択します。  
    `dockerfile-wordpress`があるところまでディレクトリを移動する必要があります。
   - 開いたウィンドウに以下のコマンドを入力し、Enterを押します。

     ```bash
     docker-compose up -d
     ```

6. **WordPressのセットアップ**
   - ブラウザで `http://localhost:8000` にアクセスします。
   - 画面の指示に従って`WordPress`のインストールを完了します。

## テーマの追加

1. `my-awesome-theme` フォルダ（または、あなたが設定したプロジェクト名のフォルダ）を開きます。

2. ここに、作成する`theme`の*中身*をコピーします。  
    この中身のファイルを`git`管理することをお勧めします。  
    例）

    ```bash
    my-awesome-theme/
    ├─.vscode
    ├─.git
    ├─.gitignore
    ├─index.php
    ├─style.css
    └─assets
        ├─css
        ├─fonts
        │  └─NotoSansJP
        ├─images
        │  ├─event-view
        │  ├─first-view
        │  │  ├─fifith-section
        │  │  ├─first-section
        │  │  ├─fourth-section
        │  │  ├─second-section
        │  │  └─third-section
        │  ├─footer
        │  ├─gallery-view
        │  ├─message-view
        │  └─others
        └─js
    ```

3. `WordPress`の管理画面（`http://localhost:8000/wp-admin`）にログインし、「外観」>「テーマ」からテーマを有効化します。

## プロジェクト構造

```bash
wordpress-dev-docker/
│
├── my-awesome-theme/       # WordPressテーマディレクトリ
│
├── plugins/                # WordPressプラグイン
│
├── uploads/                # アップロードされたメディアファイル
│
├── docker-compose.yml      # Dockerコンポーズ設定ファイル
├── dockerfile-wordpress    # WordPressのDockerfile
├── .env                    # 環境変数設定ファイル
└── README.md               # このファイル
```

## 使用方法

- **テーマの開発** `my-awesome-theme` フォルダ内のファイルを編集します。
- **プラグインの追加** `plugins/` フォルダにプラグインのZIPファイルを解凍するか、サブフォルダを作成します。
- **アップロードされたファイル** `uploads/` フォルダに自動的に保存されます。

## データベースへのアクセス

- **ホスト** `db`（外部アクセスの場合は `localhost`）
- **ポート** 3306
- **データベース名** `.env` ファイルの `DB_NAME` と同じ
- **ユーザー名** `.env` ファイルの `DB_USER` と同じ
- **パスワード** `.env` ファイルの `DB_PASSWORD` と同じ

## 注意事項

- アップロードの最大ファイルサイズは1GBです。
- PHPのメモリ制限は512MBです。
- 最大実行時間は300秒です。

## トラブルシューティング

問題が発生した場合

1. Docker Desktopを再起動します。
2. PowerShellで以下のコマンドを実行します：

   ```bash
   docker-compose down
   docker-compose up -d
   ```

3. Docker Desktopの「Containers」タブでログを確認します。
