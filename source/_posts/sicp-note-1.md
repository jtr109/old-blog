---
title: SICP 学习笔记 (一)
date: 2017-08-19 07:38:15
tags:
  - SICP
  - LISP
---

_目前从 1.2 开始做笔记, 之前的可能会, 也可能不会补上._

## 1.2

### 1.2.1 线性的递归和迭代

> 在各种常见语言的大部分实现的设计中, 对于任何递归过程的解释, 所消耗的存储量总与过程调用 数目成正比, 即使它所描述的计算过程从原理上来看是迭代的.

大部分语言中, 书写形式是递归, 但是处理逻辑是迭代的.

#### 练习 1.9

```lisp
# 题干
(define (+ a b)
  (if (= a 0)
      b
      (inc (+ (dec a) b))))

(define (+ a b)
  (if (= a 0)
      b
      (+ (dec a) (inc b))))

# 计算 (+ 4 5)
# 计算过程是递归的或者迭代的吗
```

```lisp
# 定义1

(+ 4 5)
(inc (+ 3 5))
(inc (inc (+ 2 5)))
(inc (inc (inc (+ 1 5))))
(inc (inc (inc (inc (+ 0 5)))))
(inc (inc (inc (inc 5))))
(inc (inc (inc 6)))
(inc (inc 7))
(inc 8)
9

# 结论: 以上递归过程属于线性递归计算过程

# 定义 2

(+ 4 5)
(+ 3 6)
(+ 2 7)
(+ 1 8)
(+ 0 9)
0

# 结论: 以上递归过程属于线性迭代计算过程
```

引用 [SICP 习题集](http://sicp.readthedocs.io/en/latest/chp1/9.html) 中的话:

> * 从计算过程中可以很明显地看到伸展和收缩两个阶段，且伸展阶段所需的额外存储量和计算所需的步数都正比于参数 a ，说明这是一个线性递归计算过程。
> * 从计算过程中可以看到，这个版本的 plus 函数只使用常量存储大小，且计算所需的步骤正比于参数 a ，说明这是一个线性迭代计算过程。


#### 联系 1.10

```LISP
# (A 1 10)

(A 1 10)
(A 0 (A 1 9))
(A 0 (A 0 (A 1 8)))
# ...
(A 0 (A 0 ... (A 0(A 1 1))))  # 9 个 (A 0 ...)
(A 0 (A 0 ... (A 0 2)))  # 9 个 (A 0 ...)
2^10
```

```LISP
(define (f n)
  (* 2 n))
```

```LISP
# (define (g n)
#   (A 1 n))

(g n)
(A 1 n)
(A 0 (A 1 (- n 1)))
...
# 2^n
```

### 树形递归

> 一般来说, 树形递归计算过程里所需的步骤数将正比于树中的节点数, 其空间需求正比于数的最大深度.
