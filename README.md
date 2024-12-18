# Git training

独習Gitの学習の記録。  

## git guiのインストール

基本的にはCUIで操作するので、GUIはほとんど使わない。
IDEを使わずにグラフィカルに確認したい場合のみ使う。

```bash
$ brew install git-gui
```

## CUIショートカット

```bash
# 文字を削除
ctrl + D

# 行を削除
ctrl + U

# 1文字を削除
ctrl + D

# 左の文字を削除
ctrl + H

# カーソルを先頭に移動
ctrl + A

# カーソルを末尾に移動
ctrl + E
```

<br/>

## gitコマンド一覧

```bash
# 管理されているファイルの一覧
$ git ls-files

# ファイルの詳細を確認
$ git blame README.md

# コミットログの確認
$ git log --oneline

# gitの設定を確認する
$ git config --list

# リポジトリの状態の確認
$ git status

```

<br/>


### git blame
コミットされたファイルの詳細を確認する。  
HEAD, 変更者, 変更日時、変更内容を確認できる。

<br/>

## GUIの活用

```bash
$ brew install git-gui
```

```bash
# git guiを開く
$ git gui
$ git citool

# コミットログ確認ウィンドウを開く
$ gitk
```

<br/>

**todo**  
GUIアプリケーションの作成については、`tcl/tk`を学ぶ

<br/>

## リポジトリの基本操作

### git init
.gitが作成される。

```bash
# Gitリポジトリの作成
$ git init
```

### git commit

変更を記録する。  
下記の`4ed1895`は、SHA1-IDで、コミットを一意に認識するID。  
mode`100644`は、ファイルのパーミッションを表す。


```bash
$ git commit -m 'update'
> [master 4ed1895] update
>  2 files changed, 747 insertions(+), 1 deletion(-)
>  create mode 100644 glossary.md
```

### git log

```bash
# logをファイル構成を含めて表示する
$ git log --stat
```

### git diff
ステージング前のファイルに対して、変更内容を確認する。

```bash
# ステージングされていないファイルの変更内容を確認する
$ git diff
```

```bash
# ステージングされたファイルの変更内容を確認する
$ git diff --staged
```



