---
title: 'C++ and Py'
date: 2024-07-18
categories: 语法
tags: 
    - C++
    - Python
---

学习CS61A课程中所发现C++和Python语法的一些小差别。

<!-- more -->

## 逻辑运算符

### 符号不同

逻辑与 (&& in C++, and in Python): 当且仅当两个操作数都为真时，结果为真。
逻辑或 (|| in C++, or in Python): 当至少有一个操作数为真时，结果为真。
逻辑非 (! in C++, not in Python): 用来反转操作数的逻辑状态。如果操作数为真，则结果为假，反之亦然。

### 返回值不同

C++中的逻辑运算符的返回值是bool类型，总是true或false。

> Python 中的逻辑运算符 and 和 or 返回的不是布尔值，而是它们操作数中的一个值。
> (and)：如果第一个操作数为真，则返回第二个操作数的值；如果第一个操作数为假，则返回第一个操作数的值。
> (or)：如果第一个操作数为真，则返回第一个操作数的值；如果第一个操作数为假，则返回第二个操作数的值。

```python
>>> True and 13
______13
>>> False or 0
______0
>>> not 10
______False
>>> not None
______True
```

```python
>>> True and 1 / 0
______Error (ZeroDivisionError)
>>> True or 1 / 0
______True
>>> -1 and 1 > 0
______True
>>> -1 or 5
______-1
>>> (1 + 1) and 1
______1
>>> print(3) or ""
______3
```

```python
>>> def f(x):
...     if x == 0:
...         return "zero"
...     elif x > 0:
...         return "positive"
...     else:
...         return ""
>>> 0 or f(1)
______'positive'
>>> f(0) or f(-1)
______'zero'
>>> f(0) and f(-1)
______''
```

## 条件运算符

接下来我直接给出代码上的例子。

```c++
#include <iostream>

int main() {

    //condition ? value_if_true : value_if_false;

    int x = 5;
    int y = 10;
    std::string result = (x > y) ? "x is greater" : "y is greater";
    std::cout << result << std::endl;
    return 0;
}
```

```python

#value_if_true if condition else value_if_false

x = 5
y = 10
result = "x is greater" if x > y else "y is greater"
print(result)
```

## 奇妙的语法

我在编写py中求最小公倍数的代码时，发现了一个奇妙的语法。

> 且看gcd的实现

```python

def gcd(c, d):
            while d != 0:
                c, d = d, c % d
        return c
    
```

> c, d = d, c % d

这种实现比 C++ 的实现少了一个中间变量
这是因为Python 支持同时赋值（tuple unpacking），可以在一行内交换变量值，这使得代码更加简洁和直接。

> - while d != 0: 循环用于执行欧几里德算法，直到 d 等于 0。
> - c, d = d, c % d 是 Python 特有的语法，它在一行内完成了两个操作：
> - 计算 c % d 并将结果赋给 d。
> - 将原来的 d 赋给 c。 这样就实现了交换变量的操作，而不需要像 C++ 那样使用一个额外的变量来暂存中间结果。
