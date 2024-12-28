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

```bash
$ git log --graph --decorate --pretty=oneline --all --abbrev-commit
* 711506c (HEAD -> master) update
* cc4cd9a update
* 6833726 update README
* 57bfcf1 (origin/master) update README
* 05fec74 add f
* 5d85678 add bb and update README
* 1202375 rename b to bb
* 2091f88 delete a
* fbc0bb2 finished section6
* 96da4a1 added new four files
* d673f05 update readme
* b3cf55f adding a text
* 14aac92 新しいファイルの追加
* 82b1418 update
* 4ed1895 update
* 132b89c initial commit
```


### 特定のバージョンのファイルを取り戻す

```bash
$ git rev-parse HEAD
$ git rev-parse master
```

```bash
# 特定のバージョンに戻す(HEADが96daになる)
$ git checkout 96da
```

```bash
# 最新のバージョンに戻す
$ git checkout master
```


### コミットにタグをつける
```bash
$ git tag anchor 6833726
```

```bash
# タグが表示される
$ git log --oneline
6833726 (HEAD -> master, tag: anchor) update README
57bfcf1 (origin/master) update README
05fec74 add f
5d85678 add bb and update README
1202375 rename b to bb
2091f88 delete a
...
```

```bash
# タグを使ってcheckout
$ git checkout anchor
```

```bash
# タグを削除する
$ git tag -d anchor
```

### ブランチの運用

```bash
# コミットの経路をグラフで表示する
$ git log --graph --decorate --pretty=oneline --all --abbrev-commit
```

```bash
# 開始地点を指定してブランチを作成
$ git checkout -b new_branch starting_at
```

`starting_at`には、コミットのSHA1 ID, タグ、ブランチ名を指定できる


```bash
# ブランチ切り替えのログを確認する
$ git reflog
290ee84 (HEAD -> master, dev) HEAD@{0}: checkout: moving from dev to master
290ee84 (HEAD -> master, dev) HEAD@{1}: checkout: moving from dev to dev
290ee84 (HEAD -> master, dev) HEAD@{2}: checkout: moving from master to dev
290ee84 (HEAD -> master, dev) HEAD@{3}: merge dev: Fast-forward
711506c HEAD@{4}: checkout: moving from dev to master
290ee84 (HEAD -> master, dev) HEAD@{5}: commit: update readme
efe2b2b HEAD@{6}: commit: new branch
711506c HEAD@{7}: checkout: moving from master to dev
711506c HEAD@{8}: checkout: moving from 68337260283c3e135b60c05dae2968b61d33204f to master
6833726 HEAD@{9}: checkout: moving from master to anchor
711506c HEAD@{10}: commit: update
cc4cd9a HEAD@{11}: checkout: moving from 68337260283c3e135b60c05dae2968b61d33204f to master
6833726 HEAD@{12}: checkout: moving from master to anchor
cc4cd9a HEAD@{13}: commit: update
6833726 HEAD@{14}: checkout: moving from 96da4a18ec4fe8a39db1a3b83ec59ed24f64659f to master
96da4a1 HEAD@{15}: checkout: moving from master to 96da
6833726 HEAD@{16}: commit: update README
57bfcf1 (origin/master) HEAD@{17}: commit: update README
```


### 変更内容の一時的な退避(git stash)
作業内容を一時的に保存する。
メモのような位置付けで使う。
作業中の状態ではコミットせずにスタッシュを使う。

```bash
# スタッシュの実行
$ git stash
Saved working directory and index state WIP on master: 5a06315 update

# スタッシュの確認
$ git stash list

# スタッシュの取り出し
$ git stash pop
Dropped refs/stash@{0} (2d2bcb26dc08904211cbfdbd5c321bae64792e04)
```

### マージする

```bash
# masterブランチにdevブランチをマージする
$ git checkout master
$ git merge dev
```

```bash
# ブランチの差分を確認する
# masterに対してdevの増分
$ git diff master...dev

# 変更の区分のみ確認する
$ git diff --name-status master...dev
M       README.md
```

```bash
# ログを確認
$ git log --graph --decorate --pretty=oneline --all --abgrev-commit
*   c3622a6 (HEAD -> master) Merge branch 'dev'
|\  
* | 0c66fca stashを反映しました。
* | 8d2b743 update bb
| | * 41edafd (refs/stash) WIP on dev: d340c1e update readme
| |/| 
| | * c653be3 index on dev: d340c1e update readme
| |/  
| * d340c1e (dev) update readme
| * 3741e24 update readme
|/  
* 4dcd887 update readme
* 5a06315 (origin/master) update
* 290ee84 update readme
* efe2b2b new branch
* 711506c update
* cc4cd9a update
* 6833726 update README
* 57bfcf1 update README
* 05fec74 add f
* 5d85678 add bb and update README
* 1202375 rename b to bb
* 2091f88 delete a
* fbc0bb2 finished section6
* 96da4a1 added new four files
* d673f05 update readme
* b3cf55f adding a text
* 14aac92 新しいファイルの追加
* 82b1418 update
* 4ed1895 update
* 132b89c initial commit
```


```bash
# マージコミットの親を確認する(最新のログ1件を取得する)
$ git log -1
```

### コンフリクトの解消

```bash
# マージツールの起動
$ git mergetool
```
vimdiffが起動するが、使い方が難解なので、
IDEのマージツールを使った方が良い。


### マージを中止する

```bash
$ git merge --abort
```

すでに実行したマージを元に戻すには別の手順が必要。


### fast-forward
早送りマージ。masterの位置を子孫の先頭に移動する。


### リモートの確認
```bash
$ git remote
$ git remote -v show
origin	git@github.com:tker-78/git-training.git (fetch)
origin	git@github.com:tker-78/git-training.git (push)
```

```bash
$ git branch --all
* master
  remotes/origin/master
```

```bash
# リモートの一覧の取得
$ git ls-remote
5a0631534496e21ae1eaaafe2c6eb6c478587099	HEAD
5a0631534496e21ae1eaaafe2c6eb6c478587099	refs/heads/master
```

### プッシュする

```bash
$ git remote -v show origin
* remote origin
  Fetch URL: git@github.com:tker-78/git-training.git
  Push  URL: git@github.com:tker-78/git-training.git
  HEAD branch: master
  Remote branch:
    master tracked
  Local branch configured for 'git pull':
    master merges with remote master
  Local ref configured for 'git push':
    master pushes to master (up to date)
```





