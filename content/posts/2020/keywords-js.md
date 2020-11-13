+++
title = "聞いたことはあるがよくわからないJavaScript周辺のあれこれ"
description = "Keywords of JavaScript"
date = "2020-08-09"
aliases = ["/posts/2020/keywords-js/"]
author = "Hugo Authors"
+++

JSでよくお目にかかるキーワードをまとめてみました。
今後も追加していくと思います。
<!--more-->
JavaScriptを学習していると、よくわからない概念やライブラリに出会う機会が多いです。
その中でも特によく耳にするものをざっくりまとめてみました。(ホントにざっくり)
各内容をもっと掘り下げた参考記事も貼っているので気になる方はそちらも読んでみてください。

# ECMAScript
ECMAScriptとはJavaScriptの言語仕様の取り決め。
よく耳にする `ES2015` や `ES6` といった用語はJavaScriptのバージョンを表し、ここで出てくる `ES` がECMAScriptのこと。

[【JavaScript】JavaScript、その前に〜ECMAScriptとは？](https://qiita.com/yukibe/items/acd0bafcf2a10c99d0f6)

# npm
Node Package Manager、すなわちNode.jsのパッケージを管理するもの。
npmのおかげで、 `npm install 〇〇` と打つだけで便利なライブラリを簡単にインストールして利用することができる。

[npmとは](https://qiita.com/lelouch99v/items/05f973df9c54cec23419)

# yarn
2016年にFacebookが公開したかなり新しめのJavaScriptパッケージマネージャ。
役割はnpmとほぼ同じだが、npmと比べてインストール・セキュリティ・バージョン管理の面で優れている。

[yarnとは](https://qiita.com/lelouch99v/items/c97ff951ca31298f3f24)

# package.json
パッケージマネージャを用いてプロジェクトを作成する際に、プロジェクトが依存するパッケージに関する情報（さらにはプロジェクト全体に関する情報）を記録するファイルがpackage.json。
プロジェクトを動作させるために必要なパッケージをdependencies属性とdevDependencies属性に記述しておけば、`npm install` コマンドを打つだけでプロジェクト環境を復元できるため、非常に便利。

[【初心者向け】NPMとpackage.jsonを概念的に理解する](https://qiita.com/righteous/items/e5448cb2e7e11ab7d477)

# Babel
BabelはJavaScriptのコンパイラ。
これを使うとJavaScriptのコードを新しい書き方から古い書き方へと変換してくれる。
ブラウザによって対応しているJavaScriptのバージョンや仕様が異なるので、各ブラウザの環境に合わせて記法を変換する必要がある。

[【５分でなんとなく理解！】Babel入門](https://qiita.com/Shagamii/items/a87181c22ea777ee2acc)
[webpackとBabelの基本を理解する(1) ―Babel編―](https://qiita.com/koedamon/items/92c986456e4b9e845acd)

# webpack
webpackはモジュールバンドラ。
モジュールバンドラとは、複数のファイルを１つにまとめて出力してくれるツールのこと。
webpackはJSファイルだけでなく、CSSや画像ファイルも1つにまとめてくれる。
webpackを使えば、開発時には機能ごとにファイルを分割して開発を進めることができ、読み込み時には1つのファイルとして読み込めるので、非常に便利。

[webpackってどんなもの？](https://qiita.com/kamykn/items/45fb4690ace32216ca25)
[webpackとBabelの基本を理解する(1) ―webpack編―](https://qiita.com/koedamon/items/3e64612d22f3473f36a4)

# ESLint
ESLint は JavaScript のための静的検証ツール。
コードを実行する前に明らかなバグを見つけたり、括弧やスペースの使い方などのスタイルを統一したりするのに役立つ。

[ESLint 最初の一歩](https://qiita.com/mysticatea/items/f523dab04a25f617c87d)
