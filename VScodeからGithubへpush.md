### Visual Studio Code(以降 VScode)からGithubへpush

- 大まかな流れ
    1. Windows版のGitをインストール
        - 特に苦戦ポイントは無いので、よしなに調べてやればよい
    2. GitHubのリポジトリをVScodeのコンソールからGitクライアントを使いpull
        - PowerShellを使う
        - VScode は入っている前提
    3. VScodeからGitHubへpush

---
2. 

- VScodeからPowerShellを起動(ctrl + @)

```
Windows PowerShell
Copyright (C) Microsoft Corporation. All rights reserved.

PS C:\Users\kiyot> pwd

Path
----
C:\Users\kiyot


PS C:\Users\kiyot> ls


    ディレクトリ: C:\Users\kiyot


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----       2018/10/23     22:21                .android
d-----       2018/11/03     22:47                .eclipse
d-----       2018/11/16     22:08                .p2
d-----       2018/10/20     18:49                .tooling
d-----       2018/12/14      1:23                .VirtualBox
d-----       2018/10/20     13:24                .vscode
d-r---       2018/12/12     22:53                3D Objects
d-----       2018/11/18     10:14                Cisco Packet Tracer 7.1.1
d-r---       2018/12/12     22:53                Contacts
d-r---       2018/12/12     22:53                Desktop
d-----       2018/10/20      9:19                Documents
d-r---       2018/12/12     22:53                Videos
d-----       2018/10/20     21:51                VirtualBox VMs
d-----       2018/11/04     15:54                workspace
-a----       2018/11/25     12:58            176 .packettracer

```

- Linuxコマンドがどこまで使えるか確かめる

```
PS C:\Users\kiyot\Desktop\git\vscode> alias ls

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Alias           ls -> Get-ChildItem


PS C:\Users\kiyot\Desktop\git\vscode> alias pwd

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Alias           pwd -> Get-Location


PS C:\Users\kiyot\Desktop\git\vscode> alias cd

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Alias           cd -> Set-Location

PS C:\Users\kiyot\Desktop\git\vscode> alias rm

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Alias           rm -> Remove-Item

→基本的なコマンドはalias登録されていて、Linuxのノリでたたけそう


```
- gitが入っているか確認

```
PS C:\Users\kiyot> git
usage: git [--version] [--help] [-C <path>] [-c <name>=<value>]
           [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
           [-p | --paginate | -P | --no-pager] [--no-replace-objects] [--bare]
           [--git-dir=<path>] [--work-tree=<path>] [--namespace=<name>]
           <command> [<args>]

(略)

'git help -a' and 'git help -g' list available subcommands and some
concept guides. See 'git help <command>' or 'git help <concept>'
to read about a specific subcommand or concept.

```
- gitのセットアップ

```
PS C:\Users\kiyot> git config --global user.email "test@gmail.com"
PS C:\Users\kiyot> git config --global user.name "test"

```
- GitHubにアップロードするキーペアの生成

```
PS C:\Users\kiyot\.ssh> ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (C:\Users\kiyot/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in C:\Users\kiyot/.ssh/id_rsa.
Your public key has been saved in C:\Users\kiyot/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:rQCVWqWI/iydqfyymX07MNZG8Ff1WADfG/
The key's randomart image is:
+---[RSA 2048]----+
|      .o. .o+o+.o|
|   ..oo.  .. OEo.|
|  . o=.  .  = Bo |
| .  ..o .. . o + |
|  .  o..S .   o  |
|   ++oo. .       |
|  ..*+  .        |
| ..*  o          |
|  *+o..o         |
+----[SHA256]-----+

```
- 公開鍵をGitHubに登録

```
PS C:\Users\kiyot\.ssh> Get-Content .\id_rsa.pub
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDZOp8xkatEmSXdZjdyzM35iYiINDEL3zQ8L442w2JDA5pq5OeflRNRzMsJfgwG/Cbj9E6I4YSBs4hYjVDsqv3GTANB3Zn4t8vm+VdMVbzK/wDzmRGQzIyGextrcyCddi2VRHRdZqlIe3cdGXXYOgoOqOBFk7gcIzTmvBGftwo61J+Z+b94Kfu9z8ZV0hx+LuMGO7pGde8vSYrdHoj5ElljxURggEOsCC/deGqqXJsCywfAdM1XzH2lsR/qf2R+yhmXd5zjUjz/hj0Sr6WcsSgDZDXbRScwv0dakkyaZwMLcjIn6qLa19ZlTJR6qnom2dC6VvCTS00G5jsMUSx/ewZr kiyot@DESKTOP-UMR1JUL
PS C:\Users\kiyot\.ssh>

```
- ローカルリポジトリを作成してGitHubのリポジトリをクローン

```
PS C:\Users\kiyot\Desktop\git> git clone git@github.com:bullseys/vscode.git
Cloning into 'vscode'...
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Receiving objects: 100% (3/3), done.

PS C:\Users\kiyot\Desktop\git> Get-ChildItem


    ディレクトリ: C:\Users\kiyot\Desktop\git


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----       2018/12/22     16:36                vscode

→GitHubで作成したリポジトリが表示される

PS C:\Users\kiyot\Desktop\git\vscode> Set-Location C:\Users\kiyot\Desktop\git\vscode\

PS C:\Users\kiyot\Desktop\git\vscode> Get-ChildItem


    ディレクトリ: C:\Users\kiyot\Desktop\git\vscode


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----       2018/12/22     16:36             47 README.md

→GitHub上で作成したコンテンツが表示

```
- ここまでのメモをローカルリポジトリ上に保存する

```
PS C:\Users\kiyot\Desktop\git\vscode> Get-Location

Path
----
C:\Users\kiyot\Desktop\git\vscode

→ C: から始まるパスをエクスプローラーにコピペ
→メモをその中に保存

PS C:\Users\kiyot\Desktop\git\vscode> Get-ChildItem


    ディレクトリ: C:\Users\kiyot\Desktop\git\vscode


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----       2018/12/22     16:36             47 README.md
-a----       2018/12/22     16:25           5955 VScodeからGithubへpush.md

→保存されていることがPowerShell上からも確認できる

```
- 変更内容のステージング、push
    -  VScodeのGUIで操作
