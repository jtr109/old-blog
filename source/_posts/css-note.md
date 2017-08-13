---
title: css 学习笔记
date: 2017-08-13 12:30:45
tags:
  - css
---

## 居中

### 1. 文字居中

- 水平居中: `text-align: center`
- 垂直居中: `vertical-align: middle`

### 2. div 居中

_div 居中是一个比较坑的实现, 没有什么特别优秀的办法, 这里只举部分较实用的例子._

具体方法可以参考[知乎上的这一篇回答](https://zhihu.com/question/20543196/answer/89218605), 这里暂时只介绍其中 absolute 的使用.

#### 2.1 absolute 居中

```css
// 假设我们要做一个 200px 见方的 div
.middle {
  position: absolute;
  width: 200px;
  height: 200px;
  top: 50%;
  left: 50%;
  margin-top: -100px; 
  margin-left: -100px;
  background: red;
}
```

这是一个比较稳妥的实现, 这里很明显, 是通过 `top: 50%` 来实现的垂直居中, 不过如果单单使用 `top=50%`, 会发现 div 的顶部位于父级元素 50% 位置处, 所以需要使用 `margin-top=-100px` 来实现元素的便宜. 该示例中的水平居中方法同理.

如果在确认设置无误的情况下, 发现 div 的位置不对, 请检查父级是否正确设置了 `position: relative`.
