<a name="O0awv"></a>
# 新电脑环境
<a name="yBxaK"></a>
## powershell禁止脚本执行
PowerShell 输入  get-executionpolicy 可查看脚本的执行策略。
**设置powershell为可执行脚本模式。**
```
set-executionpolicy remotesigned 
```
<a name="FVado"></a>
## nvm解决项目npm下载报错问题
[使用NVM轻松安装并管理多版本Node.js - 雨月空间站](https://www.mintimate.cn/2021/07/26/nvmNode/)

nvm不同系统版本下载地址：

- For Mac/Linux：[https://github.com/nvm-sh/nvm](https://github.com/nvm-sh/nvm)
- For Windows：[https://github.com/coreybutler/nvm-windows](https://github.com/coreybutler/nvm-windows)

如果电脑上有node，先使用geek卸载掉node。
然后删除自己配置的node路径文件夹，检查一下路径看看是否还有node或者npm文件夹。
```javascript
C:\Program Files (x86)\Nodejs
C:\Program Files\Nodejs
C:\Users{User}\AppData\Roaming\npm（或%appdata%\npm）
C:\Users{User}\AppData\Roaming\npm-cache（或%appdata%\npm-cache）
```

将之前设置过的Node环境（系统环境和用户环境）里的Node路径全部删除。
检查node和npm，在cmd中输入node-v、npm-v
重启系统。

NVM_HOME：NVM地址目录，比如：D:\myEnvironment\nvm
NVM_SYMLINK：NVM配置Node.js的软链接，该目录需指向并不存在的目录（NVM使用时候会自动创建），比如：D:\myEnvironment\nodejs

在系统环境变量中配置两个变量。
![image.png](https://cdn.nlark.com/yuque/0/2023/png/33584294/1679981993758-77f64d7e-024a-4620-be2c-dd58eb85b121.png#averageHue=%23f4f1f0&clientId=u5259b6bb-16bf-4&from=paste&height=87&id=uac1a6ac6&originHeight=45&originWidth=501&originalType=binary&ratio=1&rotation=0&showTitle=false&size=3108&status=done&style=none&taskId=u38018ede-3166-419b-95b6-a53df943d4d&title=&width=970)

追加内容到Path，追加的内容：
%NVM_HOME%
%NVM_SYMLINK%

然后 nvm version  显示版本号,表示安装成功.
在路径中创建settings.txt文件,有的话就不用创建,修改内容如下.
```javascript
root: D:\Environment\nvm
path: D:\Environment\nodejs
arch: 64
proxy: none
node_mirror: https://npm.taobao.org/mirrors/node/
npm_mirror: https://npm.taobao.org/mirrors/npm/
```

nvm list -- 查看安装的 node 版本
nvm list available -- 查看所有的node版本
nvm install [ndoe版本号]
![image.png](https://cdn.nlark.com/yuque/0/2023/png/33584294/1679982731146-83ab3155-80e5-42d2-9691-4d410fe9df62.png#averageHue=%23131313&clientId=u5259b6bb-16bf-4&from=paste&height=404&id=uff3809dd&originHeight=248&originWidth=599&originalType=binary&ratio=1&rotation=0&showTitle=false&size=7512&status=done&style=none&taskId=u48794840-4486-49c5-a2b8-31627c18d15&title=&width=975)

```
#使用该node版本
nvm use 12.22.3  
```


<a name="BcKz8"></a>
## 关于npm包报错问题
这个问题他妈的很烦，最后我就是换成npm官方源
```shell
npm ERR! code ENOTFOUND
npm ERR! errno ENOTFOUND
npm ERR! network request to http://registry.cnpmjs.org/qs failed, reason: getaddrinfo ENOTFOUND registry.cnpmjs.org
npm ERR! network This is a problem related to network connectivity.npm ERR! network In most cases you are behind a proxy or have bad network settings.
npm ERR! network
npm ERR! network If you are behind a proxy, please make sure that the
npm ERR! network 'proxy' config is set properly.  See: 'npm help config'

npm ERR! A complete log of this run can be found in:
npm ERR!     D:\SoftWare\NodeFiles\node_cache\_logs\2023-03-29T04_11_44_585Z-debug.log
PS D:\Codes\work\vue-test\vue-test> npm i qs -S 
npm ERR! code ENOTFOUND
npm ERR! errno ENOTFOUND
npm ERR! network request to http://registry.cnpmjs.org/qs failed, reason: getaddrinfo ENOTFOUND registry.cnpmjs.org
npm ERR! network This is a problem related to network connectivity.
npm ERR! network In most cases you are behind a proxy or have bad network settings.
npm ERR! network 
npm ERR! network If you are behind a proxy, please make sure that the
npm ERR! network 'proxy' config is set properly.  See: 'npm help config'

npm ERR! A complete log of this run can be found in:
npm ERR!     D:\SoftWare\NodeFiles\node_cache\_logs\2023-03-29T04_12_13_313Z-debug.log
```

**npm config set registry http://registry.npmjs.org/**

**有时候真不知道网上那些换淘宝源什么的是怎么回事，他妈的。
反正我nvm设置的npm的淘宝源，但是我又用这个命令设置了官方源，搞不懂....**

<a name="o2HI3"></a>
## 
<a name="Y9WYc"></a>
# 
