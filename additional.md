# チーム開発GitHubことはじめ

## 準備
### ローカルで作業用ディレクトリの作成
任意のディレクトリで今回のリポジトリ用のディレクトリを「日付(YYYYMMDD)_github」で作成

```
$ mkdir 20210119_github
$ cd 20210119_github
```

作成したディレクトリに遷移していること

```
$ pwd
XXXXX/20210119_github
```

### git init
ローカルでgitの初期化

```
$ git init
Initialized empty Git repository in XXXXX/20210119_github/.git/
```

### README.mdの作成
README.mdの作成(touchで作成しているが普段利用しているエディタでも良い)

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

### GitHubリポジトリの作成
右上プルダウン「New repository」もしくは左上緑色アイコンを押下

![create_repo1](./images/create_repo1.png)

Repository name「日付(YYYYMMDD)_github」、その他特に選択せず(Publicを選択、「Initialize this repository with:」は何もチェックせず)、「Create repository」を押下

![create_repo2](./images/create_repo2.png)

利用プロトコルは「SSH」を選択、「…or push an existing repository from the command line」内のコマンドをクリップボードにコピー

![create_repo3](./images/create_repo3.png)

### リモートリポジトリの登録＆push
ターミナルにペースト

```
$ git remote add origin git@github.com:hironomiu/20210119_github.git
$ git branch -M main
$ git push -u origin main
Warning: Permanently added 'github.com,52.69.186.44' (RSA) to the list of known hosts.
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Writing objects: 100% (3/3), 204 bytes | 204.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
To github.com:hironomiu/20210119_github.git
 * [new branch]      main -> main
Branch 'main' set up to track remote branch 'main' from 'origin'.
```

### リロード
GitHubリポジトリをリロードしpushが成功していることを確認

![create_repo4](./images/create_repo4.png)

## チームメンバー招待
準備で作成したリポジトリにチームメンバーを「コラボレータ」機能を用いて招待する

### collaboratorsに招待
「settings」タブを選択

![invite_collaborators1](./images/invite_collaborators1.png)

「Manage access」タブを選択

![invite_collaborators2](./images/invite_collaborators2.png)

GitHubアカウントのパスワードを入力し押下

![invite_collaborators3](./images/invite_collaborators3.png)

「invite a collaborator」を押下、招待するチームメンバーのGitHubアカウントを入力、下部にサジェストされるGitHubアカウントでチームメンバーのアカウントを選択(青くなる)し押下

![invite_collaborators4](./images/invite_collaborators4.png)

「Add XXXXX this repository」を押下

![invite_collaborators5](./images/invite_collaborators5.png)

招待されたチームメンバーにメールが届き、JOINすると「Pending invite」のステータスが招待済のステータスに変わります

![invite_collaborators5](./images/invite_collaborators5.png)


## チームメンバーとしてオペレーション

### チームリポジトリにアクセス
collaboratorsに招待されたGitHubリポジトリにアクセスし「code」を押下、「SSH」を選択しクリップボードにコピー

![team_development1](./images/team_development1.png)

### clone
任意のディレクトリでクリップボードにコピーしたgit repoのgit cloneを行う

```
$ git clone git@github.com:XXXXX/20210119_github.git
```

ディレクトリ遷移

```
$ cd 20210119_github
$ pwd
xxxxx/20210119_github
```

## チーム開発想定のオペレーション
チームでするべきissueを作成し、それを各メンバーが行うことでチーム開発的なオペレーションのトレーニングを行う

### GitHub issueの作成
  - メンバー分issue作成「メンバー.mdの作成」-> <メンバー名>.mdの作成「hoge」の記載

### ローカルで開発
　- issueに紐づくbranchの作成 -> git switch -> <メンバー>.mdの作成 -> git add -> git commit -> git push -> pr -> merge

### ローカルに取り込み
  - git switch main -> git fetch -> git merge

