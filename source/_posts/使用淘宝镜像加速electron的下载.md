title: 使用淘宝镜像加速electron的下载
author: strongant
tags:
  - electron
categories: []
date: 2017-10-29 23:07:00
---
目前github开源的electron库被好多桌面端应用广泛使用，有时候我们安装这类应用时特别慢，原因就是卡在了下载electron压缩包这个阶段，速度奇慢。为了不浪费我们宝贵的时间，使用下面的脚本可以帮助你分分钟下载成功electron，感谢淘宝npm镜像。

```bash
export ELECTRON_MIRROR="https://npm.taobao.org/mirrors/electron/"
```