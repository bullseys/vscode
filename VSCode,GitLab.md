### VSCode,PowerShell,GitLabを使った分散型バージョン管理の実践

- 今回やること
    - 以前VPS用に作成したGitLabのプライベートリモートリポジトリからWindowsのローカルリポジトリにclone
    - VSCodeとPowerShellを使い、編集してGitLabにpush
    - VPSにログインし、pullすることでWindowsからの変更内容をGitLabを通して取り込む

- GitLabにWindows側の公開鍵を登録

```
PS C:\Users\kiyot\Desktop\git\vps> Get-Content C:\Users\kiyot\.ssh\id_rsa.pub
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDZOp8xkatEmSXdZjdyzM35iYiINDEL3zQ8L442w2JDA5pq5OeflRNRzMsJfgwG/Cbj9E6I4YSBs4hYjVDsqv3GTANB3Zn4t8vm+VdMVbzK/wDzmRGQzIyGextrcyCddi2VRHRdZqlIe3cdGXXYOgoOqOBFk7gcIzTmvBGftwo61J+Z+b94Kfu9z8ZV0hx+LuMGO7pGde8vSYrdHoj5ElljxURggEOsCC/deGqqXJsCywfAdM1XzH2lsR/qf2R+yhmXd5zjUjz/hj0Sr6WcsSgDZDXbRScwv0dakkyaZwMLcjIn6qLa19ZlTJ

→これをGitLabに登録

```
- ローカルリポジトリにGitLabのリモートリポジトリをclone

```
Windows PowerShell
Copyright (C) Microsoft Corporation. All rights reserved.

PS C:\Users\kiyot> Set-Location C:\Users\kiyot\Desktop\git\

PS C:\Users\kiyot\Desktop\git> git clone git@gitlab.com:bullseyes/vps.git
Cloning into 'vps'...
The authenticity of host 'gitlab.com (35.231.145.151)' can't be established.
ECDSA key fingerprint is SHA256:HbW3
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'gitlab.com,35.231.145.151' (ECDSA) to the list of known hosts.
remote: Enumerating objects: 15, done.
remote: Counting objects: 100% (15/15), done.
remote: Compressing objects: 100% (13/13), done.
remote: Total 15 (delta 4), reused 0 (delta 0)
Receiving objects: 100% (15/15), done.
Resolving deltas: 100% (4/4), done.

→初回の認証を終え、cloneできた

```
- コンテンツの確認

```
PS C:\Users\kiyot\Desktop\git> Get-ChildItem


    ディレクトリ: C:\Users\kiyot\Desktop\git


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----       2018/12/22     23:18                vps
d-----       2018/12/22     21:45                vscode

→vps がcloneできた

PS C:\Users\kiyot\Desktop\git> Set-Location .\vps\

PS C:\Users\kiyot\Desktop\git\vps> Get-ChildItem


    ディレクトリ: C:\Users\kiyot\Desktop\git\vps


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----       2018/12/22     23:18             64 jenkins_practice.sh
-a----       2018/12/22     23:18             79 local.md
-a----       2018/12/22     23:18             51 README.md

→privateリモートリポジトリにあるものと同じコンテンツ

```
- VSCodeで編集、GitLabにpush
    - ここまでの手順をローカルリポジトリに保存
    - C: から始まるパスをエクスプローラーにコピペした先に保存

```
PS C:\Users\kiyot\Desktop\git\vps> Get-Location

Path
----
C:\Users\kiyot\Desktop\git\vps

```
- 確認

```
PS C:\Users\kiyot\Desktop\git\vps> Get-ChildItem


    ディレクトリ: C:\Users\kiyot\Desktop\git\vps


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----       2018/12/22     23:18             64 jenkins_practice.sh
-a----       2018/12/22     23:18             79 local.md
-a----       2018/12/22     23:18             51 README.md
-a----       2018/12/22     23:58           2935 VSCode,GitLab.md

```
- VSCodeのGUIでリモートリポジトリにpush
    - GUIなので手順は割愛

- GitLabで確認

- VPSにログイン

```
SAKURA Internet [Virtual Private Server SERVICE]

[kiyota@tk2-241-30361 ~]$ sudo su -
Last login: Fri Dec 21 22:44:50 JST 2018 on pts/0

```
- ローカルリポジトリの確認

```
[root@tk2-241-30361 ~]# ls -al /root/gitlab/workspace/vps/
合計 12
drwxr-xr-x 3 root root  78 12月 19 23:50 .
drwxr-xr-x 4 root root  30 12月 19 23:02 ..
drwxr-xr-x 8 root root 220 12月 19 23:51 .git
-rw-r--r-- 1 root root  49 12月 19 22:47 README.md
-rw-r--r-- 1 root root  62 12月 19 22:53 jenkins_practice.sh
-rw-r--r-- 1 root root  75 12月 19 23:50 local.md

```
- GitLabからpull

```
[root@tk2-241-30361 ~]# cd /root/gitlab/workspace/vps/
[root@tk2-241-30361 ~/gitlab/workspace/vps]# git pull
remote: Enumerating objects: 4, done.
remote: Counting objects: 100% (4/4), done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 3 (delta 0), reused 0 (delta 0)
Unpacking objects: 100% (3/3), done.
From gitlab.com:bullseyes/vps
   5bbd8ff..c7591e4  master     -> origin/master
Updating 5bbd8ff..c7591e4
Fast-forward
 VSCode,GitLab.md | 106 ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
 1 file changed, 106 insertions(+)
 create mode 100644 VSCode,GitLab.md

[root@tk2-241-30361 ~/gitlab/workspace/vps]# ls -al
合計 16
drwxr-xr-x 3 root root  102 12月 23 00:12 .
drwxr-xr-x 4 root root   30 12月 19 23:02 ..
drwxr-xr-x 8 root root  220 12月 23 00:12 .git
-rw-r--r-- 1 root root   49 12月 19 22:47 README.md
-rw-r--r-- 1 root root 3700 12月 23 00:12 VSCode,GitLab.md
-rw-r--r-- 1 root root   62 12月 19 22:53 jenkins_practice.sh
-rw-r--r-- 1 root root   75 12月 19 23:50 local.md

→WindowsのローカルリポジトリからpushしたファイルがGitLabを通してpullで反映された

```
- ここまでの手順をWindowsのローカルリポジトリからGitLab,GitHubにpush

```

S C:\Users\kiyot> Get-ChildItem C:\Users\kiyot\Desktop\git\vps\


    ディレクトリ: C:\Users\kiyot\Desktop\git\vps


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----       2018/12/22     23:18             64 jenkins_practice.sh
-a----       2018/12/22     23:18             79 local.md
-a----       2018/12/22     23:18             51 README.md
-a----       2018/12/23      0:17           5810 VSCode,GitLab.md


PS C:\Users\kiyot> Copy-Item 'C:\Users\kiyot\Desktop\git\vps\VSCode,GitLab.md' C:\Users\kiyot\Desktop\git\vscode\
PS C:\Users\kiyot> echo $?
True

→コピーは正常に実行された

PS C:\Users\kiyot> Get-ChildItem C:\Users\kiyot\Desktop\git\vscode\


    ディレクトリ: C:\Users\kiyot\Desktop\git\vscode


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----       2018/12/22     17:44             86 README.md
-a----       2018/12/23      0:17           5810 VSCode,GitLab.md
-a----       2018/12/22     21:50           8015 VScodeからGithubへpush.md

→確認できた
→後はVSCodeのGUIかPowerShellのCLIでpushするだけ

PS C:\Users\kiyot\Desktop\git\vscode> git add .

PS C:\Users\kiyot\Desktop\git\vscode> git commit -m "this change contains from both GitLab and VSCode"
[master 87b4f8c] this change contains from both GitLab and VSCode
 1 file changed, 162 insertions(+)
 create mode 100644 VSCode,GitLab.md

PS C:\Users\kiyot\Desktop\git\vscode> git push
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 8 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 2.55 KiB | 2.55 MiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To github.com:bullseys/vscode.git
   9bbbbf3..87b4f8c  master -> master

```
- [GitHubのリモートリポジトリはpublic設定になっているので見れる](https://github.com/bullseys/vscode)
