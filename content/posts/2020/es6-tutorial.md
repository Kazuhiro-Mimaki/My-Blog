+++
title = "ES6(JavaScript)の基礎を押さえる"
description = "Foundation of ES6"
date = "2020-03-29"
aliases = ["/posts/2020/es6-tutorial/"]
author = "Hugo Authors"
+++

JavaScriptの新記法ES6の基礎を少し学んだので、そのアウトプットです。
<!--more-->
# ES6とは

ES6はJavaScriptの新しいバージョン。
現在は多くのブラウザが対応していないため、ES6で書いたコードを動かすためにはES5(1つ前のバージョン)への変換が必要になる。
この変更を"トランスパイル"と呼び、Babelというツールを利用してトランスパイルを行う。

# letとconst

letで変数を、constで定数を定義できる。
letは再代入が可能であるのに対し、constは再代入が不可能。

letでの変数宣言

```javascript:
let name = 'Jonh';
console.log(name); // => Jonh

name = 'Kate'; // 再代入する
console.log(name); // => Kate
```

constでの変数宣言

```javascript:
const name = 'Jonh';
console.log(name); // => Jonh

name = 'Kate'; // 再代入するとエラーになる
```

# テンプレートリテラル

バッククオートで文字列を囲むと、`${}`で文字列内に変数展開ができ、改行も反映できる。

```javascript:
const name = 'Jonh';
const age = 21;

console.log(`${name}は${age}歳です`); // => Jonhは21歳です
```

# アロー関数

関数とはいくつかの処理をまとめたもの。
アロー関数は関数の中でも無名関数の省略形で、従来より簡潔な記述で関数を定義できる。

通常の関数

```javascript:
const a = function(){
//まとめたい処理
};
```

上と同義のアロー関数

```javascript:
const a = () => {
//まとめたい処理
};
```

# Class構文

オブジェクトを生成する際、最初に設計図を用意する必要がある。
この設計図を"クラス"と呼ぶ。
「class クラス名」とすることでクラスを定義することができる。

```javascript:
class User = {
 constructor() {
  this.name = 'Jonh';
 }
} //クラスの定義

const user = new User(); //インスタンスを生成
console.log(user.name); // => Jonh
```
