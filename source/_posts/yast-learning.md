---
title: Yet Another Scheme Tutorial 学习笔记
date: 2017-08-23 07:30:11
tags:
  - Scheme
  - LISP
  - SICP
---

## 算数操作

### 基本算数操作

- 函数 `exact->inexact` 用于把分数转换为浮点数.
- 函数 `quotient` 用于求商数（quotient）。
- 函数 `remainder` 和 `modulo` 用于求余数（remainder）。
- 函数 `sqrt` 用于求参数的平方根（square root）。

```LISP
(exact->inexact (/ 29 3 7))  ;-> 1.380952380952381
(quotient 7 3)  ;→ 2
(modulo 7 3)  ;→ 1
(sqrt 8)  ;→ 2.8284271247461903
```

### 练习

练习中发现, 如果创建 scm 文件并写入多个算式, 好像不能得出每个计算的值, 得到的只能是最后一个算式的结果.

## 表

### 空表

`'()` 即为空表

有两种非常类似的 value, 实现的方式却是不同的:

- `(3 2 . 1)`:
  ![`(3 2 .1)`](http://www.shido.info/lisp/conss2.png)
- `(1 2 3)`:
  ![`(1 2 3)`](http://www.shido.info/lisp/list2.png)

其实主要的差异是最后一个 cons 的 cdr 指向地址的不同, 上面一个是指向 1 所在的地址, 最后一个是指向一个空表 `'()`

这里指出一下[中文版](https://deathking.github.io/yast-cn/contents/chapter3.html)的图片有误, 请参照[原版](http://www.shido.info/lisp/scheme3_e.html)

## 引用

`'()`这里的空表就是使用了引用(quote)

## list 函数

特别值得注意的是, list 函数返回的是其中的元素构成的表, 函数中的每个参数都是表的一个元素:

```Scheme
(list '(1 2) '(3 4))
;Value 1: ((1 2) (3 4))

(cons '(1 2) '(3 4))
;Value 2: ((1 2) 3 4)
```
