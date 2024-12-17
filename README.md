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

```

### git blame
コミットされたファイルの詳細を確認する。  
HEAD, 変更者, 変更日時、変更内容を確認できる。


## リポジトリの基本操作

```bash
# Gitリポジトリの作成
$ git init
```

