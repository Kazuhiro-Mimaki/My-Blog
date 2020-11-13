+++
title = "[Rails] いいね数順でランキング"
description = "Ranking by like counts using rails"
date = "2020-08-20"
aliases = ["/posts/2020/rails-ranking-by-like/"]
+++


今回はいいね数の多い順(いいね数が0も含む)に投稿を表示させるランキング機能の実装方法についてです。  
ランキング機能の実装方法は他でもあったのですが、いいねが0の投稿も表示させている記事が見当たらなかったので実装してみました。
<!--more-->

# 前提
- 投稿のテーブルは `posts`、 ユーザーのテーブルは `users` とする。
- いいね機能に必要な中間テーブルは `likes` とする。
- `posts`・`users`・`likes` それぞれのテーブルはいずれも作成済みとする。

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


## コントローラーをいじる

```posts_controller.rb
def index
  @posts = Post.all.sort {|a,b| b.liked_users.count <=> a.liked_users.count}
end
```

ここでは `sort` というrubyのメソッドを使って順序を操作している。
=> [sortに関してはこちらを参照](https://docs.ruby-lang.org/ja/latest/method/Array/i/sort.html)

`a.liked_users.count`、`b.liked_users.count` が表しているのはそれぞれ各投稿のいいね数。
すなわち、各投稿のいいね数を比較して昇順で並び替えている。



## ビューで表示させる
あとはビューで表示させるだけ。

```index.html.erb
<% @posts.each do |post| %>

  #省略

<% end %>
```
まだまだ知らないメソッドたちはたくさんあるなぁ。

# 参考
- [Array#sort (Ruby 2.7.0 リファレンスマニュアル)](https://docs.ruby-lang.org/ja/latest/method/Array/i/sort.html)
