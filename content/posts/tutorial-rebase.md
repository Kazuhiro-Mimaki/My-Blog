---
title: "rebase完全に理解した"
description: "Tutorial for git rebase"
date: 2020-10-25T14:30:00+09:00
author: ["Kazuhiro Mimaki"]
categories:
 - "develop"
---

最近実務で初めてrebaseを使って「？？？？」となったので調べました。

以下の動画、記事が分かりやすかったです。
- [Git MERGE vs REBASE](https://www.youtube.com/watch?v=CRlGDDprdOQ)
- [マージとリベース](https://www.atlassian.com/ja/git/tutorials/merging-vs-rebasing)

## 具体例
今回は動画から引用してこのような場合を考えてみます。

1. m2まで作業が進んでいるmasterブランチからfeatureブランチへcheckout
2. featureブランチでf1をコミット
3. masterブランチにcheckoutしてm3をコミット
4. 再度featureブランチにcheckoutしてf2をコミット
![スクリーンショット 2020-10-25 10.58.28.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/575694/adb79854-97ec-a83f-0ac8-0f61e8c9719a.png)

## ここまでの各ブランチのlog

#### masterブランチのlog

```shell
m3
m2
m1
```

#### featureブランチのlog

```shell
f2
f1
m2
m1
```

## merge vs rebase
ここからfeatureブランチにて、masterブランチを`merge`, `rebase`するとそれぞれどうなるか見ていきます。

`git merge master`のlog

```shell
f2
m3
f1
m2
m1
```

`git rebase master`のlog

```shell
f2
f1
m3
m2
m1
```

`merge`では時系列に沿ってそのまま差分を統合しているのに対し、`rebase`ではfeatureブランチの先端がmasterで置き換えられています。
`rebase`を用いるとコミット履歴がすっきりしますね。

## rebaseのアンチパターン

[この記事](https://www.atlassian.com/ja/git/tutorials/merging-vs-rebasing)から引用します。

> リベースの特徴を理解できたら、次に最も重要なことは、実行してはいけないときを知ることです。git rebase の黄金律は、リベースを public ブランチでは決して使用しないことです。

masterブランチにて、自分の作業ブランチをrebaseしてしまうとmasterのコミット履歴が書き換えられてしまいます。
このように、他の人にも共有済みのブランチで`rebase`は使わないように注意しましょう。
