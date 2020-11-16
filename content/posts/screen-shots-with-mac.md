---
title: "[mac]スクリーンショットを超快適にしよう"
description: "Screenshots easily with mac"
date: 2020-11-13T14:30:00+09:00
author: ["Kazuhiro Mimaki"]
categories:
 - "develop"
---

Macでスクリーンショットを利用する際のtipsをシェアします。

# スクリーンショットする際のショートカットキー

**Command + Shift + 3**
画面全体をキャプチャ。

**Command + Shit + 4**
マウスで選択した範囲のみキャプチャ。
マウスカーソルの形状が変わるのでキャプチャしたい範囲をドラッグで決める。
ESCでキャンセル。

# 保存せず、そのままクリップボードにコピーしたい場合

これ超便利！知らない人は人生半分損してる。。。
ドキュメント貼り付け作業が捗ります。

**Command + Shift + Control + 3**
画面全体

**Command + Shit + Control + 4**
マウス選択の範囲。

上記のショートカットキー＋Controlキーを押すだけ。

# 保存場所を変更
デフォルトではデスクトップに保存されますが、任意のディレクトリに移動できます。
デスクトップにスクショ溜まるのうざいので、これは良い！
コマンドラインから設定し、再起動すれば反映されます。

↓今回は ~/Downloads/ に設定していますが、別のディレクトリも指定可能。

```shell
$ defaults write com.apple.screencapture location ~/Downloads/　
↓デフォルトに戻す場合はこちら。設定値を削除するイメージです。
$ defaults delete com.apple.screencapture location
```

↓やっぱりデフォルトに戻したい場合。

```shell
$ defaults delete com.apple.screencapture location
```

# 保存形式を変更

デフォルトではpngで保存されます。
複数のファイル形式を指定できます。
用途に応じて保存時に形式変更できるので最高！
こちらもコマンドラインから設定し、再起動すれば反映されます。

↓今回はjpgで保存する場合のコマンド。

```shell
defaults write com.apple.screencapture type jpg;
```

# まとめ
これであなたのスクリーンショットライフは超快適になること間違いなしですね！

# 参考
- [macOSのスクリーンショット設定を変更する](https://qiita.com/tocomi/items/8c8e8f8202ea6da2c46d)
- [Macでスクリーンショットを撮る方法と保存先＆形式を変える方法](https://qiita.com/mamohacy/items/559af38aacb7a17a1600)
