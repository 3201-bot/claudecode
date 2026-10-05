# claudecode

Claude Code 用のプロジェクト設定・スキル置き場。

## 収録スキル

### ebay-listing-maker (`.claude/skills/ebay-listing-maker/`)
日本の中古品をeBayに輸出販売するための、リサーチ〜出品下書き〜在庫監視の自動化スキル。
このリポジトリを開いた Claude Code セッションでは、プロジェクトスキルとして自動で認識される。

ローカルの Claude Code 全体(他のプロジェクトでも)で使いたい場合は、個人スキルとして配置する:

```bash
unzip ebay-listing-maker-skill-*.zip -d /tmp/ebay-skill
mkdir -p ~/.claude/skills
cp -r /tmp/ebay-skill/ebay-listing-maker ~/.claude/skills/
```

配置後、`~/.claude/skills/ebay-listing-maker/SKILL.md` が存在していれば完了。
Claude Code を再起動し、「eBay出品のリサーチをして」などと頼むか `/ebay-listing-maker` で呼び出せる。
