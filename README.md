# Git training

独習Gitの学習の記録。  

## tips

### catコマンド

```bash
# 行番号を付けてファイルの内容を出力する
$ cat -n README.md
```

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

### git add
変更をステージングする。 

```bash
# 予行練習(結果の事前確認)
$ git add --dry-run .
$ git add -n .
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

```bash
# 変更全てをステージングしてコミットする
$ git commit -a -m 'update'
$ git commit --all -m 'update'
```

### git log

```bash
# logをファイル構成を含めて表示する
$ git log --stat

# logをワンラインで表示する
$ git log --oneline

# logの短い情報を付加して表示する
$ git log --shortstat
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

### git restore
ステージングしたファイルをステージングから取り戻す。

```bash
# eをステージングから取り戻す
$ git restore --staged e
```

<br/>


### レポジトリからの削除(git rm)

`git rm`を使うと、削除と同時に変更をステージングしてくれる。

```bash
$ git rm a
$ git status
On branch master
Your branch is up to date with 'origin/master'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        deleted:    a
```

これはOSのコマンド`rm`を使って、その後`git add`するのと等価。
```bash
$ rm a
$ git add a
$ git status
On branch master
Your branch is up to date with 'origin/master'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        deleted:    a
```

ステージングした後に`git commit`を行うことで、
リポジトリに変更が反映される。


```bash
$ git commit -m 'deleting a'
```

### ファイル名の変更(git mv)

同様に、ファイル名を変更する場合は、
gitのコマンド`git mv`か、osコマンド`mv` + `git add`を行う。

### 部分的にステージングする(git add -p)
変更箇所のうち、コミットしたくない箇所がある場合、
部分的にステージングすることができる。

```bash
$ git add -p
# この後eを選択する
```

vscodeでこの機能を使用する場合は、
コードエディタのdefaultを`vim`に設定する
```bash
$ git config -e
# 下記の行を追加する
[core]
    editor = vim
```

### ステージングエリアからの変更の削除(git reset)


ステージングエリアの変更を取り消す

```bash
$ git reset bb.sh
```

### 変更前のファイルを取り戻す(git checkout)
```bash
# 最後のコミットのファイルを取り戻す
$ git checkout -- sample.txt
```

ここで、`--`はオプション指定の終了を明示的に表す。
これがないと、`sample.txt`をコミットIDやブランチ名と誤解される可能性がある。




### コミットログの確認(git log)

```bash
$ git log --parents --oneline
57bfcf1 05fec74 (HEAD -> master, origin/master) update README
05fec74 5d85678 add f
5d85678 1202375 add bb and update README
1202375 2091f88 rename b to bb
2091f88 fbc0bb2 delete a
fbc0bb2 96da4a1 finished section6
96da4a1 d673f05 added new four files
d673f05 b3cf55f update readme
b3cf55f 14aac92 adding a text
14aac92 82b1418 新しいファイルの追加
82b1418 4ed1895 update
4ed1895 132b89c update
132b89c initial commit
```

現在のSHA1 ID 親のSHA1 IDの順に表示される。


```bash
# 変更の詳細も確認
$ git log --patch

# 変更箇所数も確認
$ git log --stat
```


### 特定のバージョンのファイルを取り戻す

```bash
$ git rev-parse HEAD
$ git rev-parse master
```
