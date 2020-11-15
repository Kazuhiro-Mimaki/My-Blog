---
title: "静的サイトジェネレーターHugoで自作ブログ"
description: "Make blog by hugo"
date: 2020-11-15
author: "Kazuhiro Mimaki"
tags:
 - "Hugo"
categories:
 - "develop"
---

今回Hugoで自作ブログを作ってみました。
<!--more-->

## Hugoとは
Hugoとはスピードと柔軟性を兼ね備えたGo製の静的サイトジェネレーターです。
静的サイトジェネレーターやjamstackといった静的サイトベースの技術を最近よく目にするので、僕もその波に乗りました。(ミーハー)

クラウドサーバーを使えば、自分でサーバーを管理する手間も省けるし、DBも不要。
あと、当たり前かもだけど動的サイトと比べるとページ表示速度がとにかく速い。
このあたりがWordpressのようなCMSと比べた時のメリットかなと思います。

## Hugoでブログ作成をスタート
Hugoには素敵なテンプレートがたくさん用意されています。
ので、僕のように「完全オリジナルは面倒」という人も安心してください。
このブログも「」というテーマを拝借させていただいています。
[Hugoテーマ一覧](https://themes.gohugo.io/)

以下のコマンドを打つだけで最初のセットアップが完了します。
なんて便利なんだ、、、！
```zsh
$ hugo new site <ディレクトリ名>
$ cd <ディレクトリ名>
$ git init
$ git submodule add <GitHub上のテーマのurl> <テーマの名前>
```

あとは自分好みにレイアウトやデザインをカスタマイズしたり、記事を追加していけばいい感じになります。(適当)
各テーマのdocumentを見れば割とカスタマイズできるかと思います。

## Firebaseでホスティング
FirebaseかNetlifyが良さそうだなぁと思っていたのですが、表示速度は妥協したくなかったのでfirebaseにしました。
ドメインはgoogle domainで取得しました。(まじで一瞬だった)
- [徹底比較！Firebase vs Netlify (2018年版)](https://techblog.kayac.com/netlify-vs-firebase-2018)
- [【GithubPages VS Netlify VS Firebase】爆速で静的サイトのホスティングができるのはどれ？](https://usomitainikagayakumachi.tokyo/2018-05-29_github_pages_or_netrify_or_firebase/)

GitHub Actionsで自動ビルド&デプロイをしてくれるように設定しておけば、pushするだけで本番環境に差分が反映されるのでオススメです。

## まとめ
まだ未完成の部分もあるのでそこの調整は引き続きしていきます。
静的サイトジェネレーターめちゃくちゃ便利だなとしみじみ。
新しくブログを書き始めるならHugoにhello worldしてみてはどうでしょうか。