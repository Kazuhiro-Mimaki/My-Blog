---
title: "[Rails] link_toのリンク先を別タブで表示させたい"
description: "Open the page on another tab by using rails"
date: 2020-07-11
aliases: ["/posts/ails-link_to/"]
---

railsのlink_toでの遷移先を別タブで表示させたい。
<!--more-->
Railsでlink_toを使うときに別タブで表示させたいと思い、実装したのでメモとして残しておきます。

# 手順

まず `link_to` で表示させたい文字列とリンク先URLを指定。

```rhtml
<%= link_to "文字列", "リンク先URL" %>
```

別タブで表示させるため、`target: :_blank` を追加

```rhtml
<%= link_to "文字列", "リンク先URL", target: :_blank %>
```

これで別タブで開けるようになる。
しかし、これだとパフォーマンスとセキュリティの面で問題が。。。

- [グーグルのエンジニアが警告、「別タブで開く」リンクは実はヤバいんだって！？【SEO情報まとめ】](https://webtan.impress.co.jp/e/2020/03/13/35510)
- [実はヤバい？危険な「別タブで開く（target=”_blank”）」](https://wwg.co.jp/blog/3807)

この問題を回避するためには `rel="noopener noreferrer"` をつけるといいみたい。

```rhtml
<%= link_to "文字列", "リンク先URL", target: :_blank, rel: "noopener noreferrer" %>
```

これで安心して別タブを開けます。
