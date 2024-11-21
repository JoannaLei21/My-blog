---
title: "Python-LEGB"
date: "2024-11-19"
author: Joanna Lei
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/LEGB.png
# images:
#   - /img/cover.jpg
categories:
  - Learning Code
tags:
  - Python
# nolastmod: true
draft: false
---

## Function 的作用域

<!--more-->

## LEGB 規則

一般的程式語言，作用域大致分為全域和區域兩種。  
在 Python 裡，作用域則有小到大分為以下四種：

### Local 區域

當自己家裡有的時候，就用自己家的，而且外面拿不到  
這個就是 local

```py
def say_hi():
  name = "Joanna"
  print (f"hello {name}")
```

### Enclosing 封閉

只有在高階函數裡會出現，也就是函數裡有函數時

```py
def say_hi():
  name = "Joanna"

  def inner_hi():
    print (f"hello {name}")
```

這時候`inner_hi()`裡面沒有`name`，外面家裡有，這時候`name = "Joanna"`就是 enclosing

### Global 全域

在外面沒有被包起來的`name = "Lei"`，就是 global

```py
name = "Lei"

def say_hi():
  name = "Joanna"
  print (f"hello {name}")
```

### Built-in 內建

Python 有些非關鍵字的內建函數，如`print` `list` `int`

在找變數時，會依照範圍大小的順序去找：L->E->G->B。

### a = a + 1

當在函數內做賦值時，就是在宣告區域變數。

```py
a = 1

def hi():
  a = 2
  print(a)

hi()#2
print(a)#1
```

```py
a = 1

def hi():
  a = a + 1
  print(a)
```

這時候，`a`在函數裡面做了宣告的動作，但卻沒有實際賦值，這時候會出現錯誤訊息  
另外下面的也會出現一樣的錯誤訊息

```py
a = 1

def hi():
  print(a)
    a = 2
```

像是 JavaScript 裡面的 TDZ

### global & nonlocal

在函數內可以用`global`改變外面變數的值

```py
a = 1

def hi():
  global a #從這邊開始，後面的a都是指外面的a
  a = 2 #把a重新賦值

hi()#2
print(a)#2
```

`nonlocal`不等於`global`，帶表目前的不是 local，需要往外找 enclosing

```py
a = 0

def hi():
  a = 10

  def hey():
    nonlocal a #代表這邊不是local，所以往外找會找到 a = 10
    a +=1

  hey()
  print(f"1-{a}") #1-11

hi()
print(f"1-{a}") #1-0
```

### 函數 vs 方法

基本上都是函數

```py
number = [1,2,3,4]

numbers.sort() #方法 method，對物件做“sort”，會改變物件
sorted(numbers) #函數 function 將物件變成參數，不會改變物件
```
