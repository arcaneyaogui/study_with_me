# Hadoop 安装教程

创建一个Hadoop用户 

```shell
sudo useradd -m hadoop -s /bin/bash
```

在home文件夹下,使用ls能够看见hadoop表示创建成功.

使用如下命令,将hadoop用户的密码设置成 hadoop 

```shell
sudo passwd hadoop
```

给 hadoop 用户 添加管理员权限,方便后面的命令执行.

```shell
sudo adduser hadoop sudo
```

切换到用户 hadoop

```shell
su hadoop
```

先更新一下 apt，后续我们使用 apt 安装软件，如果没更新可能有一些软件安装不了。

```shell
sudo apt-get update
```

安装 vim 方便编辑文件.

```shell
sudo apt-get install vim
vim -version #查看版本
```

看教程说是 集群、单节点模式都需要用到 SSH 登陆（类似于远程登陆，你可以登录某台 Linux 主机，并且在上面运行命令），Ubuntu 默认已安装了 SSH client，此外还需要安装 SSH server

```shell
sudo apt-get install openssh-server
```

可以使用 `  ssh localhost `登陆本机,但是每一次需要输入密码.

首先退出刚才的 ssh，就回到了我们原先的终端窗口，然后利用 ssh-keygen 生成密钥，并将密钥加入到授权中：

```shell
exit                           				# 退出刚才的 
ssh localhostcd ~/.ssh/                     # 若没有该目录，请先执行一次
ssh localhostssh-keygen -t rsa              # 会有提示，都按回车就可以
cat ./id_rsa.pub >> ./authorized_keys  		# 加入授权
```

**~的含义**: 在 Linux 系统中，~ 代表的是用户的主文件夹，即 "/home/用户名" 这个目录，如你的用户名为 hadoop，则 ~ 就代表 "/home/hadoop/"。 
此时再用 `ssh localhost` 命令，无需输入密码就可以直接登陆了

---



## 安装 JDK1.8 

首先下载好 JDK1.8 , 创建存放与安装jdk1.8的文件夹,
然后使用 Mobaxterm 上传文件 , 用命令进行解压和安装.

```shell
cd /usr/libs
sudo mkdir jvm 			#创建/usr/lib/jvm目录用来存放JDK文件
sudo mkdir jvmFiles 	#创建/usr/lib/jvmFiles目录安装JDK文件
sudo tar -zxvf jdk-8u162-linux-x64.tar.gz -C ./jvmFiles  #把JDK文件解压到/usr/lib/jvm目录下
```

使用 ls 可以看到，在/usr/lib/jvm目录下有个jdk1.8.0_162目录。

下面继续执行如下命令，设置环境变量：

```bash
cd ~vim ~/.bashrc
```

上面命令使用vim编辑器 打开了hadoop这个用户的环境变量配置文件，请在这个文件的开头位置，添加如下几行内容：

```
export JAVA_HOME=/usr/lib/jvm/jvmFiles/jdk1.8.0_162
export JRE_HOME=${JAVA_HOME}/jre
export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
export PATH=${JAVA_HOME}/bin:$PATH
```

保存.bashrc文件并退出vim编辑器。然后，继续执行如下命令让.bashrc文件的配置立即生效：

```shell
source ~/.bashrc
```

这时，可以使用如下命令查看是否安装成功：

```shell
java -version
```

如果能够在屏幕上返回如下信息，则说明安装成功：

```
hadoop@ubuntu:~$ java -version
java version "1.8.0_162"
Java(TM) SE Runtime Environment (build 1.8.0_162-b12)
Java HotSpot(TM) 64-Bit Server VM (build 25.162-b12, mixed mode)
```

至此，就成功安装了Java环境。下面就可以进入Hadoop的安装。

---

## Hadoop 单机配置(非分布式)

Hadoop安装文件，可以到[Hadoop官网](https://www.apache.org/dyn/closer.cgi/hadoop/common/hadoop-3.1.3/hadoop-3.1.3.tar.gz)下载hadoop-3.1.3.tar.gz。

```shell
cd /usr/local/
sudo mkdir hadoopFiles
sudo tar -zxf hadoop-3.1.3.tar.gz -C ./hadoopFiles     # 解压到/usr/local中
cd hadoopFiles
sudo mv ./hadoop-3.1.3/ ./hadoop            		# 将文件夹名改为hadoop
sudo chown -R hadoop ./hadoop       				# 修改文件权限
```

进入hadoop文件目录 ,查看 hadoop版本 , 判断是否安装成功

```shell
cd /usr/local/hadoopFiles/hadoop
./bin/hadoop version
```

在hadoop文件夹下,使用如下代码 查看hadoop附带的所有例子

```shell
./bin/hadoop jar ./share/hadoop/mapreduce/hadoop-mapreduce-examples-3.1.3.jar
```

---

在hadoop的文件目录下,使用一个小案例,判断hadoop是否能够正常运行

```shell
cd /usr/local/hadoop
mkdir ./input
cp ./etc/hadoop/*.xml ./input   # 将配置文件作为输入文件
./bin/hadoop jar ./share/hadoop/mapreduce/hadoop-mapreduce-examples-3.1.3.jar grep ./input ./output 'dfs[a-z.]+'
cat ./output/*    # 输出:  1      dfsadmin
```

**注意**，Hadoop 默认不会覆盖结果文件，因此再次运行上面实例会提示出错，需要先将 `./output` 删除。

```shell
rm -r ./output
```