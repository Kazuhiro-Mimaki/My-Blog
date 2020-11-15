---
title: "【PATHを通す】を理解する"
description: "Understand the meaning of「PATHを通す」"
date: 2020-04-25
aliases: ["/posts/2020/pass-path/"]
---

「PATHを通す」ってよく聞くけど、意味がよく分からなかったので勉強しました。
<!--more-->
**PATHを通す**の意味がよくわからんので、色々調べました。

# そもそもPATHとは
PATHとは環境変数の1つ。環境変数とはPC環境についての変数で、すでに多くの環境変数が設定されている。Terminalで

```zsh
$ env
```
と入力すると、設定されているすべての環境変数が表示される。

```zsh
PWD=/Users/hogehoge
SHELL=/bin/zsh
PATH=/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin
COLORTERM=truecolor
HOME=/Users/hogehoge
USER=hogehoge
LOGNAME=hogehoge
ZSH=/Users/hogehoge/.oh-my-zsh
PAGER=less
LESS=-R
LC_CTYPE=en_US.UTF-8
LSCOLORS=Gxfxcxdxbxegedabagacad
_=/usr/bin/printenv
```

例えば`$HOME`という環境変数がホームディレクトリのパスになっていたり、`$USER`という環境変数にユーザ名が入ってるのがわかる。`＄PATH`という環境変数にもパスが入っているのが分かる。


# PATH変数
Terminal上でコマンドが実行されたらコンピュータはそのコマンドを探しに行く。でも、コンピュータの中にはたくさんのファイルやフォルダがあるので、コンピュータ内をすべて探していたら時間がかかる。PATH変数に登録されているPATHだけ探すことで手間を省いている。


実際に通っているPATHはechoコマンドで確認できる。

```zsh
$ echo $PATH
/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin
```

パスは`:`で区切られており、今回の例では下記のパスが設定されている。

```zsh
/usr/local/bin
/usr/bin
/bin
/usr/sbin
/sbin
/usr/local/sbin
```

# PATHを通す
PATHを通すというのはすなわちPATHという環境変数に新しいパスを追加するということ。新しいパスを追加したい場合は、`~/.bash_profile`などの設定ファイルに

```zsh
export PATH=$PATH：<追加したいPATH>
```
を追記すればいい。

# 環境変数を永続化する
PATH以外でも、環境変数を永続化する場合、やり方は同様。環境変数はshellからexitすると消えるので、環境変数を永続化するためにはshellファイルを利用する。Bashというshellなら`~/.bash_profile`や`~/.bashrc`、zshなら`~/.zshrc`がshellファイルに当たる。このファイルの中にexportで環境変数を追加する処理を加えれば、環境変数を永続化できる。すなわち、Terminalを再び立ち上げた後もその変数を利用できる。

