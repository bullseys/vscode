### VScodeからGithubへpush

- PowerShellを使う

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
d-r---       2018/12/22     11:06                Downloads
d-----       2018/12/21     21:28                dwhelper
d-r---       2018/12/12     22:53                Favorites
d-r---       2018/12/12     22:53                Links
d-r---       2018/12/12     22:53                Music
dar---       2018/10/20     21:43                OneDrive
d-r---       2018/12/12     22:53                Saved Games
d-r---       2018/12/12     22:53                Searches
d-r---       2018/12/12     22:53                Videos
d-----       2018/10/20     21:51                VirtualBox VMs
d-----       2018/11/04     15:54                workspace
-a----       2018/11/25     12:58            176 .packettracer

PS C:\Users\kiyot> git
usage: git [--version] [--help] [-C <path>] [-c <name>=<value>]
           [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
           [-p | --paginate | -P | --no-pager] [--no-replace-objects] [--bare]
           [--git-dir=<path>] [--work-tree=<path>] [--namespace=<name>]
           <command> [<args>]

These are common Git commands used in various situations:

start a working area (see also: git help tutorial)
   clone      Clone a repository into a new directory
   init       Create an empty Git repository or reinitialize an existing one

work on the current change (see also: git help everyday)
   add        Add file contents to the index
   mv         Move or rename a file, a directory, or a symlink
   reset      Reset current HEAD to the specified state
   rm         Remove files from the working tree and from the index

examine the history and state (see also: git help revisions)
   bisect     Use binary search to find the commit that introduced a bug
   grep       Print lines matching a pattern
   log        Show commit logs
   show       Show various types of objects
   status     Show the working tree status

grow, mark and tweak your common history
   branch     List, create, or delete branches
   checkout    Switch branches or restore working tree files
   commit     Record changes to the repository
   diff       Show changes between commits, commit and working tree, etc
   merge      Join two or more development histories together
   rebase     Reapply commits on top of another base tip
   tag        Create, list, delete or verify a tag object signed with GPG

collaborate (see also: git help workflows)
   fetch      Download objects and refs from another repository
   pull       Fetch from and integrate with another repository or a local branch
   push       Update remote refs along with associated objects

'git help -a' and 'git help -g' list available subcommands and some
concept guides. See 'git help <command>' or 'git help <concept>'
to read about a specific subcommand or concept.
PS C:\Users\kiyot> git config --global user.email "bullseye.takuramakan@gmail.com"
PS C:\Users\kiyot> git config --global user.name "bullseye"
PS C:\Users\kiyot> ls

PS C:\Users\kiyot\.ssh> ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (C:\Users\kiyot/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in C:\Users\kiyot/.ssh/id_rsa.
Your public key has been saved in C:\Users\kiyot/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:rQCVWqWI/iydqfyymX07MNZG8Ff1WADfG/CD9hTXMpQ kiyot@DESKTOP-UMR1JUL
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

PS C:\Users\kiyot\.ssh> Get-Content .\id_rsa.pub
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDZOp8xkatEmSXdZjdyzM35iYiINDEL3zQ8L442w2JDA5pq5OeflRNRzMsJfgwG/Cbj9E6I4YSBs4hYjVDsqv3GTANB3Zn4t8vm+VdMVbzK/wDzmRGQzIyGextrcyCddi2VRHRdZqlIe3cdGXXYOgoOqOBFk7gcIzTmvBGftwo61J+Z+b94Kfu9z8ZV0hx+LuMGO7pGde8vSYrdHoj5ElljxURggEOsCC/deGqqXJsCywfAdM1XzH2lsR/qf2R+yhmXd5zjUjz/hj0Sr6WcsSgDZDXbRScwv0dakkyaZwMLcjIn6qLa19ZlTJR6qnom2dC6VvCTS00G5jsMUSx/ewZr kiyot@DESKTOP-UMR1JUL
PS C:\Users\kiyot\.ssh>

PS C:\Users\kiyot\.ssh> git clone git@github.com:bullseys/test.git
Cloning into 'test'...
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Receiving objects: 100% (3/3), done.

PS C:\Users\kiyot\.ssh> Get-ChildItem


    ディレクトリ: C:\Users\kiyot\.ssh


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----       2018/12/22     16:24                test
-a----       2018/12/22     16:15           1679 id_rsa
-a----       2018/12/22     16:15            404 id_rsa.pub
-a----       2018/12/22     16:08            407 known_hosts