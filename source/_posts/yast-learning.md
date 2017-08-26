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

## 字符串操作

- `string-append`: 字符串拼接

## 函数定义

### 定义变量

```Scheme
(define vhello "Hello world!")
```

### 定义函数

定义函数有两种方式, 一个是 lambda 一个是简写, 暂时不清楚两者的实际区别.

```Scheme
;;; 定义不带参数的函数

; lambda 定义
(define hello
  (lambda ()
    "Hello world!"))

; 简写
; (define (hello)
;  ("Hello world!"))
; 不成立

;;; 定义带参数的函数

; lambda
(define hello
  (lambda (name)
    (string-append "Hello " name "!")))

; 简写
(define (hello name)
  (string-append "Hello " name "!"))

```

## if 判断

### true and false

在 LISP 中 true 用 `#t` 表示, false 用 `#f` 表示.

### 关于空表的判断

由于 R4RS 和 R5RS 对空表 `'()` 是否为 false (`#f`) 的标准不同, 所以判断表为空应使用 `null?`:

```Scheme
(null? '())
;Value: #t
```

### 数字判断

- `positive?`: 判断正数
- `zero?`: 是否为 0
- `negative?`: 判断负数

### 原生函数

- `integer->char`: 正数转化为 ascii 码

## and 和 or

Scheme 中的 and 和 or 相对 C 类语言来说十分特殊:

> `and` 具有任意个数的参数，并从左到右对它们求值。
> 如果某一参数为 `#f`，那么它就返回 `#f`，而不对剩余参数求值。
> 反过来说，如果所有的参数都不是 `#f`，那么就返回最后一个参数的值。

> `or` 具有可变个数的参数，并从左到右对它们求值。
> 它返回第一个不是值 `#f` 的参数，而余下的参数不会被求值。
> 如果所有的参数的值都是 `#f` 的话，则返回最后一个参数的值。

关于 `or` 逻辑的最后依据可以看作 or 会从左往右求职到第一个非 `#f` 的值, 如果没有 `#f` 会一直计算到最后一个参数, 并返回其结果 `#f`
