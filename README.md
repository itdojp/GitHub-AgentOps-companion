# GitHub AgentOps Companion（for Book3）

本リポジトリは、書籍「GitHub AgentOps 実践ガイド」の Companion Repository です。
書籍側が「理解（背景/判断基準）」、本リポジトリが「導入（コピペ資産）」を担います。

本書は、例として Codex / GitHub Agents / Copilot coding agent を扱います（主要例は Codex）。

## オンライン版（Book）

- GitHub Pages: https://itdojp.github.io/GitHub-AgentOps-book/
- Book repo: https://github.com/itdojp/GitHub-AgentOps-book

## 収録内容（初期）

- `.github/ISSUE_TEMPLATE/`: Issue フォーム（実行仕様のテンプレ）
- `.github/PULL_REQUEST_TEMPLATE.md`: PR テンプレ
- `.github/codex/prompts/`: Codex Action 用プロンプト雛形
- `skills/`: `SKILL.md` 雛形（反復タスク手順資産）
- `custom-agents/`: `.agent.md` 雛形（役割特化エージェント）
- `rules/`: allow / prompt / forbidden のポリシー雛形
- `.github/workflows/`: サンプルワークフロー（Codex Action）

## 使い方（想定）

1. 自組織リポジトリに必要なファイルをコピーして適用する
2. 書籍本文の手順に沿って、運用ルールと品質ゲートを確立する
3. 四半期棚卸しでテンプレ/サンプルの整合性を維持する

## Codex GitHub Action サンプル

本リポジトリには、`openai/codex-action@v1` を用いた最小サンプルを含みます。

### 収録ワークフロー

- PR 作成/更新時の要約 + リスク抽出コメント: `.github/workflows/codex-pr-review.yml`
- リリース前の変更点サマリ/影響範囲/チェックリスト生成（手動実行）: `.github/workflows/codex-release-prep.yml`

### 導入手順（最小）

1. `.github/workflows/` と `.github/codex/prompts/` を自組織リポジトリへコピー
2. GitHub の Repository Secrets に `OPENAI_API_KEY` を追加
3. GitHub Actions を有効化し、必要に応じて org ポリシー（Actions 制限/監査）を適用

### Secrets/権限/実行範囲（注意）

- **Secrets**: `OPENAI_API_KEY` は OpenAI API を呼び出します（課金/監査/ローテーションを前提に運用）。
- **最小権限**: PR コメント投稿のため `issues: write` を付与しています。組織ポリシーにより追加調整が必要な場合があります。
- **フォーク PR**: `pull_request` トリガではフォーク PR に Secrets が渡らないため、サンプルは実質的に「同一リポジトリ内のブランチ PR」向けです。
- **プロンプトインジェクション**: PR 本文やコード内の指示を信頼しない前提でプロンプトを作っています。`pull_request_target` への安易な置換は推奨しません。
- **実行コスト**: `effort` を調整し、必要なら `paths` / ラベル条件 / 手動実行（`workflow_dispatch`）へ寄せて運用してください。

### 参照（一次情報）

- OpenAI Codex GitHub Action: https://platform.openai.com/docs/codex/automation/github-action
- Action リポジトリ: https://github.com/openai/codex-action

## ライセンス

現状は暫定として MIT を適用します（書籍本文のライセンスは別途）。
