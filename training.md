# Git&GitHub入門

## Git
基本的なgit操作(add,commit,etc)を学びます

### ディレクトリ作成と遷移
ワークツリー用のディレクトリを作製し遷移します。
```
$ mkdir git-practice
$ cd git-practice/
```

### Authorの確認
今回はglobalで設定します(プロジェクト毎に設定したい場合はlocalで設定しましょう)初めての場合は以下のエラーがでます。
```
$ git config --global --list
fatal: unable to read config file ‘/Users/h-miura/.gitconfig’: No such file or directory
```

設定(自身のuser.name、user.emailに置き換えましょう)
```
$ git config --global user.name hironomiu
$ git config --global user.email hironomiu@gmail.com
$ git config --global --list
user.name=hironomiu
user.email=hironomiu@gmail.com
```

### git操作
初期化によるローカルリポジトリの作製(ワークツリーの作製)
```
$ git init
Initialized empty Git repository in /xxxx/git-practice/.git/
```

branchの確認(何も表示されない。バージョンによっては`* master`が表示されることがある)
```
$ git branch
```

トラッキングの対象外の設定(`.gitignore`の作成)
```
$ touch .gitignore
$ ls .gitignore
.gitignore
```

giboを用いたトラッキングの対象外の設定(`.gitignore`の作成)。Macの場合`brew install gibo`でインストールでできる
```
$ gibo dump macOS >> .gitignore
```

ワークツリーでREADME.mdファイルの作成と編集
```
$ vi README.md
$ cat README.md
# git-practice
```

ステータス確認
```
$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   .gitignore
	new file:   README.md
```

add(インデックスに登録)
```
$ git add README.md
$ git add .gitignore
```

ステータス確認
```
$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   .gitignore
	new file:   README.md
```

commit(ローカルリポジトリに記録)
```
$ git commit -m "created .gitignore README.md"
[master (root-commit) 6af3859] created README.md
 2 files changed, 1 insertion(+)
 create mode 100644 .gitignore
 create mode 100644 README.md
```

ブランチの確認
```
$ git branch
* master
```

ステータス確認
```
$ git status
On branch master
nothing to commit, working tree clean
```

ログの確認
```
$ git log
commit 6af38593cd0476e4abfce0590582db58311bb424 (HEAD -> master)
Author: hironomiu <hironomiu@gmail.com>
Date:   Fri Dec 6 10:33:23 2019 +0900

    created README.md
```

Author,Commiterを確認
```
$ git log --pretty=fuller
commit 758a745499dbdad697e3eaa4f8e9bb9579f45a30 (HEAD -> master)
Author:     hironomiu <hironomiu@gmail.com>
AuthorDate: Mon Apr 20 13:07:08 2020 +0900
Commit:     hironomiu <hironomiu@gmail.com>
CommitDate: Mon Apr 20 13:07:08 2020 +0900

    created .gitignore README.md
```

README.mdの追記
```
$ vi README.md
$ cat README.md
# git-practice
hogefugapiyo
```

差分の確認
```
$ git diff README.md
diff --git a/README.md b/README.md
index 3e4b5a2..4d69739 100644
--- a/README.md
+++ b/README.md
@@ -1 +1,2 @@
 # git-practice
+hogefugapiyo
```

ステータスの確認
```
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")
```

ワーキングディレクトリ内の変更の取り消し(2.23.0以降は`git restore`で同様のことが可能)
```
$ git checkout README.md
Updated 1 path from the index
$ cat README.md
# git-practice
```

ステータス確認
```
$ git status
On branch master
```

README.mdの追記
```
$ vi README.md
$ cat README.md
# git-practice
piyofugahoge
```

ステータス確認
```
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")
```

差分の確認
```
$ git diff README.md
index 3e4b5a2..2565824 100644
--- a/README.md
+++ b/README.md
@@ -1 +1,2 @@
 # git-practice
+piyofugahoge
```

add(`git add .`はカレントディレクトリ全てを指定)
```
$ git add .
```

ステータス確認
```
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   README.md
```

差分の確認(何も返らない)
```
$ git diff README.md
```

インデックスの登録を取り消す
2.23.0以降は`git restore --staged README.md`がおすすめ
```
$ git reset HEAD README.md
Unstaged changes after reset:
M	README.md
```

ステータス確認
```
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   README.md
```

差分の確認
```
$ git diff README.md
diff --git a/README.md b/README.md
index 3e4b5a2..2565824 100644
--- a/README.md
+++ b/README.md
@@ -1 +1,2 @@
 # git-practice
+piyofugahoge
```

ファイル確認(変更内容は残っている)
```
$ cat README.md
# git-practice
piyofugahoge
```

add(インデックス登録)
```
$ git add .
```

ステータス確認
```
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   README.md
```

commit(ローカルリポジトリに記録)
```
$ git commit -m "modify README.md"
[master 0052cf3] modify README.md
 1 file changed, 1 insertion(+)
```

ステータス確認
```
$ git status
On branch master
nothing to commit, working tree clean
```

ログの確認
```
$ git log
commit 0052cf340c58c076ae01fc172d21bbac9861e223 (HEAD -> master)
Author: hironomiu <hironomiu@gmail.com>
Date:   Fri Dec 6 11:08:10 2019 +0900

    modify README.md

commit 6af38593cd0476e4abfce0590582db58311bb424
Author: hironomiu <hironomiu@gmail.com>
Date:   Fri Dec 6 10:33:23 2019 +0900
```

commitの取り消し(ワーキングディレクトリの内容も巻き戻し)
```
$ cat README.md
# git-practice
piyofugahoge

$ git reset --hard HEAD^

$ cat README.md
# git-practice
```

ログの確認
```
$ git log
commit 6af38593cd0476e4abfce0590582db58311bb424 (HEAD -> master, origin/master)
Author: hironomiu <hironomiu@gmail.com>
Date:   Fri Dec 6 10:33:23 2019 +0900

    created README.md
```

**commitの取り消し(インデックスに戻しワークツリーに戻す)**

README.mdの追記
```
$ vi README.md
$ cat README.md
# git-practice
piyofugahoge
```

add(インデックス登録)
```
$ git add .
```

commit(ローカルリポジトリに記録)
```
$ git commit -m "modify README.md"
[master 73d5417] modify README.md
 1 file changed, 1 insertion(+)
```

ログの確認
```
$ git log
commit 73d541704f634965f879285218c862ccb411758a (HEAD -> master)
Author: hironomiu <hironomiu@gmail.com>
Date:   Wed May 27 17:09:06 2020 +0900
    modify README.md
commit b9e365dd9205ebae5c5cc8cd78a147dafb828e68
Author: hironomiu <hironomiu@gmail.com>
Date:   Wed May 27 16:55:17 2020 +0900
    created .gitignore README.md
```

commitの取り消し(インデックスに戻す)
```
$ git reset --soft HEAD^
```

ステータス確認
```
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   README.md
```

ファイル確認(変更内容は残っている)
```
$ cat README.md
# git-practice
piyofugahoge
```

インデックスの取り消し
```
$ git restore --staged README.md
```

ファイルの確認
```
$ cat README.md
# git-practice
piyofugahoge
```

ステータスの確認
```
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   README.md
no changes added to commit (use "git add" and/or "git commit -a")
```

ワークツリーの取り消し
```
$ git restore README.md
```

ステータス確認
```
$ git status
On branch master
nothing to commit, working tree clean
```

ファイル確認
```
$ cat README.md
# git-practice
```

## GitHub

### 鍵の登録
鍵が作成できない or 扱えない人は行わなくてOKです

#### 鍵の作成

メールアドレスはGitHubに登録しているメールアドレスを設定しましょう。パスフレーズは設定しましょう

```
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/miurahironori/.ssh/id_rsa): ファイル名(省略した場合はid_rsa)
Enter passphrase (empty for no passphrase): パスフレーズ
Enter same passphrase again: パスフレーズ
Your identification has been saved in hoge.
Your public key has been saved in hoge.pub.
The key fingerprint is:
SHA256: hironomiu@gmail.com
The key's randomart image is:
+---[RSA 4096]----+

+----[SHA256]-----+
```
#### 公開鍵のコピー
クリップボードに公開鍵をコピーしましょう
```
$ cat id_rsa.pub
```

#### 鍵の登録
右上からsettings -> SSH and GPG keys -> New SSH key -> Title -> Key(作成したid_rsa.pubの内容をコピペ) -> Add SSH key

#### 確認
```
$ ssh git@github.com
Enter passphrase for key ;
PTY allocation request failed on channel 0
Hi hironomiu! You've successfully authenticated, but GitHub does not provide shell access.
Connection to github.com closed.
```

### リポジトリの作成
git-practiceで作成しましょう

Repositories -> New -> Repository name「git-practice」 -> Create repository

…or push an existing repository from the command lineの以下をローカルで実行
```
$ git remote add origin git@github.com:xxxxu/git-practice.git
$ git push -u origin master
Enter passphrase for key '/xxxx/.ssh/id_rsa':
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 12 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (4/4), 283 bytes | 283.00 KiB/s, done.
Total 4 (delta 0), reused 0 (delta 0), pack-reused 0
To github.com:hironomiu/git-practice.git
 * [new branch]      master -> master
Branch 'master' set up to track remote branch 'master' from 'origin'.
```

ブラウザをリロードしてGitの演習で作成した内容が反映されていることを確認

### 開発サイクル
これから開発サイクル「issue、branch、add、commit、push、pull request、merge」を行います

### issue
GitHubの画面から

issues -> New issue -> title「README編集」Write「fugahogepiyoを追記する」 -> Submit new issue

### branch
masterで活動してることを確認
```
$ git branch
* master
```

branchの作成
```
$ git branch modify-readme
$ git branch
* master
  modify-readme
```

modify-readmeに遷移(2.23.0以降は`git switch modify-readme`がおすすめ)
```
$ git checkout modify-readme
Switched to branch 'modify-readme'
```

### README.md編集
README.mdをissueの内容に沿って編集
```
$ vi README.md
$ cat README.md
# git-practice
fugahogepiyo
```

### add&commit
ステータス確認
```
$ git status
On branch modify-readme
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")
```

diff
```
$ git diff
diff --git a/README.md b/README.md
index 3e4b5a2..40551f9 100644
--- a/README.md
+++ b/README.md
@@ -1 +1,2 @@
 # git-practice
+fugahogepiyo
```

add
```
$ git add .
```

commit
```
$ git commit -m "#1 modify README.md"
[modify-readme aacfd67] #1 modify README.md
 1 file changed, 1 insertion(+)
```

ステータス確認
```
$ git status
On branch modify-readme
nothing to commit, working tree clean
```
 
### push
作成したmodify-readmeをpush
```
$ git push origin modify-readme
Enter passphrase for key '/Users/miurahironori/.ssh/id_rsa':
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Writing objects: 100% (3/3), 279 bytes | 139.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
remote:
remote: Create a pull request for 'modify-readme' on GitHub by visiting:
remote:      https://github.com/hironomiu/git-practice/pull/new/modify-readme
remote:
To github.com:hironomiu/git-practice.git
 * [new branch]      modify-readme -> modify-readme
```

### pull requestの作成とmerge
GitHubの画面から

Compare & pull request -> Write「fixed #1」 -> Create pull request -> Merge pull request -> Confirm merge -> Delete branch

## ローカル取り込み(fetch & merge)
リモートのmasterからローカルに取り込み
```
$ git branch
  master
* modify-readme
```

masterに遷移(2.23.0以降は`git switch`)
```
$ git checkout master
Switched to branch 'master'
Your branch is up to date with 'origin/master'.
$ git branch
* master
  modify-readme
```

fetch
```
$ git fetch origin master
Enter passphrase for key '/Users/miurahironori/.ssh/id_rsa':
remote: Enumerating objects: 1, done.
remote: Counting objects: 100% (1/1), done.
remote: Total 1 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (1/1), done.
From github.com:hironomiu/git-practice
 * branch            master     -> FETCH_HEAD
   6af3859..79dcedd  master     -> origin/master
```

diff
```
$ git diff HEAD FETCH_HEAD
diff --git a/README.md b/README.md
index 3e4b5a2..40551f9 100644
--- a/README.md
+++ b/README.md
@@ -1 +1,2 @@
 # git-practice
+fugahogepiyo
```

merge
```
$ git merge FETCH_HEAD
Updating 6af3859..79dcedd
Fast-forward
 README.md | 1 +
 1 file changed, 1 insertion(+)
```

diff(何もない)
```
$ git diff HEAD FETCH_HEAD
```

確認
```
$ cat README.md
# git-practice
fugahogepiyo
```

## 追加 CONFLICTの解消
### clone
GitHub -> Clone or download -> Use SSH -> クリップボードにコピー
```
$ git clone git@github.com:hironomiu/git-practice.git
Cloning into 'git-practice'...
Enter passphrase for key '/Users/miurahironori/.ssh/id_rsa':
remote: Enumerating objects: 19, done.
remote: Counting objects: 100% (19/19), done.
remote: Compressing objects: 100% (8/8), done.
remote: Total 19 (delta 4), reused 17 (delta 3), pack-reused 0
Receiving objects: 100% (19/19), done.
Resolving deltas: 100% (4/4), done.
```
ディレクトリ遷移
```
$ cd git-practice
```

最初のリポジトリ
```
$ git branch first
$ git checkout first
$ vi README.md
$ cat README.md
# git-practice
fugahogepiyo
first
$ git add .
$ git commit -m "first"
[first deea0c2] first
 1 file changed, 1 insertion(+)
# git push origin first
```

新しいリポジトリ
```
$ git branch second
$ git checkout second
$ vi README.md
$ cat README.md
# git-practice
fugahogepiyo
second
$ git add .
$ git commit -m "second"
$ git push origin second
```

### pull requestの作成とmerge
GitHubの画面から

Compare & pull request -> Write「first」 -> Create pull request -> Merge pull request -> Confirm merge -> Delete branch


### pull requestの作成とmerge
GitHubの画面から

Compare & pull request -> Write「second」 -> Create pull request -> Merge pull request -> Confirm merge -> Delete branch

`Can’t automatically merge.` が表示される

新しいリポジトリ(secondを編集)でfetch
```
$ git fetch origin master
```
merge
```
$ git merge FETCH_HEAD
Auto-merging README.md
CONFLICT (content): Merge conflict in README.md
Automatic merge failed; fix conflicts and then commit the result.
```
内容を確認
```
$ cat README.md
# git-practice
fugahogepiyo
<<<<<<< HEAD
second
=======
first
>>>>>>> e968e86c05394d2d6d14fe8e1cc5727841772257
```
CONFLICTを解消
```
$ vi README.md
$ cat README.md
# git-practice
fugahogepiyo
second
first
```
add&commit
```
$ git add .
$ git commit -m "CONFLICTの修正"
```

push
```
$ git push origin second
```

GitHubの画面から

Confirm merge -> Delete branch
