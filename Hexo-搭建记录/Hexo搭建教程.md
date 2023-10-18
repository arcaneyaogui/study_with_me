<a name="GKptA"></a>
### 1.安装 node.js
因为我安装过,但是写教程,我先说说怎么卸载.
C:\Users\admin\AppData\Roaming下手动删除npm和npm-cache文件夹(要以管理员身份删除)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/33584294/1697625571967-2512b205-8718-427f-bee1-d5aaf5877982.png#averageHue=%232f2c27&clientId=ub67b8922-cd3e-4&from=paste&id=ueaed4bb1&originHeight=584&originWidth=918&originalType=url&ratio=1.5&rotation=0&showTitle=false&size=97555&status=done&style=none&taskId=u87aa2067-19d3-46a7-9741-a551754e46c&title=)编辑
我先是将这两个文件删除,并没有那种弹出让我授权管理员,应该不是管理员删除文件,就是正常的删除文件,不知道行不行,先试试.
接下来我卸载了node.js , 现在我们看看是不是卸载了.
反正再查版本是报错蛮,这样就是删除了.
![image.png](https://cdn.nlark.com/yuque/0/2023/png/33584294/1697625571846-60c76e8a-960b-4d62-b29d-8a0c51474979.png#averageHue=%23030201&clientId=ub67b8922-cd3e-4&from=paste&id=u8599159d&originHeight=101&originWidth=795&originalType=url&ratio=1.5&rotation=0&showTitle=false&size=11596&status=done&style=none&taskId=uef71cb79-fbc7-4559-a7b1-dbf417d5985&title=)编辑
**接下来我们来安装node.js**

```html
// 献上node.js官方文档
http://nodejs.cn/learn/how-to-install-nodejs
```
点击下面网址,下载你对应的版本.

```html
http://nodejs.cn/download/
```
安装步骤如下:
![image.png](https://cdn.nlark.com/yuque/0/2023/png/33584294/1697625571843-ddcfb9b3-7c6d-4565-9889-8145382bbdd5.png#averageHue=%23f9f8f8&clientId=ub67b8922-cd3e-4&from=paste&id=uc76e1c21&originHeight=383&originWidth=489&originalType=url&ratio=1.5&rotation=0&showTitle=false&size=26551&status=done&style=none&taskId=uc27d4582-7c74-474b-b923-87cc307cfd3&title=)编辑
![image.png](https://cdn.nlark.com/yuque/0/2023/png/33584294/1697625572252-18fd4848-7ff4-4028-be07-6b063061147e.png#averageHue=%237daf73&clientId=ub67b8922-cd3e-4&from=paste&id=u0a6af148&originHeight=449&originWidth=760&originalType=url&ratio=1.5&rotation=0&showTitle=false&size=279882&status=done&style=none&taskId=u625be7c3-f32e-41ba-87e6-3132196cd5b&title=)编辑
![image.png](https://cdn.nlark.com/yuque/0/2023/png/33584294/1697625572122-354060c0-7349-4cf5-97fd-29ef295f0a88.png#averageHue=%23579551&clientId=ub67b8922-cd3e-4&from=paste&id=ub498f4e1&originHeight=466&originWidth=818&originalType=url&ratio=1.5&rotation=0&showTitle=false&size=341051&status=done&style=none&taskId=ua4365c90-8d59-4d7a-85b0-8ddf4e47168&title=)编辑
用我蹩脚的英语水平,只能马虎翻译翻译下面是个东西是啥.

-  	Node.js 的运行. 	
-  	npm 包的信息 	
-  	在线文档的快捷键 	
-  	添加到环境变量. 	

反正点击next 就对了
![image.png](https://cdn.nlark.com/yuque/0/2023/png/33584294/1697625572804-1f15e392-2ced-4698-8b2b-8e49c961d0f0.png#averageHue=%23edebe9&clientId=ub67b8922-cd3e-4&from=paste&id=ufb29f7d4&originHeight=373&originWidth=495&originalType=url&ratio=1.5&rotation=0&showTitle=false&size=34059&status=done&style=none&taskId=u57272a33-f5e4-41fd-aef8-3db45f0be7d&title=)编辑
翻译:
_自动安装需要的工具,注意,这个也将下载巧克力?(巧克力什么鬼),这个脚本将在完全更新完后弹出一个新窗口._
总结:反正就是不用勾选....直接next
![image.png](https://cdn.nlark.com/yuque/0/2023/png/33584294/1697625573336-2d70695c-c864-4c03-9332-6761c2c5ae6c.png#averageHue=%239dc089&clientId=ub67b8922-cd3e-4&from=paste&id=u6f93a037&originHeight=460&originWidth=663&originalType=url&ratio=1.5&rotation=0&showTitle=false&size=222182&status=done&style=none&taskId=u5aceb626-20ba-46cc-a8ac-ad0e6134a8e&title=)编辑
next 后直接 就finish 安装完成了.我们再看看是否安装完成
莫名奇妙说更新npm,反正没出错,我就更新了一下npm.
![image.png](https://cdn.nlark.com/yuque/0/2023/png/33584294/1697625573716-10d92f5d-0e38-4ac0-9380-ab6f9596313d.png#averageHue=%23121212&clientId=ub67b8922-cd3e-4&from=paste&id=u62200168&originHeight=563&originWidth=851&originalType=url&ratio=1.5&rotation=0&showTitle=false&size=50345&status=done&style=none&taskId=ufa70361f-6203-4032-866c-c84cebd14c2&title=)编辑
能查出这两个的版本号,就是安装好了.
<a name="FJzpx"></a>
### 2.安装Git
**请自行谷歌或者自行参考相关文档.**
<a name="wEida"></a>
### 3.安装hexo
创建一个路径中不包含中文空格得文件,就起名叫MyBlog把.
用git bash here , 在此文件中安装hexo

```html
npm install -g hexo-cli  <!-- 安装hexo -->

hexo -v  <!-- 查看hexo版本 -->
```
**下方为使用git 和 powershell 分别检测安装好node+git+hexo**
网上是说,使用powershell 和 git 都可以进行命令操作,我先选择git进行操作试试.
首先建好一个文件夹,这个文件夹用来放hexo相关东西,这个文件夹路径不要有中文和空格.
![image.png](https://cdn.nlark.com/yuque/0/2023/png/33584294/1697625573714-609f432e-a55f-42ff-b6d7-35e3e7984670.png#averageHue=%23282727&clientId=ub67b8922-cd3e-4&from=paste&id=u9918d613&originHeight=504&originWidth=717&originalType=url&ratio=1.5&rotation=0&showTitle=false&size=40821&status=done&style=none&taskId=u3b0c8d90-a0d2-4af5-9730-4a768482c31&title=)编辑
![image.png](https://cdn.nlark.com/yuque/0/2023/png/33584294/1697625573939-fabde7fa-ac42-4c73-8f31-7131baa7b1b9.png#averageHue=%23012456&clientId=ub67b8922-cd3e-4&from=paste&id=ucbe2188e&originHeight=485&originWidth=829&originalType=url&ratio=1.5&rotation=0&showTitle=false&size=39678&status=done&style=none&taskId=u17142433-0789-46d0-ac14-f3411e476cc&title=)编辑
![image.png](https://cdn.nlark.com/yuque/0/2023/png/33584294/1697625574806-afc9d278-7c3f-4b2f-b5bd-109e17fbeb04.png#averageHue=%23040403&clientId=ub67b8922-cd3e-4&from=paste&id=u72ee201b&originHeight=433&originWidth=882&originalType=url&ratio=1.5&rotation=0&showTitle=false&size=35673&status=done&style=none&taskId=u8750f92b-4c53-4840-b0ac-7408d66bf84&title=)编辑
由于我安装过hexo了,再在另外一个文件夹输入安装命令会如下图.

```html
D:\SoftWare\NodeFiles\node_global\hexo -> D:\SoftWare\NodeFiles\node_global\node_modules\hexo-cli\bin\hexo
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@~2.3.1 (node_modules\hexo-cli\node_modules\chokidar\node_modules\fsevents):
npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@2.3.2: wanted {"os":"darwin","arch":"any"} (current: {"os":"win32","arch":"x64"})

+ hexo-cli@4.2.0
removed 1 package and updated 26 packages in 31.671s
```
我觉得去年安装的hexo版本低了,这里先来卸载一遍.

```html
npm uninstall hexo-cli -g               // hexo卸载命令.
```
卸载后 , 再按照上面安装如下:
![image.png](https://cdn.nlark.com/yuque/0/2023/png/33584294/1697625574809-67eacee3-7cf2-4c49-81b3-b960612627c6.png#averageHue=%23030201&clientId=ub67b8922-cd3e-4&from=paste&id=u908267c7&originHeight=440&originWidth=733&originalType=url&ratio=1.5&rotation=0&showTitle=false&size=40993&status=done&style=none&taskId=u0d1aa9af-192a-46e7-b21a-7baabfe9df1&title=)编辑
但是我有点离谱,和别人教程出来的结果不对,不管是我这git最后出来的结果,还是对比GitHub上的hexo仓库,我都觉得不对劲,但是我又是零基础,没爆那种红,那种错误,我都不知道到底是错了还是没错.
![image.png](https://cdn.nlark.com/yuque/0/2023/png/33584294/1697625575566-a0c97eca-f241-4fc7-8ccd-4349e292129a.png#averageHue=%23252b34&clientId=ub67b8922-cd3e-4&from=paste&id=uda7cb878&originHeight=582&originWidth=1000&originalType=url&ratio=1.5&rotation=0&showTitle=false&size=84404&status=done&style=none&taskId=u674e739e-2aee-4931-8cdc-961ee233c8c&title=)编辑
![image.png](https://cdn.nlark.com/yuque/0/2023/png/33584294/1697625575576-357a3bf2-8741-4855-8d66-5a1aac4f0db9.png#averageHue=%23050201&clientId=ub67b8922-cd3e-4&from=paste&id=u911cbaee&originHeight=592&originWidth=867&originalType=url&ratio=1.5&rotation=0&showTitle=false&size=59739&status=done&style=none&taskId=ue2217bae-9ab6-4321-9519-7042e0b12b5&title=)编辑
为啥我文件会和被人创库里面的文件不一样呢......
先不管,先看看 hexo g 和 hexo s 能不能生成出来博客.
先来试试 hexo g
![image.png](https://cdn.nlark.com/yuque/0/2023/png/33584294/1697625575656-7c0ec3c7-5e2e-455a-aea9-69ebe16a52aa.png#averageHue=%23100705&clientId=ub67b8922-cd3e-4&from=paste&id=u2144d3d1&originHeight=431&originWidth=845&originalType=url&ratio=1.5&rotation=0&showTitle=false&size=78802&status=done&style=none&taskId=u79cb846c-2ba1-45fd-8f64-bdc1f1befaf&title=)编辑
有没有发现运行hexo之后,多出来了一个文件是public , 这个里面就是我们博客页面生成的文件.
![image.png](https://cdn.nlark.com/yuque/0/2023/png/33584294/1697625576091-26251b0f-3f2c-4ac0-a071-a1b3834bf35b.png#averageHue=%230b0201&clientId=ub67b8922-cd3e-4&from=paste&id=u09ec9188&originHeight=72&originWidth=840&originalType=url&ratio=1.5&rotation=0&showTitle=false&size=11012&status=done&style=none&taskId=uf46c8843-869d-46ad-93d3-24e04027255&title=)编辑
接下来看hexo s
![image.png](https://cdn.nlark.com/yuque/0/2023/png/33584294/1697625576182-3a0c1bd7-8443-45ee-8962-344511dc1ecb.png#averageHue=%23110302&clientId=ub67b8922-cd3e-4&from=paste&id=ub2c6e9c9&originHeight=85&originWidth=861&originalType=url&ratio=1.5&rotation=0&showTitle=false&size=11785&status=done&style=none&taskId=ua341bf96-2315-4bdf-9be5-357336faf83&title=)编辑
我们用浏览器,输入 [http://localhost:4000](http://localhost:4000) 看看能不能访问.
![image.png](https://cdn.nlark.com/yuque/0/2023/png/33584294/1697625577020-b5886afa-0689-441a-98d1-08e8a4fc5313.png#averageHue=%23918679&clientId=ub67b8922-cd3e-4&from=paste&id=ub4b72d40&originHeight=1552&originWidth=1074&originalType=url&ratio=1.5&rotation=0&showTitle=false&size=371953&status=done&style=none&taskId=u0e5c7917-e8ab-4ba2-82ff-5e579b91489&title=)编辑
OK,这样你就看到了我们的这个hexo页面是确实能够被推出来的.
<a name="aRjAB"></a>
## 如何写博客?
<a name="NkthN"></a>
### 创建标题,写下内容

```html
// 命令如下,就可以生成一篇文章
hexo new "标题名称"

hexo g 生成
hexok s 推送
```
怎么写文章内容?
我们用vscode打开这个文件夹区域
![image.png](https://cdn.nlark.com/yuque/0/2023/png/33584294/1697625578113-5ca55d24-a52e-4d3d-8f5d-52ca187246e6.png#averageHue=%23292d36&clientId=ub67b8922-cd3e-4&from=paste&id=ua9e498c8&originHeight=1799&originWidth=1067&originalType=url&ratio=1.5&rotation=0&showTitle=false&size=550640&status=done&style=none&taskId=u2ea56f58-6abf-4ac1-8de8-90598ddcb36&title=)编辑
编辑完内容后,保存文件,然后 hexo g >> hexo s 推送出去就可以看见了.
![image.png](https://cdn.nlark.com/yuque/0/2023/png/33584294/1697625577780-9f822f26-5c87-4c66-966b-fe3f83457cf8.png#averageHue=%23e5e4e3&clientId=ub67b8922-cd3e-4&from=paste&id=u1de701c2&originHeight=1374&originWidth=1049&originalType=url&ratio=1.5&rotation=0&showTitle=false&size=176011&status=done&style=none&taskId=ud5dc0e60-5623-48eb-b599-f3e29c314f3&title=)编辑
<a name="xREU5"></a>
### 草稿 和 页面
草稿

```html
hexo new draft  " 草稿名称"
```
注意,创建草稿页面,使用hexo g 的时候是不会被生成的.
纯粹页面

```html
hexo new page  "页面名称"
```
然后页面管理的文件夹是 scaffolds
![image.png](https://cdn.nlark.com/yuque/0/2023/png/33584294/1697625577700-673ec335-5004-4581-89eb-0c60882c29d8.png#averageHue=%23262b33&clientId=ub67b8922-cd3e-4&from=paste&id=u76768be8&originHeight=475&originWidth=223&originalType=url&ratio=1.5&rotation=0&showTitle=false&size=17655&status=done&style=none&taskId=u4c8c99ec-eb74-4fef-a995-63e68a1421d&title=)编辑
我们也可以自己创建页面等等,但是由于笔者也是水平有限,只能教基础. 搭建零基础根本不是问题,学就完了,如果你爱折腾,可以不厌其烦的百度,谷歌搜索不同答案,不断验证,错几遍也就会了.
<a name="mMk5Y"></a>
## 创建GitHub仓库
创建一个GitHub仓库,仓库名字需要和自己名字一样 , 后面 + .github.io

```html
举个例子
比如你的github用户名叫 zhagnsan
那么你的那个仓库名字就是 zhangsan.github.io
```
<a name="B9nkU"></a>
### git 绑定 GitHub

```html
git config --global user.name "你的GitHub用户名"
git config --global user.email "你的GitHub注册邮箱"
ssh-keygen -t rsa -C "你的GitHub注册邮箱"

分别输入完上面三个代命令后,直接三个回车就行.
```
然后我们看这个新生成了这个文件,右键记事本打开,复制里面内容.
![image.png](https://cdn.nlark.com/yuque/0/2023/png/33584294/1697625577709-2c8aa70b-c03e-4de0-9358-1e2069991906.png#averageHue=%23222121&clientId=ub67b8922-cd3e-4&from=paste&id=uee06189f&originHeight=289&originWidth=947&originalType=url&ratio=1.5&rotation=0&showTitle=false&size=18487&status=done&style=none&taskId=ude4af5a0-8e34-43a4-b0af-feb697090a1&title=)编辑
然后我们再GitHub上面新建 SSH Keys
![image.png](https://cdn.nlark.com/yuque/0/2023/png/33584294/1697625578676-14a29a62-38e5-4f86-bfbf-92629e489019.png#averageHue=%23242931&clientId=ub67b8922-cd3e-4&from=paste&id=u3f5d6b37&originHeight=1098&originWidth=1066&originalType=url&ratio=1.5&rotation=0&showTitle=false&size=110354&status=done&style=none&taskId=u69663404-2d59-42a3-849a-0f12141bc82&title=)编辑
然后把那一堆东西复制到这个key下面.标题是按照你喜好自己取名.点击add ssh key.
![image.png](https://cdn.nlark.com/yuque/0/2023/png/33584294/1697625578807-d8318242-4c85-4a88-8808-e34f573d462f.png#averageHue=%2395daa5&clientId=ub67b8922-cd3e-4&from=paste&id=u7eeb5a8b&originHeight=346&originWidth=677&originalType=url&ratio=1.5&rotation=0&showTitle=false&size=46341&status=done&style=none&taskId=u1ddf5c53-0629-46e5-aeaa-cdd92550c0e&title=)编辑
然后你就可以看见这个样子的了.
![image.png](https://cdn.nlark.com/yuque/0/2023/png/33584294/1697625578958-ebb9dabc-6087-43c8-b516-f23bf7e2221a.png#averageHue=%23252b32&clientId=ub67b8922-cd3e-4&from=paste&id=uaef24615&originHeight=292&originWidth=804&originalType=url&ratio=1.5&rotation=0&showTitle=false&size=29989&status=done&style=none&taskId=uee6912d2-b2a3-4ac5-8c4c-aab8b2c6c78&title=)编辑
**注意,如果你也是跟我一样之前弄过但是失败了,并且现在还换了一个GitHub账号,那么你需要把 .ssh文件夹中的文件删除干净,然后再按照上面的步骤来一遍,就可以了.**
<a name="Yoofe"></a>
### 推送网站
这个是我们的**站点配置文件**
主题中有个名字和这个一样的文件,称为**主题配置文件**
![image.png](https://cdn.nlark.com/yuque/0/2023/png/33584294/1697625579301-df9f64a3-6222-4f35-9f5f-2b22f8dd2634.png#averageHue=%23292625&clientId=ub67b8922-cd3e-4&from=paste&id=u2dc4f32d&originHeight=319&originWidth=856&originalType=url&ratio=1.5&rotation=0&showTitle=false&size=36753&status=done&style=none&taskId=uaa1eb3f9-c85a-4f85-bdf4-f84524afe84&title=)编辑
我们用vscode打开这个文件,直接到最下面去.
![image.png](https://cdn.nlark.com/yuque/0/2023/png/33584294/1697625580531-5e2a7d59-ed9f-45a3-a268-875acd64f7b7.png#averageHue=%23292d36&clientId=ub67b8922-cd3e-4&from=paste&id=u4ca2605c&originHeight=1772&originWidth=1026&originalType=url&ratio=1.5&rotation=0&showTitle=false&size=262859&status=done&style=none&taskId=u5714e6da-6400-43c2-9e30-2cd959cf658&title=)编辑
修改成我这个样子的,然后**保存.**

```html
deploy: 
  type: git
  repo: https://github.com/你自己GitHub名称/你自己GitHub名称.github.io.git
  branch: main
```
接下来我们写几条命令,把它推送到GitHub的创库的上面去.
告知的你hexo你要把博客部署到那个地方.

```html
npm install hexo-deployer-git --save
```
每次更新推文时都得写这个东西.

```html
hexo clean     // 用来清除缓存文件,和以生成的静态文件.

hexo g       // 生成博客的指令

hexo d       // d 表示 depoly[配置,部署的意思]
```
![image.png](https://cdn.nlark.com/yuque/0/2023/gif/33584294/1697625580265-b5f630f8-aa59-49ad-986c-d1e1584512e5.gif#averageHue=%23ffffff&clientId=ub67b8922-cd3e-4&from=paste&id=u9bf8eb6e&originHeight=1&originWidth=1&originalType=url&ratio=1.5&rotation=0&showTitle=false&size=43&status=done&style=none&taskId=ua7b6d6e4-4922-4529-a5dd-48df7c28773&title=)
然后接下来你可以访问你GitHub的网址进行访问你的博客了.

```html
你自己GitHub名称.github.io    //直接就可以访问
```
![image.png](https://cdn.nlark.com/yuque/0/2023/gif/33584294/1697625580385-9414d218-d2d2-4b19-93ad-932cb0f4d926.gif#averageHue=%23ffffff&clientId=ub67b8922-cd3e-4&from=paste&id=u07046c1a&originHeight=1&originWidth=1&originalType=url&ratio=1.5&rotation=0&showTitle=false&size=43&status=done&style=none&taskId=u2834004e-0196-4cb8-b5ff-2a73183f5e0&title=)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/33584294/1697625580931-68921763-2c68-47d2-a808-4b28e76bbe64.png#averageHue=%23d9d8d7&clientId=ub67b8922-cd3e-4&from=paste&id=uc8d0c8a2&originHeight=1488&originWidth=1071&originalType=url&ratio=1.5&rotation=0&showTitle=false&size=434828&status=done&style=none&taskId=u1d5d2079-dee2-452f-b4bf-4ed93872d37&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/gif/33584294/1697625580560-5cb36265-ba85-4fcc-a7cc-fc418c70f8aa.gif#averageHue=%23ffffff&clientId=ub67b8922-cd3e-4&from=paste&id=u03967047&originHeight=1&originWidth=1&originalType=url&ratio=1.5&rotation=0&showTitle=false&size=43&status=done&style=none&taskId=u44b89291-eb2c-4c34-95ef-acd0735c867&title=)编辑
<a name="EO4rU"></a>
### 尾声
 	

-  	基本的框架就这样搭起来了 	 		
   -  		你可以换自己喜欢的主题. 		
-  		
   -  		你甚至可以自己写页面部署上去. 		
-  		
   -  		你可以买自己域名绑定. 		
-  		
   -  		当然也可以搭建再自己买的服务器上. 		
-  	 	

```html
https://hexo.io/zh-cn/docs/        // hexo文档.
```
![image.png](https://cdn.nlark.com/yuque/0/2023/gif/33584294/1697625580984-be6f1368-ec1f-4cb9-9211-de2018c177f4.gif#averageHue=%23ffffff&clientId=ub67b8922-cd3e-4&from=paste&id=u42749d06&originHeight=1&originWidth=1&originalType=url&ratio=1.5&rotation=0&showTitle=false&size=43&status=done&style=none&taskId=uf417c6ff-7d25-4287-b558-10a369ecb51&title=)
