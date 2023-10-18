<a name="Y9WYc"></a>
# Git 配置多账号记录
<a name="feE7n"></a>
## 0.0 相关文章置顶
本文参考博客文章里链接如下：
[通过 ssh config 配置 Git 多账户 SSH 登录](https://hanpanpan200.github.io/2019/10/14/setup-multiple-git-accounts-by-ssh-config/)

[配置多个 Git 账号 - 掘金](https://juejin.cn/post/7124197374318084127)

---


<a name="LvXqP"></a>
## 0.1 生成秘钥

在此之前，可以尝试使用 ` ssh -V (大写) `   查看ssh 的版本<br />比如我的返回 : OpenSSH_9.2p1, OpenSSL 1.1.1t  7 Feb 2023
```
ssh-V 是一个命令，用于查看 SSH 客户端的版本和支持的加密算法。
SSH 是一种安全的远程登录协议，可以用于连接到其他计算机或服务器。

OpenSSH_9.2p1 是 SSH 客户端的版本号，表示您使用的是 OpenSSH 的 9.2 版本，p1 表示第一个补丁。
OpenSSH 是一种开源的 SSH 实现，由 OpenBSD 项目开发。

OpenSSL 1.1.1t 7 Feb 2023 是 SSL 库的版本号，表示您使用的是 OpenSSL 的 1.1.1 版本
t 表示第二十个补丁，7 Feb 2023 表示发布日期。OpenSSL 是一种开源的 SSL 实现，用于提供加密和证书功能。

这些信息可以帮助您了解您的 SSH 客户端的功能和兼容性，以及是否需要更新或升级。


echo $(($(echo -n "$(cat ~/.ssh/id_rsa.pub | cut -d'' -f2)" | base64 -d | wc -c) * 8))
```


使用命令，将你所拥有的各个平台的账号都生成一个公钥和私钥，私钥自己留存，公钥则放置在对应的平台用来加密和解密。<br />比如我现在的需求是，公司有个gitlab的账号，但是我自己也有个github甚至还有个国内gittee平台的账号。<br />提交代码的时候，我需要有着切换账号的功能，将不同的代码通过不同的账号提交到对应的平台。

```git
ssh-keygen -t <算法> -b <长度> -C <注释>
# 本文改用ed25519创建
ssh-keygen -t ed25519 -C "Your_GitHub_Email"
ssh-keygen -t ed25519 -C "Your_GitLab_Email" -f my_gitlab
------------------------------------------------------------
# 使用命令生成对称秘钥 --github
ssh-keygen -t rsa -C 'Your_GitHub_Email'
# 使用命令生成对称秘钥 --gitlab
ssh-keygen -t rsa -C 'Your_GitLab_Email' -f my_gitlab
```

> 注意：这次添加了-f my_gitlab 这样，~/.ssh 目录下就会生成my_gitlab 和 my_gitlab.pub 文件，将my_gitlab.pub 的内容添加到 gitlab 账户的 Setting 里面

<a name="K7U7P"></a>
## 0.2 将私钥配置到 Git 中
```shell
ssh-add id_ed25519  # 添加第一个账户 github
ssh-add my_gitlab  # 添加第二个账户 gitlab
---------------------------------------------------------
ssh-add id_rsa  # 添加第一个账户 github
ssh-add my_gitlab  # 添加第二个账户 gitlab
```

如果将私钥添加到 git 中的时候，出线如下英文：<br />Could not open a connection to your authentication agent.

那么你需要先使用如下命令，开启ssh-add功能（ 该开启命令仅限于window，其他系统会有所变更。）
```git
eval `ssh-agent -s`
```

查看结果图片结果应该如图所示：![1681278717826.jpg](https://cdn.nlark.com/yuque/0/2023/jpeg/33584294/1681278724499-45f3a0e9-97ac-4b31-9547-e6fb4c3fc1d3.jpeg#averageHue=%23030201&clientId=u4173c0a9-4308-4&from=paste&height=180&id=u2dab729b&originHeight=62&originWidth=380&originalType=binary&ratio=1&rotation=0&showTitle=false&size=2809&status=done&style=none&taskId=u7e181432-d7f3-4710-a646-e3cbaa230ac&title=&width=1103)

![1681278876579.png](https://cdn.nlark.com/yuque/0/2023/png/33584294/1681278886414-459841d6-47da-45fc-aee1-0d26d48878da.png#averageHue=%23070604&clientId=u4173c0a9-4308-4&from=paste&height=333&id=u2e651943&originHeight=111&originWidth=385&originalType=binary&ratio=1&rotation=0&showTitle=false&size=7774&status=done&style=none&taskId=u46c36b84-dbb1-4575-a9d5-6e9d491c249&title=&width=1156)

直接创建config文件（没有后缀，直接config） ， 然后配置这个文件中的内容。

- Host：标识一个配置区间，此处 * 意为匹配所有的 host
- IdentityFile: 指定秘钥认证使用的私钥文件路径，此处默认为 ~/.ssh/id_rsa
- UseKeychain yes  AddKeysToAgent yes  设置后让电脑保存ssh秘钥密码，避免频繁输入密码。
   - 注意 ： window上UseKeychain yes  时 ssh会报错, 所以本文直接没写。
```
# config文件

# GitHub
Host personal-Yaogui
HostName github.com  # 这里是托管平台的域名
identityFile ~/.ssh/id_ed25519 #使用rsa创建就是id_rsa

# Gitlab
Host company-Yaogui
HostName gitlab.com
identityFile ~/.ssh/my_gitlab
```

最后需要在clone代码是注意处理下ssh host ![1681280401734.png](https://cdn.nlark.com/yuque/0/2023/png/33584294/1681280407306-a990084b-7874-4b50-9500-963bab7e5b86.png#averageHue=%23f6f5f4&clientId=u1cfbca65-ed09-4&from=paste&height=336&id=u9904e094&originHeight=388&originWidth=926&originalType=binary&ratio=1&rotation=0&showTitle=false&size=67312&status=done&style=none&taskId=u6cf9e366-f20c-4029-bdc2-dc065f0512e&title=&width=801)

然后就是需要去gitlab或者是github上添加自己生成的公钥的。<br />github： settings => SSH and GPG keys  => Add new<br />gitlab:   Edit profile  => SSH Keys <br />最后测试一下是否链接成功，如果连接失败肯定是不能clone代码的。
```git
# @ 符号后为自己设置的host

ssh -T git@personal-Yaogui
ssh -T git@company-Yaogui
```

链接成功的时候会让你确认是否链接，输入yes就行![1681354471760.png](https://cdn.nlark.com/yuque/0/2023/png/33584294/1681354482488-30d5735f-7d06-4b1b-919b-3cc8943c4c55.png#averageHue=%230c0b09&clientId=u5fa83cef-2902-4&from=paste&height=641&id=ud6178eaa&originHeight=564&originWidth=962&originalType=binary&ratio=1&rotation=0&showTitle=false&size=63811&status=done&style=none&taskId=uf984f3d4-6e3f-465d-850e-fe204266699&title=&width=1094)


现在唯一需要注意的一点就是，在下载对应网站的项目代码的时候，需要将对应的网站改成自己命名的host。<br />原来下载一个github项目是如下方式：
```
git clone  git@github.com:arcaneyaogui/study_with_me.git
```
需要将github的网址那块，改成自己在config中配置的host：
```
git clone  git@personal-Yaogui:arcaneyaogui/study_with_me.git
```
gitlab 项目也是同理

最后在仓库中修改提交的时候需要配置信息
```git
git config user.name "用户名"
git config user.email "邮箱号"
```
<br />全局配置（建议全局配置主 Git 账户）

```git
git config --global user.name arcaneyaogui
git config --global user.email arcane.yaogui@outlook.com
```

---

config配置有3个层级：

- system（系统级别）
- global（用户级别）
- local（仓库级别）

覆盖优先级为local > global > system , 优先读取local，其次是global，最后是system。
<a name="QJOSs"></a>
## 0.3 查看配置
读取system级别的配置
```cpp
$ git config --system --list
```
读取global级别的配置
```php
$ git config --global --list
```
读取local级别的配置<br />配置全局的主账户信息
```csharp
$ git config --global user.name "yourusername"
$ git config --global user.email "youremail@email.com"
```
删除配置信息
```bash
$ git config --unset user.name
```


---


<a name="WtbPB"></a>
# Git 使用命令记录
<a name="QPsp9"></a>
## 1.0 本地空文件夹拉去远端仓库

将空文件初始化为git仓库
```git
git init  
```

链接远端仓库，并设置别名方便标识。<br />不设置别名,默认是 origin 
```git
#查看有哪些远端仓库
git remote -v  

#添加远端仓库命令
git remote add <别名> <仓库的 网址/ssh>
#上文中改了config文件,所以这里需要把github编程personal-Yaogui
git remote add study git@personal-Yaogui:arcaneyaogui/study_with_me.git
```

拉去新仓库的时候,由于本地没有以往的分支信息,需要先抓取一下这个仓库远端的分支信息到本地.<br />这个命令会访问远程仓库，从中拉取所有你还没有的数据。 执行完成后，你将会拥有那个远程仓库中所有分支的引用，可以随时合并或查看
```git
git fetch study # study改成你的别名或者仓库地址
```
这里要注意，fetch 将所有的信息获取下来，但是不会给你合并这些信息。<br />所以必须要fetch之后使用pull命令拉取一下该仓库中的代码，让它自动合并。
```git
# study：你远端仓库别名 main则为该仓库中的远端分支。
git pull study main
```

如果想要查看某一个远程仓库的更多信息，可以使用 git remote show <remote> 命令。
```git
git remote show study

------------------------------------------------------------------------
$ git remote show study
* remote study
  Fetch URL: git@personal-Yaogui:arcaneyaogui/study_with_me.git
  Push  URL: git@personal-Yaogui:arcaneyaogui/study_with_me.git
  HEAD branch: main
  Remote branches:
    learnbook tracked
    main      tracked
```
还可以通过 git remote show 看到更多的信息。

倘若你觉得你刚刚起的别名不好听,可以重命名
```git
git remote rename <原来名字> <新名字>
```
移除现有的远端仓库
```git
git remote remove <别名 or 网址>
```
使用切换分支命令创建分支并切换到新分支.
```git
git checkout -b <分支名>

#也可以使用分支命令创建
git branch <分支名>
```
#查看所有分支（注意：fetch后 branch -a本地分支显示不出来，需要pull之后，本地分支才会显示）
```git
git branch -a  #查看所有分支
git branch -r  #查看远端分支
```

如果是第一次推送的时候 ， push 命令后 需要添加 ` -u ` 属性。<br />创建远端的分支 , 就是恩地创建新分支后,提交代码,然后将这个本地新分支岁送到远端,远端就会自动创建
```git
# 注意!! 冒号前后不能有空格
git push study-vue coding:coding
```

---

<a name="QPmBE"></a>
# Git  问题记录
<a name="oJXqs"></a>
## 1. fetch 抓取gitlab 仓库没反应（windows下）
尝试使用 winpty 包：<br />winpty 是一个 Windows 软件包，提供一个类似于 Unix pty-master 的接口，用于与 Windows 控制台程序通信
```git
winpty git fetch
```
说实话还是有点离谱的，2023-4-14 今天我使用gitlab，但是fetch 还是 pull 命令，都需要添加winpty才能运行，系统是win11家庭中文版（公司的）。


---

**fatal: refusing to merge unrelated histories**<br />因为本地仓库和远程仓库没有共同的提交历史，导致 Git 无法将它们合并在一起。为了解决这个问题，在 git merge 命令中添加 --allow-unrelated-histories 参数，以允许合并不相关的历史记录。<br />运行以下命令将远程仓库与本地仓库关联：<br />git remote add origin <GitHub仓库的URL><br />运行以下命令从远程仓库获取最新的更新：
```git
git fetch origin
```
运行以下命令将远程分支合并到本地分支（假设您要将远程分支 main 合并到本地分支 master）：
```git
git merge origin/main --allow-unrelated-histories
```
运行以下命令将合并后的更改推送到远程仓库：
```git
git push origin master
```
请注意，根据您的实际情况，您可能需要将远程分支和本地分支的名称替换为适当的值。
