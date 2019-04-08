---
layout: post
title: Ubuntu Dev.Guide
category: 资源
tags: 工具
keywords: 资源,工具,Ubunt
published: true
---

# Ubuntu Dev.Guide

> 抛弃了 Windows 后，就一直使用 Ubuntu 系统，重装了 N 次了，这里还是需要写一篇总结。

## 重装后

装完系统后，配置一下自己的工作环境.

- 安装 Google Chrome
- 安装 [SSR](https://github.com/shadowsocks/shadowsocks-qt5) 客户端
- node.js, 国内切换淘宝源。
- WPS，Linux 下的 WPS
- [Jekyll on Ubuntu](https://jekyllrb.com/docs/installation/ubuntu/)
- PicGo, 使用 GitHub 做图床
- Shutter, 截图工具，有其他好用的截图工具，希望看到的小伙伴留言告诉一下。
-
- 安装 [Slack](https://get.slack.help/hc/en-us/articles/212924728-Download-Slack-for-Linux-beta)、[Telegram]()

## 配置

### git 配置

```bash
$ ssh-keygen
$ sudo apt install git
# 生成公钥
$ ssh-keygen
# 测试是否连接成功，成功会有　successfully。
$ ssh -T git@github.com
# 配置　git 文件
$ git config --global user.name "AlvinMi"
$ git config --global user.email "alvin.mi0620@gmail.com"
```

### 配置 Python 环境

推荐使用 Anaconda 安装，包比较完善！使用虚拟环境开发。

### 配置 VSCode

- 1.安装 `setting sync` 插件，同步自己的 vscode 插件和配置.
- 2.同步插件，需要 [github token](https://github.com/settings/tokens)，gist id `289dd0d76ca746fc9dedb9f530569ffd` 就可以了，这个 id 是我自己本地的配置。

### Ruby 环境

最终更新 - by 2019-03-19...