---
title: hexo傻瓜一键部署带后台
date: 2021-08-07 20:39:00
categories: lab
tags: [hexo,部署]
urlname: hexo
---
# 1.要求

1.首先，你需要一台电脑，注册有**github**账号，**CloudFlare账号**（访问不了试试用魔法）

2.我猜你们用Windows，所以Linux用户百度同理

3.能全程魔法就用吧，毕竟github这玩意...（部署的站点会用CloudFlare加速，所以不用担心）

# 2.安装



- [node.js](https://cdn.npm.taobao.org/dist/node/v16.6.1/node-v16.6.1-x64.msi "淘宝镜像下载") 管他英语，一直下一步



- [Git](https://cdn.npm.taobao.org/dist/git-for-windows/v2.33.0-rc0.windows.1/Git-2.33.0-rc0-64-bit.exe "淘宝镜像下载") 同上



考虑到百度老有**奇奇怪怪的高速下载器**，这里直接给国内镜像链接（淘宝）

# 3.配置github上传


因为习惯ssh了，这里不介绍https

1.在桌面右键，选择Git Bash Here.

输入命令`git config --global user.name "你用户名"`

输入命令`git config --global user.email "填写你邮箱"`

注意：（引号内请输入你自己设置的名字，和你自己的邮箱）此用户名和邮箱是git提交代码时用来显示你身份和联系方式的，并不是github用户名和邮箱.

2.生成ssh密钥

打开Git Bash Herele输入`sh-keygen -t rsa -C "你的github邮箱"`

然后无脑回车


打开c盘，找到**用户**这个文件夹，在里面进你的用户名命名的文件夹，里面有个`.ssh`文件夹，打开

打开`id_rsa.pub`用记事本打开即可，复制里面的内容

回到github，进入Settings，找到SSH and GPG keys，选择[New SSH Key](https://github.com/settings/keys "怕你找不到")

Title随便填，Key粘贴进去，保存

返回Git命令行，输入`ssh -T git@github.com`

看到Hi xxx! ...证明配置成功

#  4.配置

1.在github创建 `你的用户名.github.io` 仓库 `blog`仓库 `img`仓库

仓库一定要Public（开放的），勾选Add a README file

2.下载[https://cdn.jsdelivr.net/gh/15601560/img@main/blog-main.zip](https://cdn.jsdelivr.net/gh/15601560/img@main/blog-main.zip)


3.打开blog-main压缩包，解压

配置`_config.yml`里面的东西（有中文注释，跟着来）

配置`\blog-main\themes\geek`里的`_config.yml`（一样有注释）

配置`blog-main\.github\workflows`同上

配置`blog-main\themes\geek\layout`index.ejs（logo自己用cloudflareWorkes反代就可以过内，免费额度有限...）

如果懒得搞就和我挤一挤`https://hidden-mountain-d21a.imgblz.workers.dev/get/@index?theme=rule34`

关于页面`blog-main\source\about`

友链`blog-main\source\links`

这里`blog-main\source\CANME`记事本改成绑定的域名

把你的域名`CANME`形式解析到`你的用户名.github.io`

4.打开github找到blog这个仓库（刚才创建的）

点击`Settings`然后点击`secrets`点击 `New Repository secrets`

name填写`HEXO_DEPLOY_PRIVATE_KEY`

Value把前面**生成ssh密钥**里的id_rsa.pub内容复制进去

# 5上传

随便在哪个地方打开Git，输入`git clone 你的blog仓库` 这里不是github.io那个

等完成，打开blog文件夹，把blog-main里的东西全复制到这里面，在这里打开Git

输入`git add .`  （注：别忘记后面的.，此操作是文件夹下面的文件都添加进来）

输入`git commit  -m  "first"`

输入`git push -u origin main`成功后，就不需要了，该删的都删了

# 6.配置后台

基于[HexoPlusPlus](https://hexoplusplus.js.org)

众所周知，Hexo+HexoPlusPlus等于Typecho！！！

跟着里面一把梭https://hexoplusplus.js.org/start/

## 你就拥有了有后台的，白嫖的blog