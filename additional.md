# チーム開発 GitHub ことはじめ

## 準備

### ローカルで作業用ディレクトリの作成

任意のディレクトリで今回のリポジトリ用のディレクトリを「日付(YYYYMMDD)\_github」で作成

```
$ mkdir XXXXXXXX_github
$ cd XXXXXXXX_github
```

作成したディレクトリに遷移していること

```
$ pwd
XXXXX/XXXXXXXX_github
```

### git init

ローカルで git の初期化

```
$ git init
Initialized empty Git repository in XXXXX/XXXXXXXX_github/.git/
```

### README.md の作成

README.md の作成(touch で作成しているが普段利用しているエディタでも良い)

```
$ touch README.md
```

確認

```
$ ls
README.md
```

### add & commit

確認

```
$ git status
On branch main

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	README.md

nothing added to commit but untracked files present (use "git add" to track)
```

add

```
$ git add README.md
```

commit

```
$ git commit -m "first"
```

確認

```
$ git status
On branch main
nothing to commit, working tree clean
```

### GitHub リポジトリの作成

右上プルダウン「New repository」もしくは左上緑色アイコンを押下

![create_repo1](./images/create_repo1.png)

Repository name「日付(YYYYMMDD)\_github」、その他特に選択せず(Public を選択、「Initialize this repository with:」は何もチェックせず)、「Create repository」を押下

![create_repo2](./images/create_repo2.png)

利用プロトコルは「SSH」を選択、「…or push an existing repository from the command line」内のコマンドをクリップボードにコピー

![create_repo3](./images/create_repo3.png)

### リモートリポジトリの登録＆push

ターミナルにペースト

```
$ git remote add origin git@github.com:hironomiu/XXXXXXXX_github.git
$ git branch -M main
$ git push -u origin main
Warning: Permanently added 'github.com,52.69.186.44' (RSA) to the list of known hosts.
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Writing objects: 100% (3/3), 204 bytes | 204.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
To github.com:hironomiu/XXXXXXXX_github.git
 * [new branch]      main -> main
Branch 'main' set up to track remote branch 'main' from 'origin'.
```

### リロード

GitHub リポジトリをリロードし push が成功していることを確認

![create_repo4](./images/create_repo4.png)

## チームメンバー招待

準備で作成したリポジトリにチームメンバーを「コラボレータ」機能を用いて招待する

### collaborators に招待

「settings」タブを選択

![invite_collaborators1](./images/invite_collaborators1.png)

「Manage access」タブを選択

![invite_collaborators2](./images/invite_collaborators2.png)

GitHub アカウントのパスワードを入力し押下

![invite_collaborators3](./images/invite_collaborators3.png)

「invite a collaborator」を押下、招待するチームメンバーの GitHub アカウントを入力、下部にサジェストされる GitHub アカウントでチームメンバーのアカウントを選択(青くなる)し押下

![invite_collaborators4](./images/invite_collaborators4.png)

「Add XXXXX this repository」を押下

![invite_collaborators5](./images/invite_collaborators5.png)

招待されたチームメンバーにメールが届き、JOIN すると「Pending invite」のステータスが招待済のステータスに変わります

![invite_collaborators5](./images/invite_collaborators5.png)

## チームメンバーとしてオペレーション

### チームリポジトリにアクセス

collaborators に招待された GitHub リポジトリにアクセスし「code」を押下、「SSH」を選択しクリップボードにコピー

![team_development1](./images/team_development1.png)

### clone

任意のディレクトリ(これまでオペレーションしたディレクトリとは別で他のディレクトリ)でクリップボードにコピーした git repo の git clone を行う

```
$ git clone git@github.com:XXXXX/XXXXXXXX_github.git
```

ディレクトリ遷移

```
$ cd XXXXXXXX_github
$ pwd
xxxxx/XXXXXXXX_github
```

## チーム開発想定のオペレーション

チームでするべき issue を作成し、それを各メンバーが行うことでチーム開発的なオペレーションのトレーニングを行います

### GitHub issue の作成

「issues」タブを選択、「New Issue「New issue」を押下

![create_issue1](./images/create_issue1.png)

タイトル「<メンバー名>.md の作成」の記載(<>内は各自の GitHub アカウント名)、Write「 <メンバー名>.md の作成`hoge`の記載する」を記載し「Submit new issue」を押下

![create_issue2](./images/create_issue2.png)

作成した issue のパーマリンクを覚えておくこと(issue に限らず GitHub ではパーマリンクが作成される)

![create_issue3](./images/create_issue3.png)

### ローカルで開発

現在の branch を確認

```
$ git branch
* main
```

issue に紐づく branch を作成(xxxx は各自の GitHub アカウント名)し遷移

```
$ git branch create_xxxx_markdownfile
$ git switch create_hironomiu_markdownfile
Switched to branch 'create_hironomiu_markdownfile'
```

確認

```
$ git branch
* create_hironomiu_markdownfile
  main
```

### 開発想定の作業

<メンバー名>.md を作成し`hoge`を記載しセーブ

xxxx は各自の GitHub アカウント名

```
$ vi xxxx.md
$ cat xxxx.md
hoge
```

add & commit。commit メッセージに`fixed #1`を記載すること

```
$ git add .
$ git commit -m "create markdown file fixed #1"
[create_hironomiu_markdownfile 5a9a7dc] create markdown file fixd #1
 1 file changed, 1 insertion(+)
 create mode 100644 xxxx.md
```

push

```
$ git push origin create_hironomiu_markdownfile
Warning: Permanently added 'github.com,52.192.72.89' (RSA) to the list of known hosts.
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 4 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 290 bytes | 290.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
remote:
remote: Create a pull request for 'create_hironomiu_markdownfile' on GitHub by visiting:
remote:      https://github.com/hironomiu/XXXXXXXX_github/pull/new/create_hironomiu_markdownfile
remote:
To github.com:hironomiu/XXXXXXXX_github.git
 * [new branch]      create_hironomiu_markdownfile -> create_hironomiu_markdownfile
```

「Pull requests」タブの選択、「New pull request」を押下

![create_issue4](./images/create_issue4.png)

「compare」に今回 push した branch を選択、「Create pull request」を押下

![create_issue5](./images/create_issue5.png)

Write にメッセージがあれば記載(本来は LGTM は取り込み時に入れるメッセージ)、「Create pull request」を押下

![create_issue6](./images/create_issue6.png)

「Merge pull request」を押下(本来は PR の内容をレビューした後に行う)

![create_issue7](./images/create_issue7.png)

「Confirm merge」を押下

![create_issue8](./images/create_issue8.png)

「Delete branch」を押下(チームによっては消さない運用を選択する場合もあるが今回は削除する)

![create_issue9](./images/create_issue9.png)

`main`に取り込まれていることをブラウザで確認

![create_issue10](./images/create_issue10.png)

## ローカルに取り込み

チームメンバー(今回は自身のも)が開発し main に取り込まれた内容をローカルの main に取り込む

switch

```
$ git switch main
Switched to branch 'main'
Your branch is up to date with 'origin/main'.
```

fetch

```
$ git fetch origin main
Warning: Permanently added 'github.com,52.69.186.44' (RSA) to the list of known hosts.
remote: Enumerating objects: 1, done.
remote: Counting objects: 100% (1/1), done.
remote: Total 1 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (1/1), 630 bytes | 315.00 KiB/s, done.
From github.com:hironomiu/XXXXXXXX_github
 * branch            main       -> FETCH_HEAD
   562e5d2..2d5efe9  main       -> origin/main
```

merge

```
$ git merge FETCH_HEAD
Updating 562e5d2..2d5efe9
Fast-forward
 hironomiu.md | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 hironomiu.md
```

ファイルの確認

```
$ ll
total 8
drwxr-xr-x   5 miurahironori  staff  160  1 19 13:02 .
drwxr-xr-x   3 miurahironori  staff   96  1 19 11:56 ..
drwxr-xr-x  15 miurahironori  staff  480  1 19 13:02 .git
-rw-r--r--   1 miurahironori  staff    0  1 19 11:56 README.md
-rw-r--r--   1 miurahironori  staff    5  1 19 13:02 hironomiu.md
```
