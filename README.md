<p align="center">
  <a href="https://vibekanban.com">
    <picture>
      <source srcset="frontend/public/vibe-kanban-logo-dark.svg" media="(prefers-color-scheme: dark)">
      <source srcset="frontend/public/vibe-kanban-logo.svg" media="(prefers-color-scheme: light)">
      <img src="frontend/public/vibe-kanban-logo.svg" alt="Vibe Kanban Logo">
    </picture>
  </a>
</p>

<p align="center">Claude Code、Gemini CLI、Codex、Amp、その他のコーディングエージェントを10倍活用しましょう...</p>
<p align="center">
  <a href="https://www.npmjs.com/package/vibe-kanban"><img alt="npm" src="https://img.shields.io/npm/v/vibe-kanban?style=flat-square" /></a>
  <a href="https://github.com/BloopAI/vibe-kanban/blob/main/.github/workflows/publish.yml"><img alt="Build status" src="https://img.shields.io/github/actions/workflow/status/BloopAI/vibe-kanban/.github%2Fworkflows%2Fpublish.yml" /></a>
</p>

![](frontend/public/vibe-kanban-screenshot-overview.png)

## 概要

AIコーディングエージェントが世界のコードを書くことが増え、人間のエンジニアは今や、タスクの計画、レビュー、調整に多くの時間を費やしています。Vibe Kanbanはこのプロセスを合理化し、以下のことを可能にします：

-   さまざまなコーディングエージェントを簡単に切り替える
-   複数のコーディングエージェントの実行を並行または直列で調整する
-   作業を迅速にレビューし、開発サーバーを起動する
-   コーディングエージェントが取り組んでいるタスクのステータスを追跡する
-   コーディングエージェントのMCP設定を一元管理する

[こちら](https://youtu.be/TFT3KnZOOAk)でビデオ概要をご覧いただけます。

## インストール

お気に入りのコーディングエージェントで認証していることを確認してください。サポートされているコーディングエージェントの完全なリストは[ドキュメント](https://vibekanban.com/)にあります。その後、ターミナルで以下を実行します：

```bash
npx vibe-kanban
```

## ドキュメント

最新のドキュメントとユーザーガイドについては、[ウェブサイト](https://vibekanban.com)をご覧ください。

## サポート

バグを見つけたり、機能リクエストがある場合は、このリポジトリでissueを開いてください。

## コントリビューション

アイデアや変更は、まずGitHubのissueを通じてコアチームに提案していただくことを推奨します。そこで、実装の詳細や既存のロードマップとの整合性について議論できます。チームと最初に提案を議論することなくPRを開かないでください。

## 開発

### 前提条件

-   [Rust](https://rustup.rs/) (最新の安定版)
-   [Node.js](https://nodejs.org/) (>=18)
-   [pnpm](https://pnpm.io/) (>=8)

追加の開発ツール：
```bash
cargo install cargo-watch
cargo install sqlx-cli
```

依存関係のインストール：
```bash
pnpm i
```

### 開発サーバーの実行

```bash
pnpm run dev
```

これにより、フロントエンドとバックエンドがライブリロードで起動します。空のDBが`dev_assets_seed`フォルダからコピーされます。

### ソースからのビルド

1.  `build-npm-package.sh`を実行します
2.  `npx-cli`フォルダで`npm pack`を実行します
3.  `npx [生成されたファイル].tgz`でビルドを実行できます

### 環境変数

以下の環境変数は、ビルド時または実行時に設定できます：

| 変数 | タイプ | デフォルト | 説明 |
|----------|------|---------|-------------|
| `GITHUB_CLIENT_ID` | ビルド時 | `Ov23li9bxz3kKfPOIsGm` | 認証用のGitHub OAuthアプリのクライアントID |
| `POSTHOG_API_KEY` | ビルド時 | 空 | PostHog分析APIキー（空の場合は分析を無効化） |
| `POSTHOG_API_ENDPOINT` | ビルド時 | 空 | PostHog分析エンドポイント（空の場合は分析を無効化） |
| `BACKEND_PORT` | 実行時 | `0` (自動割り当て) | バックエンドサーバーのポート |
| `FRONTEND_PORT` | 実行時 | `3000` | フロントエンド開発サーバーのポート |
| `HOST` | 実行時 | `127.0.0.1` | バックエンドサーバーのホスト |
| `DISABLE_WORKTREE_ORPHAN_CLEANUP` | 実行時 | 未設定 | git worktreeのクリーンアップを無効にする（デバッグ用） |

**ビルド時変数**は`pnpm run build`の実行時に設定する必要があります。**実行時変数**はアプリケーションの起動時に読み込まれます。

#### カスタムGitHub OAuthアプリ（オプション）

デフォルトでは、Vibe KanbanはBloop AIのGitHub OAuthアプリを認証に使用します。セルフホスティングやカスタムブランディングのために独自のGitHubアプリを使用するには：

1.  [GitHub Developer Settings](https://github.com/settings/developers)でGitHub OAuthアプリを作成します
2.  アプリの設定で「Device Flow」を有効にします
3.  スコープを`user:email,repo`に設定します
4.  クライアントIDを使用してビルドします：
   ```bash
   GITHUB_CLIENT_ID=your_client_id_here pnpm run build
   ```
