# GitHub に公開鍵の登録

GitHub は SSH と HTTPS の 2 つのプロトコルが利用できます。SSH を利用する場合は公開鍵秘密鍵を作成し GitHub に対応する公開鍵を登録する必要があります

鍵が作成できない or 扱えない人は行わなくて OK です(**その場合は以降 SSH の箇所は HTTPS で読み替えてください**)

## 鍵の作成

メールアドレスは GitHub に登録しているメールアドレスを設定しましょう。パスフレーズは設定しましょう

**ファイル名(省略した場合は id_rsa)について作成したファイルは一般的には`~/.ssh`に`600`で配置します。ファイル名が衝突する場合は適時命名してください**

```
$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
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

## 公開鍵のコピー

クリップボードに公開鍵をコピーしましょう

```
$ cat id_rsa.pub
```

## 鍵の登録

右上から settings -> SSH and GPG keys -> New SSH key 押下

![ssh-key](./images/ssh-key.png)

Title 記入 -> Key(作成した id_rsa.pub の内容をコピペ) -> Add SSH key 押下

![ssh-key2](./images/ssh-key2.png)

## 確認

ssh コマンドで`git`ユーザで`github.com`に対して接続確認を行う

```
$ ssh git@github.com
Enter passphrase for key ;
PTY allocation request failed on channel 0
Hi hironomiu! You've successfully authenticated, but GitHub does not provide shell access.
Connection to github.com closed.
```
