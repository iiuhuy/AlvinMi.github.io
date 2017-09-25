---
title: Hexo+GitHub Pages 分支搭建博客避免电脑重装
date: 2017-09-25 20:05:04
tags:
---

# 01 简介
这是几个月之前使用 Hexo + GitHub Pages 搭建打个人博客。 这篇还是需要总结一下的, 个人搭建起来时总的来说不算太难, 但确实会遇到很多坑, 毕竟前端的东西接触少, 也只是业余才接触。 

个人还是喜欢总结一些东西在自己的博客上, 避免时间久了就忘了。 但是之前搭建的时候总是想不到应该如何避免电脑重装或者在其他电脑上更新自己的博客内容。 

直到后来参考了网上的例程: 总的来说可以完美的避免这样的问题, 值得借鉴！ 参考链接请看文末。

# 02 首先需要了解的

* [Git](https://git-scm.com/book/zh/v2)
* [GitHub Pages](https://pages.github.com/)
* [Hexo](https://hexo.io/zh-cn/)
* [Markdown 语法规则]()

Git 就不多解释, 懂的人自然会懂。 

Github Pages 是面向用户、组织和项目开放的公共静态页面搭建托管服务，站点可以被免费托管在Github 上，你可以选择使用Github Pages 默认提供的域名github.io 或者自定义域名来发布站点。

Hexo 即一个开源的博客框架, 而 GitHub 开源的博客框架是 Jekyll (这个框架好像国外的朋友都喜欢用)。 至于你用哪个看你自己的选择了。 百度、谷歌一搜就知道了。

Markdown 这个基本的语法基本需要熟悉, 会的就不说了, 不会的也很简单，找篇语法介绍的教程跟着写几遍就熟了。 熟悉了之后保证你肯定会爱上它。

# 03 开始搭建
总的来讲我觉得可以分为三步走。 (其实也就两步走)

* 首先创建仓库, 仓库里面分别是两个分支 master 和 hexo（这个你自己随意命名）后面就直接两步记录完成！
* 在本地把 Hexo + GitHub Pages 的博客搭建起来, 并部署到 master 分支上。(其实这个时候你的博客已经搭建起来了, 可以自己发布博文什么的了)
* 这个分支的目的就是 **备份源文件** 的目的, 也是我之前不知道怎么备份源文件的一种方式。也能在其他电脑上修改博文, 再发布； 更避免了电脑重装系统后源文件丢失的情况。 否则就得重新搭建了！ 我也忘记自己重新搭建了多少次了。 就觉得这个方法还不错。 当然也有人把源文件备份到私有仓库(例如 coding 上可以免费创建 2 个私有仓库。) 方法自行百度、谷歌吧！ 小小白有的坑肯定还是需要踩的。

## 3.1 如果没有搭建起来博客
这一步可以搜索 Hexo + GitHub Pages 搭建博客！ 如果你已经搭建完成并部署了, 那么直接跳过查看 3.2 即可！

那么可以参考文末的链接搭建。说简单来讲就是相关环境的配置安装。部署到 GitHub 仓库就搭建好了。

部署优化就是使用 **分支** 或者 **远程仓库** 来备份本地源文件。 就算系统重装后也只需要简单的几步就好。

主要参考 [crazymilk.github.io](https://crazymilk.github.io/2015/12/28/GitHub-Pages-Hexo%E6%90%AD%E5%BB%BA%E5%8D%9A%E5%AE%A2/).

搭建步骤如下

* 在自己的GitHub账号下创建一个新的仓库，命名为username.github.io（username是你的账号名)。
* 安装 Git！ [Git 官网下载](https://git-scm.com/downloads) 然后进行相关的配置(配置查看参考链接, 这里不提了。)
* 安装 Hexo. 安装 Hexo 需要下载安装 [node.js 环境](https://nodejs.org/en/download/) 选择自己电脑匹配的版本安装。
* 然后在本地建站, 参考链接也就几步！ 
* 本地建站完成后需要部署到 GitHub Pages(主题也包含)，如果当你的博客能通过你的 username.github.io 在网上访问的时候, 你的博客已经搭建完成。 后面将本地源文件备份一下就好。


## 3.2 本地源文件备份到分支

搭建好博客后, 根据 [crazymilk.github.io](https://crazymilk.github.io/2015/12/28/GitHub-Pages-Hexo%E6%90%AD%E5%BB%BA%E5%8D%9A%E5%AE%A2/) 博客的搭建流程, 这里作为小白的我, 也许是踩到坑了。 这里进行说明一下！

### 3.2.1 首先看看流程

1. 创建仓库，Username.github.io；
2. 创建两个分支：master 与 hexo； 上面部署的时候用到了 master 分支
3. 设置hexo为默认分支（因为我们只需要手动管理这个分支上的Hexo网站文件)；	
4. 使用git clone git@github.com:CrazyMilk/CrazyMilk.github.io.git拷贝仓库； 这里其实不用拷贝，直接就用你本地的源文件进行操作。 如果不放心, 先把整个博客源文件做一个备份在进行操作。 当然也省去了第 5 步的操作, 因为你只需要用到 hexo 分支上的 .git 文件。把它克隆下来放到 Username.github.io 文件目录下即可 (这样当前的分支才是 hexo) 如果不是, 需要设置 hexo 为默认分支或者使用 `git checkout origin hexo`。
5. 在本地CrazyMilk.github.io文件夹下通过Git bash依次执行npm install hexo、hexo init、npm install 和 npm install hexo-deployer-git（此时当前分支应显示为hexo）;
6. 修改博客目录_config.yml中的deploy参数，分支应为master；
7. 依次执行git add .、git commit -m “…”、git push origin hexo提交网站相关的文件；
8. 执行hexo generate -d生成网站并部署到GitHub上。

这样一来就完成了，在 GitHub 上的 Username.github.io 仓库就有两个分支，一个 hexo 分支用来存放网站的原始文件，一个 master 分支用来存放生成的静态网页。 确实完美( •̀ ω •́ )y biu~~！

> 或者你觉得多了个 .deploy_git 文件夹, 其实不影响！对比一下 GitHub 里面的文件就能发现！


# 04 博客管理流程

## 4.1 日常修改

在本地对博客进行修改（添加新博文、修改样式等等一样可以支持 hexo 的相关操作）后，通过下面的流程进行管理

1. 依次执行 `git add .`、`git commit -m “…”`、`git push origin hexo` 指令将改动推送到GitHub 仓库(此时当前分支应为hexo)；
2. 然后执行 `hexo generate -d` 就能发布网站到 master 分支上。

两个过程顺序调转一般不会有问题，不过逻辑上这样的顺序是绝对没问题的（例如突然死机要重装了，悲催….的情况，调转顺序就有问题了）。这个还没遇到过。

## 4.2 本地资料丢失
当重装电脑之后，或者想在其他电脑上修改博客，可以使用下列步骤

1. 使用 `git clone git@github.com:Username/Username.github.io.git` 拷贝仓库（默认分支为 hexo )；
2. 在本地新拷贝的 Username.github.io 文件夹下通过 Git bash 依次执行下列指令：`npm install hexo`、 `npm install`、`npm install hexo-deployer-git`（记得，不需要 hexo init 这条指令）。

> 结尾

> 主要参考就是 CrazyMilk 的这篇教程。
> [crazymilk.github.io](https://crazymilk.github.io/2015/12/28/GitHub-Pages-Hexo%E6%90%AD%E5%BB%BA%E5%8D%9A%E5%AE%A2/) 省去了搭建过程的详细步骤，如果详细写下来就太多了。 所以还是讲讲如何采坑比较好。


