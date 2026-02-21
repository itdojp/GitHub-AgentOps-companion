# CODEOWNERS 指針（参考）

## 目的

変更の承認責任を「ファイル/ディレクトリ単位」で明示し、レビューの抜け漏れと属人化を抑止します。

## 例（最小）

`CODEOWNERS` は `.github/` 配下に配置します。

```text
# 例: 運用ルール/テンプレは専任が承認
/.github/ISSUE_TEMPLATE/  @platform-team
/.github/PULL_REQUEST_TEMPLATE.md  @platform-team
/rules/  @security-team
/custom-agents/  @platform-team
/skills/  @platform-team
```

## 運用ルール（推奨）

- CODEOWNERS は「責任分界（人間/エージェント/CI）」の一部として扱う
- 例外（緊急対応など）は、承認ログを Issue/PR に残す
- チーム変更時は CODEOWNERS も更新対象に含める

