---
title: "[Rails] webpackerでCSSを読み込みたい"
description: "Load CSS by webpacker"
date: 2020-08-24
aliases: ["/posts/2020/webpacker-css/"]
---

railsのver.6以上を使うなら `asset pipeline` ではなく `webpacker` でCSSを読み込みたいと思い、実装したのでメモです。
<!--more-->

## ディレクトリ構成
[webpacker](https://github.com/rails/webpacker) のREADME.mdより。

```
app/javascript:
  └── packs:
      # only webpack entry files here
      └── application.js
      └── application.css
```

# 手順
`rails new` は完了しているものとします。
rails6より下のversion使ってる人はwebpackerもインストールしましょう。

## 新規フォルダ・ファイル作成
↑のディレクトリ構成に従う。
app/javascript/packsに `application.css` ファイルを作成

## エントリーポイント
エントリーポイントは packs/application.js なので、application.cssファイルをimport。

```packs/application.js
import "packs/application.css";
```


## application.html.erbを編集
views/layouts/application.html.erb に以下を記述。
おそらくデフォルトだと `stylesheets_link_tag` になっているので、そこを `stylesheets_pack_tag` に変更すればいいかと。

```erb
<%= javascript_pack_tag 'application' %>
<%= stylesheet_pack_tag 'application' %>
```

## CSSを書く
あとはCSSを書くのみです。
次はReact、Vue.jsあたりも導入してみたい。

今回は手順だけをメモした感じなので、もう少し詳しく中身を知りたい人は↓が参考になると思われます。

# 参考
[Rails 6+Webpacker開発環境をJS強者ががっつりセットアップしてみた（翻訳）](https://techracho.bpsinc.jp/hachi8833/2019_11_28/83678)
[webpackerでcssとimagesを参照したい](https://qiita.com/msy-naka/items/dba5e880c501ca0d5d92)
[webpacker でページごとにスタイルを分ける](https://cloudpack.media/51718)
