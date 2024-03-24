---
title: "Supabaseのデータをリアルタイムに取得できる便利なhooksを作った"
emoji: "🥷"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["nodejs", "supabase", "react", "reacthooks"]
published: false
---

Firebase のサンプルコードで、`onSnapshot`を活用してデータをリアルタイムに取得する方法をよく目にすると思います。

それの Supabase 版です。

コードだけ見れば十分という方は、ライブラリ化したので中身覗いてみてください！

TODO：GitHub のリンクを貼る。

## Supabase のデータ取得について

Google で調べると、シンプルにデータを取得するサンプルコードしか出てこない...

それを汎用的な関数に書き換えると、、、

```ts
import { createClientComponentClient } from "@supabase/auth-helpers-nextjs";

const supabase = createClientComponentClient();

export const getOneByCondition = async (table: string, filters: Filter[]) => {
  const query = supabase.from(table).select()
  queryBuilder(query, filters)

  const res = await query.single();
  return res;
}
export const = list = async (table: string, pg: PaginationParams) => {
  const { from = 0, to = from + 1, sort, filters = [] } = pg;

  const query = supabase.from(table).select("*", { count: "exact" });
  queryBuilder(query, filters);
  query.range(from, to);

  if (sort) {
    const { column, ...rest } = sort;
    query.order(column, { ...rest })
  }

  const res = await query;
  return res;
}
```
