---
title: 关于
layout: about
date: 2021-01-01 00:00:00
updated: 2022-12-12 18:00:00
---

<img src="..\C.png" style="zoom:75%;" />

如你所见，[本博客](https://blog.iscccc.eu.org)的博主。一个~~训练有素的~~学生。

兴趣使然

---

**哔哩哔哩:[这里](https://space.bilibili.com/379876445)**

**网易云音乐:[这里](https://music.163.com/#/user/home?id=1514730143)**

~~**MCBBS:[这里](https://www.mcbbs.net/home.php?mod=space&uid=2839905)**~~

**Steam:[这里](https://steamcommunity.com/id/Cccc_owo/)**

*//Steam社区打不开看[这篇文章](https://blog.iscccc.eu.org/posts/c47e0b89/)*

---

感谢你的到来

## 站点日志

### 2022-08-16

新域名：<https://blog.iscccc.eu.org/>

### 2022-02-07

将博客主题自[Volantis](https://github.com/volantis-x/hexo-theme-volantis)迁移至[Yun](https://github.com/YunYouJun/hexo-theme-yun)

### 2022-02-05

将博客主题自[Yun](https://github.com/YunYouJun/hexo-theme-yun)迁移至[Volantis](https://github.com/volantis-x/hexo-theme-volantis)

### 2021-10-02

将博客主题自[Next](https://github.com/next-theme/hexo-theme-next)迁移至[yun](https://github.com/YunYouJun/hexo-theme-yun)

### 2021-09-21

更新了文章访问计数(虽然我觉得有点晚了

### 2021-09-20

目前使用[Vercel](https://vercel.com/dashboard)配置，简单快捷。

注:同时已开放了评论，大概

结果我还是个善变的人（

关于评论区:

本博客评论区使用[utterances](https://github.com/utterance/utterances),由[Github Issues](https://github.com/Cccc-owo/blog-related)强力驱动。

发表评论需登录Github账号，另外在中华地区加载速度可能比较慢，见谅

### 2021-08-12

再次换回Github Actions进行博客部署，原因是Travis的免费计划有构建10000次的次数限制。

虽然Travis免费计划额度很大，但Github Actions有方便的[部署部件](https://github.com/marketplace?type=actions)且无花费，经过一番研究，我决定还是横跳回Github Actions。

这是~~目前的~~workflow配置，可供参考:

```yml
## This is a basic workflow to help you get started with Actions

name: pages

## Controls when the workflow will run
on:
  ## Triggers the workflow on push or pull request events but only for the main branch
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

  ## Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

## A workflow run is made up of one or more jobs that can run sequentially or in parallel
jobs:
  ## This workflow contains a single job called "build"
  build:
    ## The type of runner that the job will run on
    runs-on: ubuntu-latest

    ## Steps represent a sequence of tasks that will be executed as part of the job
    steps:
      ## Checks-out your repository under $GITHUB_WORKSPACE, so your job can access it
      - uses: actions/checkout@v2.3.4
      - uses: actions/cache@v2.1.6
        with:
          path: node_modules
          key: ${{ runner.OS }}-npm-cache
          restore-keys: |
            ${{ runner.OS }}-npm-cache
      - name: Setup Node.js environment
        uses: actions/setup-node@v2.4.0
      - name: Install Dependencies
        run: npm install      
      - name: Build
        run: npm run build
      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3.8.0
        with:
          github_token: ${{ secrets.GH_TOKEN }}
          publish_dir: ./public
          publish_branch: gh-pages  ## deploying branch
```

### 2021-05-30

#### 起因

我的电脑系统重装，忘记备份ssh密钥了，只好重新生成并顺手删除了以前的密钥。因此依赖于以前密钥的仓库Secret失效了。

我又忘记当时是怎么配置workflow的，所以想要更新博客时又构建失败了。

百度一番解决方法，找到了以前想用但没采用的Travis

#### 经过

参考[Hexo文档](https://hexo.io/zh-cn/docs/github-pages)稍作修改。

~~仓库[travis.yml](https://github.com/Cccc-owo/myBlog/blob/main/.travis.yml)~~

``` yml
sudo: false
language: node_js
node_js:
  - 14.17.0
cache: npm
branches:
  only:
    - main ## build master branch only
script:
  - hexo generate ## generate static files
deploy:
  provider: pages
  skip-cleanup: true
  github-token: $GH_TOKEN
  keep-history: true
  on:
    branch: main
  local-dir: public
```

#### 结果

昨天把博客的构建从Github Actions换到了Travis。目前体验良好。

**教训：不要忘记备份！**

更新：记得要选择Travis的免费计划，否则会无法构建
