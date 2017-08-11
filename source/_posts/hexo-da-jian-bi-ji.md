---
title: Hexo 搭建笔记
date: 2017-08-11 07:41:21
tags:
  - DIY
---

## 项目搭建

项目搭建可以参考这篇 limedroid 的[Hexo 博客搭建指南](https://github.com/limedroid/HexoLearning#9-分类给文章归档). 这里对自己遇到的一些问题做一些相应的补充.

## 语言设置

如果你和我一样按照上面的文章配置了 Hexo, 你会发现自己的时间文字显示为德语 "Veröffentlicht am".

这是由于默认配置的语言不符. 首先确认 `theme/next/languages/` 目录下有 `zh-Hans.yml` 文件, 另外我们需要将 `_config.yml` 中配置语言:

```
language: zh-Hans
```

参考:

- [使用Hexo踩坑小记](http://supermaryy.com/2016/07/02/Obstacles_I_Met_When_Using_Hexo/)
