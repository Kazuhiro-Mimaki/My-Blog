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
1~10のリストをバブルソートで並び替える場合。
```python
x = [4, 6, 1, 9, 7, 2, 3, 8, 10, 5]

for i in range(len(x)-1):
  # 各段階の中で、順番に比較を行う
  for j in range(0, len(x)-1-i):
    # 左の方が大きければ左右を入れ替える
    if x[j] > x[j+1]:
      x[j], x[j+1] = x[j+1], x[j]

print(x)

# 出力結果
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```