---
title: "Vitestで任意の.envファイルから環境変数を読み込む"
emoji: "😸"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [vitest, dotenv]
published: true
---

```ts:vitest.config.ts
import { defineConfig } from 'vitest/config';
import dotenv from 'dotenv';

export default defineConfig({
 test: {
   env: dotenv.config({ path: ".env.test" }).parsed,
 },
});
```
