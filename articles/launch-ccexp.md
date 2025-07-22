---
title: "散らばったClaude Codeの設定ファイルを一元管理するCLIツール ccexp を作った"
emoji: "🔎"
type: "idea" # tech: 技術記事 / idea: アイデア
topics: [claudecode, claude, tool, oss]
published: false
---

## 実行方法

```bash
npx ccexp@latest
```

もしくは

```bash
bunx ccexp@latest
```

上記のコマンドで使うことができます。

## はじめに

みなさん、Claude Code を使っていますか？

私は個人開発で、Claude Code を主体とした Agentic Coding を日々行っています。

ただ、複数のプロジェクトを同時に進めていると、こんな経験はありませんか？「Next.js ではこの CLAUDE.md を、CLI ツールではあっちの CLAUDE.md を...」といった具合に、丹精込めて育てた CLAUDE.md やカスタムコマンドが、あちこちに散らばってしまうことに悩んでいました。

**ccexp（claude-code-explorer）** は、そんな悩みを解消するために作りました。

## ccexp の機能

### 1. TUI ベース

ccexp は Claude Code と同じく、ターミナルで動く UI として作られています。`npx ccexp@latest`を実行すると、左側にファイルリスト、右側にプレビューという2ペイン構成の画面が表示されます。

![ccexp のファイルリスト画面 - プロジェクトの CLAUDE.md ファイルやグローバル設定を一覧表示](https://api.izanami.dev/storage/v1/object/public/pictures/eyecatch/ac12d936-8830-4e4c-bd98-fbb0f97fad7e/5c70608d-178c-48f2-a5f9-398213b305e5.png)

*ccexp のメイン画面。左側にファイルリスト、右側にプレビューが表示される*

プロジェクト内の CLAUDE.md だけでなく、グローバル設定（~/.claude/CLAUDE.md）やスラッシュコマンド定義ファイル（.claude/commands/）まで、Claude Code 関連のすべての設定ファイルを一つの画面で確認できます。

### 2. シンプルな操作

一般的な TUI における操作パターンに準拠しています。矢印キーでファイルを選択し、Enter でアクションメニューを開きます。また、キーワード検索も可能で、プロジェクト名やコマンド名による絞り込みが簡単に行えます。

### 3. 豊富なアクション

ファイルを選んで Enter を押すと、アクションメニューが表示されます。例えば、こんな操作ができます：

![ccexp のアクションメニュー - ファイル操作のオプション一覧](https://api.izanami.dev/storage/v1/object/public/pictures/eyecatch/ac12d936-8830-4e4c-bd98-fbb0f97fad7e/77477f4f-864f-4492-952d-9338e96f9aef.png)

*選択したファイルに対して実行できるアクションメニュー*

- ファイル内容をクリップボードにコピー
- 絶対パスをコピー
- 相対パスをコピー
- ファイルを現在のディレクトリにコピー
- エディタで編集（VSCode や Cursor, Zed などの$EDITOR に設定されているもの）
- デフォルトアプリケーションで開く

これらのアクションで、設定ファイルの確認から共有、編集まで、すべての作業をスムーズに進められます。

## まとめ

Claude Code を使っていれば、設定ファイルの管理は避けて通れません。もし同じ悩みを感じている方がいれば `npx ccexp@latest`を一度お試しください！

今後は設定ファイル(settings.json)のサポートも予定しており、Claude Code 関連の設定を一元管理できるツールとして改善を重ねていきます。

もしよろしければ、[GitHub リポジトリ](https://github.com/nyatinte/ccexp)に star をいただけると励みになります！

閲覧ありがとうございました！

## 謝辞

[awesome-claude-code](https://github.com/hesreallyhim/awesome-claude-code)にも掲載いただきました！ありがとうございます！

## リンク集

- [GitHub リポジトリ](https://github.com/nyatinte/ccexp)
- [npm](https://www.npmjs.com/package/ccexp)
- [X](https://x.com/nyatinte/status/1942569219117498577)
