---
title: "[Rails] いいね数順でランキングかつページネーション"
description: "Ranking by like counts using rails with pagination"
date: 2020-11-11T14:30:00+09:00
author: ["Kazuhiro Mimaki"]
tags:
 - "Rails"
categories:
 - "develop"
---

以前このような記事を書きました。
[[Rails]いいね数順でランキング]({{< relref "/posts/rails-ranking-by-like.md#アンカー" >}})

この内容に加え、ページネーションを実装したのでメモとして残しておきます。
今回はいいね数順で並び替えた投稿を1ページに5つ表示させるページネーションの実装を目指します。

# 前提
- 投稿のテーブルは `posts`、 ユーザーのテーブルは `users` とする。
- いいね機能に必要な中間テーブルは `likes` とする。
- `posts`・`users`・`likes` それぞれのテーブルはいずれも作成済みとする。
- ページネーションは`Kaminari`というgemを使用して実装

# 手順

## モデルにアソシエーションを定義

```post.rb
class Post < ApplicationRecord
    belongs_to :user
    has_many :likes, dependent: :destroy
    has_many :liked_users, through: :likes, source: :user
end
```

```user.rb
class User < ApplicationRecord
  has_many :posts,dependent: :destroy
  has_many :likes, dependent: :destroy
  has_many :liked_posts, through: :likes, source: :post
end
```

```like.rb
class Like < ApplicationRecord
  belongs_to :post
  belongs_to :user
end
```

## Kaminari をGemfileに追記し, bundle install

```Gemfile
gem 'kaminari', '~> 0.17.0'
```

```zsh
$ bundle install
```

## コントローラーをいじる

```app/controller/posts_controller.rb
def index
  posts = Post.includes(:liked_users).sort {|a,b| b.liked_users.size <=> a.liked_users.size}
  @posts = Kaminari.paginate_array(posts).page(params[:page]).per(5)
end
```

ここでは `sort` というrubyのメソッドを使って順序を操作している。
=> [sortに関してはこちらを参照](https://docs.ruby-lang.org/ja/latest/method/Array/i/sort.html)

`a.liked_users.size`、`b.liked_users.size` が表しているのはそれぞれ各投稿のいいね数。
すなわち、各投稿のいいね数を比較して昇順で並び替えている。

`sort`メソッドによって生成される`posts`という変数は配列のデータなので、`paginate_array`というメソッドを使用している。



## ビューで表示させる
あとはビューで表示させるだけ。

```app/view/posts/index.html
<% @posts.each do |post| %>

  #省略

<% end %>
<%= paginate @posts %>
```
まだまだ知らないメソッドたちはたくさんあるなぁ。

# 参考
- [Array#sort (Ruby 2.7.0 リファレンスマニュアル)](https://docs.ruby-lang.org/ja/latest/method/Array/i/sort.html)
- [[rails]kaminariを使ってページネーションを作る](https://qiita.com/you8/items/df68aaee3010e282d1ae)
- [kaminariを使って配列に対してのページャーを作成する](https://blog.konboi.com/post/2013/03/31/224939/)
