---
title: "Claude Code環境でのみGit hooksを実行するlefthook設定"
emoji: "🪝"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [claudecode, lefthook, agenticcoding, git, githooks]
published: false
---


## はじめに

最近このポストを見てClaude Code環境で`CLAUDECODE=1`という環境変数があることを知りました。

https://x.com/r_masseater/status/1947860128944029745?s=46&t=zvUyvngihVg12ojk_zLm2A

そこでlefthookをClaude Codeでのコミット時のみ有効化できるようになったのでシェアします。

Anthropicの公式ガイド「[How Anthropic teams use Claude Code](https://www-cdn.anthropic.com/58284b19e702b49db9302d5b6f135ad8871e7658.pdf)」では、以下のように述べられています：

> Create self-sufficient loops Set up Claude to verify its own work by running builds, tests, and lints automatically. This allows Claude to work longer autonomously and catch its own mistakes, especially effective when you ask Claude to generate tests before writing code.

つまり、Claude Codeが自律的に動作するためには、ビルドやテスト、リントなどの自動検証が重要です。

一方で、人間が開発する場面では、WIPコミットや実験的なコードのコミット時にlintエラーで止まったり、急いでいる時に重いチェックが走ることが煩わしく感じられることもあります。

今回紹介する設定により、Claude Code環境でのみこれらの検証を実行し、AIには厳格な自己修正ループを提供しつつ、人間の開発時は柔軟性を保つことができます。

## 実装方法

Claude CodeのBash Mode内で`env`コマンドを実行すると、`CLAUDECODE=1`という環境変数が設定されていることが確認できます。

```bash
$ env | grep CLAUDE
CLAUDE_CODE_ENTRYPOINT=cli
CLAUDECODE=1
```

この環境変数を使って、lefthookの`skip`機能でClaude Code環境でのみhooksを実行するように設定できます。

## lefthook.yml設定例

以下の設定により、Claude Codeからのコミット時のみpre-commit hooksが実行されます。

コード例は[Biome.js公式ドキュメントにおけるlefthook統合](https://biomejs.dev/ja/recipes/git-hooks/#lefthook)のサンプルコードを改良したものです。

```yaml:lefthook.yml
pre-commit:
  skip:
    - run: test "$CLAUDECODE" != 1  # Claude Code以外はスキップ
  commands:
    check:
      glob: "*.{js,ts,cjs,mjs,d.cts,d.mts,jsx,tsx,json,jsonc}"
      run: npx @biomejs/biome check --no-errors-on-unmatched --files-ignore-unknown=true --colors=off {staged_files}
```

skip条件として`test "$CLAUDECODE" != 1`を使用しています。これにより、`CLAUDECODE`環境変数が設定されていない場合（つまり、Claude Code以外の環境）ではhooksがスキップされます。

https://lefthook.dev/configuration/skip.html?highlight=test#skip

## まとめ

`CLAUDECODE=1`環境変数を活用することで、Claude Codeでの開発時とマニュアル開発時で異なるGit hooksワークフローを簡単に構築できます。

AI駆動開発では自動修正を積極的に適用し、手動開発では軽量なチェックにとどめるなど、開発スタイルに合わせた最適化が可能になります。

---

**謝辞**: Claude Code環境変数の存在を教えてくださった[@r_masseater](https://x.com/r_masseater)さん、ありがとうございます！
