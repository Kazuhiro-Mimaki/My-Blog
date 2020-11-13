+++
title = "Web APIの概念を押さえる"
description = "What is web API"
date = "2020-04-11"
aliases = ["/posts/2020/what-is-web-api/"]
author = "Hugo Authors"
+++

Web API is 何？
<!--more-->
# APIとは
Web APIの前に、そもそもAPIとはApplication Program Interfaceの略。どのアプリーケーションでも共通で使える機能を提供する仕組み。

> 例えば「AというファイルをBという名前でコピーをして、作業完了したら、ポップアップウィンドウを出して知らせる！」というプログラムを作るとします。実際にどんな動きをするのかパートに分けてみると……、

> 1. Aというファイルを選択
> 2. 実行ボタンを押すと3のステップへ
> 3. データをコピーする
> 4. コピーされたデータをBという名前を付け保存
> 5. ポップアップウィンドウを出して作業完了を告げる


>この1.〜5.の作業をすべて一から作成すると、かなり手間が掛かります（マウスの動きを計算して、ウィンドウのデザインを考えて……）。そこで登場するのがAPIです。

> 1. ファイルを選択するAPI
> 2. ボタンを押すとプログラムを動かすAPI
> 3. データをコピーするAPI
> 4. ファイルに名前を付けるAPI
> 5. ウィンドウを出してメッセージを出すAPI


> と、いろいろな機能があるAPIから、必要なAPIを探し出し組み合わせるだけで、プログラムができてしまうのです。つまりAPIは「特定の機能を持つプログラム部品」なのです。よく使われる命令をAPIにしてみんなで共有してしまえば、非常に効率的に作業ができますね。

> API
![alt](https://image.itmedia.co.jp/ait/articles/0703/13/r85minapi_01.gif)
図1 APIを使えば、細かい作業や無駄を省いてプログラムができる

> by https://www.atmarkit.co.jp/ait/articles/0703/13/news095.html

# Web APIとは

Web APIはWebサービスの窓口。外部Webサービスから通信を通して、操作することができる。自分で作成することも可能。

具体例 １：【マッチングアプリ】  
Facebook APIから情報を取得。Facebook API経由でFacebookの友達のデータを取ってきて、そのデータを元にその人とは会わないようにアプリ側が人をマッチングさせてくれる。

具体例 ２：【食べログ】  
Google Maps APIから情報を取得。「ウェブサイトに地図を埋め込む」、「レストランや店舗のデータベースを、地図情報とともに提供する」、「目的までの最適なルートを探し出す」、といった機能を実現している。

具体例 ３  
PythonでTwiiter APIからツイートを取得しフォロワーの全ての人のデータを取ってくることもできる。


# Web APIに対応している主なサービス

- Twitter
- Instagram
- Youtube
- Google map
- Slack
- Chatwork
- 仮想通貨

# APIを実装してみる

- [Web APIとは？ （LINE bot API・グルナビAPI）](https://qiita.com/Masato338/items/6fb1ac277c965905e019)
- [Ruby on Rails: twitterでユーザー認証](https://qiita.com/keiya01/items/c96a0393c76f5560ee41)
- [ドットインストール/Google Maps API入門 (全17回)](https://dotinstall.com/lessons/basic_google_maps_v2)

# 参考資料
- https://qiita.com/busyoumono99/items/9b5ffd35dd521bafce47
- https://qiita.com/Arata0608/items/f292dedffc8c0db1df28
- https://www.atmarkit.co.jp/ait/articles/0703/13/news095.html
