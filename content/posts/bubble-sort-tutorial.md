---
title: "バブルソート入門"
description: "Tutorial for bubble sort"
date: 2020-11-19T00:00:00+09:00
author: ["Kazuhiro Mimaki"]
draft: false
tags:
 - "Algorithm"
categories:
 - "Algorithm"
---

バブルソートについてのメモ。

## バブルソートとは
ソートアルゴリズムの1種。
リストにおいて、**隣り合う要素の大小比較**を繰り返すことで、全体を並べ替える。
昇順 or 降順に並び替える。

## イメージ
降順でソートする場合のイメージ。
![bubble-sort](/images/posts/bubblesort.jpg)

このように、隣接する要素の大小比較と入れ替えを繰り返すことで、徐々に最大値が右に寄っていく。
バブルソートは他の多くのアルゴリズムと比べ、処理時間が長くかかるのが弱点。

## 実装してみる