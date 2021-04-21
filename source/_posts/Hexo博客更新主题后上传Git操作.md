---
title: Hexo博客更新主题后上传Git操作
date: 2019-09-19 18:00:51
toc: true
categories: 博客相关
tags: 
- hexo
- GitHub
---

## 从GitHub上克隆主题(以next主题为例)

在根目录下右键git bush here，输入：

```
git clone https://github.com/iissnan/hexo-theme-next themes/next
```

## 在站点配置文件（_config.yml） 中将主题改为新增主题

```yml
# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
theme: next
```

<!--more-->

## 进入主题目录，更新git

```
cd themes/next
```

```
git pull
```

##  执行更新

```
hexo clean
```

```
hexo g
```

```
hexo s
```

## 测试网址

输入网址 http://localhost:4000 查看主题是否已更新，正常即可输入：

```
hexo d
```

完成部署，然后打开个人域名网址即可。