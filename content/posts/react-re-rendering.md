---
title: "【React】再レンダリングの仕組みと最適化"
date: 2021-03-16
author: "Kazuhiro Mimaki"
tags:
 - "react"
---

Reactのレンダリングについてまとめてみました。

# Reactが再レンダリングするタイミング
基本的にReactで再レンダリングが起きるタイミングは以下の3つ。
1. stateが更新された時
2. propsが更新された時
3. 親コンポーネントが再レンダリングされた時

## 1. stateが更新された時
```js:src/App.jsx
import { useState } from "react";

export default function App() {
  console.log("App");
  const [text, setText] = useState("");

  const changeText = (e) => {
    setText(e.target.value);
  };

  return (
    <>
      <p>App component</p>
      <input type="text" onChange={changeText} />
    </>
  );
}
```
上記のコードで空欄に文字を入力・削除してみると、処理回数に応じてconsoleに `App` が繰り返される。
すなわち、stateが変更されることで再レンダリングが発生している。

## 2. propsが更新された時
```js:src/App.jsx
import { useState } from "react";
import Child from "./components/Child";

export default function App() {
  const [count, setCount] = useState(0);

  const countUp = () => {
    setCount(count + 1);
  };

  return (
    <>
      <p>App component</p>
      <button onClick={countUp}>count up</button>
      <Child count={count} />
    </>
  );
}
```

```js:src/components/Child.jsx
const Child = (props) => {
  const { count } = props;
  console.log("Child");

  return (
    <>
      <p>Child component</p>
      {count}
    </>
  );
};

export default Child;
```
親である`App`コンポーネントから子である`Child`コンポーネントへ`count`というpropsを渡している。
ブラウザで実行して`count up`ボタンを押すと数字が1ずつ増えていき、consoleには`Child`が回数分表示される。
すなわち、propsが変更されることで再レンダリングが発生している。

## 3. 親コンポーネントが再レンダリングされた時
これは「親コンポーネントで再レンダリングが発生すると、その配下にある子コンポーネントが全て再レンダリングされてしまう」というもの。

```js:src/App.jsx
import { useState } from "react";
import Child from "./components/Child";

export default function App() {
  console.log("App");
  const [text, setText] = useState("");

  const changeText = (e) => {
    setText(e.target.value);
  };

  return (
    <>
      <p>App component</p>
      <input type="text" onChange={changeText} />
      <br />
      <Child />
    </>
  );
}
```

```js:src/components/Child.jsx
const Child = () => {
  console.log("Child");

  return (
    <>
      <p>Child component</p>
    </>
  );
};

export default Child;
```
上記のコードでは親子間でのpropsの受け渡しはないが、ブラウザ上で空欄に文字を入力・削除すると(親である`App`コンポーネントに記述されている`input`要素に値を入力すると)、consoleに`App`と`Child`が繰り返し表示されることが確認できる。
すなわち、親コンポーネントが再レンダリングされているタイミングで子コンポーネントも再レンダリングされている。
親子間で値の受け渡しが無いのにも関わらず、意図せずこのような再レンダリングが発生してしまうことで、パフォーマンスが下がってしまう。

# 再レンダリングを最適化する
再レンダリングを最適化する、すなわち無駄な計算や処理を抑えるために必要なReactの機能が以下の3つ。
1. memo
2. useCallback
3. useMemo

これらの機能を用いることで、メモ化(計算結果を保持し、それを再利用すること)ができる。
同じ結果を返す処理に関しては初回のみ処理を実行しておき、2回目以降は前回の処理結果を呼び出すことで毎回同じ処理を実行しなくてよくなる。

## 1. memo
以下のコードをブラウザで実行し、空欄に文字を入力・削除すると(親である`App`コンポーネントに記述されている`input`要素に値を入力すると)、consoleには`App`のみが繰り返し表示される。(メモ化していない先ほどのコードでは`App`と`Child`が交互に繰り返されていた)
Childコンポーネントはメモ化されているので、`Child`はconsoleに表示されない。

```js:src/App.jsx
import { useState } from "react";
import Child from "./components/Child";

export default function App() {
  console.log("App");
  const [text, setText] = useState("");

  const changeText = (e) => {
    setText(e.target.value);
  };

  return (
    <>
      <p>App component</p>
      <input type="text" onChange={changeText} />
      <br />
      <Child />
    </>
  );
}
```

```js:src/components/Child.jsx
import { memo } from "react";

const Child = memo(() => {
  console.log("Child");

  return (
    <>
      <p>Child component</p>
    </>
  );
});

export default Child;
```

## 2. useCallback
`useCallback`はメモ化したコールバック関数を返すHooks API。
次に、以下のようなコードを実行してみる。

```js:src/App.jsx
import { useState } from "react";
import Child from "./components/Child";

export default function App() {
  console.log("App");
  const [text, setText] = useState("");

  const changeText = (e) => {
    setText(e.target.value);
  };

  return (
    <>
      <p>App component</p>
      <br />
      <Child changeText={changeText} />
    </>
  );
}
```

```js:src/components/Child.jsx
import { memo } from "react";

const Child = memo((props) => {
  console.log("Child");
  const { changeText } = props;

  return (
    <>
      <input type="text" onChange={changeText} />
      <p>Child component</p>
    </>
  );
});

export default Child;
```
先ほど親コンポーネント(App)で処理していたinput要素を子コンポーネント(Child)に移動させ、関数`changeText`もpropsで受け渡している。
以下のコードをブラウザで実行し、空欄に文字を入力・削除すると(親である`App`コンポーネントに記述されている`input`要素に値を入力すると)、再びconsoleに`App`と`Child`が繰り返し表示される。
「`Child`コンポーネントをメモ化しているのになぜ？」

この原因はpropsで受け渡した関数にある。
親コンポーネントで生成した関数をpropsで子コンポーネントに渡すと、関数の内容が同じでも子コンポーネントでは「毎回新しい関数が渡されている」と判断されてしまう。
そこで`useCallback`を使う。

```js:src/App.jsx
import { useState, useCallback } from "react";
import Child from "./components/Child";

export default function App() {
  console.log("App");
  const [text, setText] = useState("");

  const changeText = useCallback(
    (e) => {
      setText(e.target.value);
    },
    [setText]
  );

  return (
    <>
      <p>App component</p>
      <br />
      <Child changeText={changeText} />
    </>
  );
}
```
以上のように関数(changeText)を`useCallback`で囲み、第2引数には配列を設定できる。(`useEffect`と同様)
このコードをブラウザで実行し、空欄に文字を入力・削除すると(親である`App`コンポーネントに記述されている`input`要素に値を入力すると)、consoleには`App`のみが繰り返し表示される。

## 3. useMemo
`useMemo`は変数のメモ化ができるHooks API。

```js:src/App.jsx
import { useState } from "react";

export default function App() {
  console.log("App");
  const [text, setText] = useState("");

  const changeText = (e) => {
    setText(e.target.value);
  };

  const todayDate = () => {
    console.log("Date");
    const dateObj = new Date();
    const dateString = `${dateObj.getFullYear()}年${
      dateObj.getMonth() + 1
    }月${dateObj.getDate()}日`; // YYYY年MM月DD日
    return <p>日付：{dateString}</p>;
  };

  return (
    <>
      <p>App component</p>
      <input type="text" onChange={changeText} />
      <br />
      {todayDate()}
    </>
  );
}
```
以上のコードをブラウザで実行し、空欄に文字を入力・削除すると(親である`App`コンポーネントに記述されている`input`要素に値を入力すると)、consoleに`App`と`Date`が交互に繰り返し表示される。


```js:src/App.jsx
import { useState, useMemo } from "react";

export default function App() {
  console.log("App");
  const [text, setText] = useState("");

  const changeText = (e) => {
    setText(e.target.value);
  };

  const todayDate = useMemo(() => {
    console.log("Date");
    const dateObj = new Date();
    const dateString = `${dateObj.getFullYear()}年${
      dateObj.getMonth() + 1
    }月${dateObj.getDate()}日`; // YYYY年MM月DD日
    return <p>日付：{dateString}</p>;
  }, []);

  return (
    <>
      <p>App component</p>
      <input type="text" onChange={changeText} />
      <br />
      {todayDate}
    </>
  );
}
```
以上のように変数を返す関数(todayDate)を`useMemo`で囲み、第2引数には配列を設定できる。(`useEffect`と同様)
このコードをブラウザで実行し、空欄に文字を入力・削除すると(親である`App`コンポーネントに記述されている`input`要素に値を入力すると)、consoleには`App`のみが繰り返し表示される。


# 参考
- https://zenn.dev/tsukunin/articles/4b41bce046ba74011cf4
- https://times.hrbrain.co.jp/entry/react-hooks-performance