[![npm version](https://badge.fury.io/js/hexo-recommended-posts.svg)](https://badge.fury.io/js/hexo-recommended-posts)

[中文](README.md) | [English](README-en.md)
# 致谢
首先，我想感谢，未曾谋面的朋友们，对此插件的贡献，谢谢他们极具建设性的意见和快速的测试反馈
- [reuixiy](https://reuixiy.github.io/)
- [sd44](http://sd44.github.io/)

# 已支持主题
- [hexo-theme-freemind](https://github.com/wzpan/hexo-theme-freemind)

# Hexo跨博客文章推荐插件
本插件帮助大家跨博客推荐彼此文章，为博客找到更多读者。更多动机请看[开发笔记](https://hui-wang.info/2017/12/22/%E5%AE%89%E5%8F%AF%E6%8E%A8%E8%8D%90%E7%B3%BB%E7%BB%9F%E5%BC%80%E5%8F%91%E7%AC%94%E8%AE%B0%EF%BC%881%EF%BC%89/)。

# 工作原理
插件从[推荐服务器](https://github.com/huiwang/encore)里获取文章推荐列表。列表中，一部分为博客内链（指向您自己的博客），一部分为外链（指向其他博主的文章）。所有链接均为静态生成，不需额外添加Javascript代码，有利于增加网站的搜索排名。基于互利互惠的合作思想，使用该插件的博主越多，文章被其他博主推荐的机会就越大。

在安装使用之前，您可以[实时预览](https://hui-wang.info)该插件的效果。

# 如何使用
## 1. 安装文章推荐插件：

```
npm install hexo-recommended-posts --save
```
## 2. 配置插件

在博客根目录的`_config.yml`里添加插件配置：
```
recommended_posts:
  server: https://api.truelaurel.com #后端推荐服务器地址
  timeoutInMillis: 5000 #服务时长，超过此时长，则使用离线推荐模式
  internalLinks: 3 #内部文章数量
  externalLinks: 1 #外部文章数量
```

## 3. 下载推荐文章列表

在编辑完新的文章之后，使用如下命令获取推荐列表
```
hexo recommend
```
## 4. 显示推荐文章

插件提供两个途径显示推荐文章，您可按需挑选
- 通过在文章Markdown里插入`tag`操作单一文章
- 通过修改主题，使用`helper`覆盖博客所有文章

### 4.1. 手动添加Tag

在文章Markdown的合适位置插入`{% recommended_posts %}`标签， 比如
```
---
title: Hello World
date: 2017-12-21 20:21:52
tags: [hello, world]
---
文章正文
# 推荐文章
{% recommended_posts %}
```

### 4.2. 配置主题

Hexo有两个比较流行的渲染器：
- EJS ：请参看[hexo-theme-freemind](https://github.com/wzpan/hexo-theme-freemind/pull/77/files)的配置
- SWIG：请参看[hexo-next-them](https://github.com/iissnan/hexo-theme-next/pull/2054/files)的配置

如果您是主题的维护者，请在配置完毕之后联系我，我会把您的主题加入到支持该插件的列表中。

## 5. 生成博客

下载完列表之后，生成博客，推荐文章将会按照主题的配置加入到相应的页面
```
hexo generate
```

# 常见问题
- 当无法连接推荐服务器时，插件如何工作？

当服务器无法使用时，对旧文章，插件会使用原有的推荐列表；对新文章，将使用离线推荐算法推荐内部文章。
