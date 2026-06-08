# Article Production Template

Codex cloudでSEO記事を作成し、HTML確認後にWordPressへ下書き投稿するためのテンプレートです。

## 基本フロー

1. `briefs/` に記事ごとの指示書を作成
2. Codex cloudに記事作成を依頼
3. `drafts/` にMarkdown記事を生成
4. `public/` にHTML確認版を生成
5. HTML確認後、WordPressへ下書き投稿

## よく使うコマンド

```bash
npm install
npm run html -- drafts/sample-article.md public/sample-article.html
npm run validate -- drafts/sample-article.md
npm run wp:draft -- public/yyc-sefure.html
```

## GitHub Actionsから下書き投稿する

GitHubのリポジトリ画面で `Settings` → `Secrets and variables` → `Actions` を開き、Repository secrets に次の3つを登録します。

```text
WP_BASE_URL
WP_USERNAME
WP_APP_PASSWORD
```

`WP_BASE_URL` は `https://www.atarijo.com/media` を指定します。`WP_APP_PASSWORD` はコードやREADMEには書かず、Secretsにだけ保存してください。

登録後、`Actions` → `Publish WordPress Draft` → `Run workflow` を開き、`article_path` に `public/yyc-sefure.html` を指定して実行します。投稿スクリプトはWordPressの投稿ステータスを必ず `draft` にして作成します。

## 注意

- WordPress投稿は必ず `draft` 状態で行います。
- 投稿先は `https://www.atarijo.com/media` 配下のWordPressだけに制限しています。
- 認証情報は `.env` またはGitHub Actions Secretsに保存し、GitHubへコミットしないでください。
- `.env.example` をコピーして `.env` を作成してください。
