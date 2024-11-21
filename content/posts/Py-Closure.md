---
title: "Python-Closure"
date: "2024-11-20"
author: Joanna Lei
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/py-closure.png
# images:
#   - /img/cover.jpg
categories:
  - Learning Code
tags:
  - Python
# nolastmod: true
draft: true
---

## Python 裡的閉包 Closure-待補充

<!--more-->

### 自由變數 Free Variable

在 enclosing 的情況下，內層函數使用要外層變數的時候，外層的變數對內層來說就是自由變數

```py
def hi():
  name = "Joanna"

  def inner_hi():
    print(name)

  hi()

hi()# "Joanna"
```

對`inner_hi()`而言，`name = "Joanna"`就是自由變數。  
這時候如果再呼叫函數裡面的變數，是拿不到的

```py
def hi():
  name = "Joanna"

  def inner_hi():
    print(name)

  hi()

hi()# "Joanna"
print(name)#Error
```

### 閉包

延續上面的例子，把裡面的函數`reture`給外面的函數時，就會產生閉包的效果。

```py
def hi():
  name = "Joanna"

  def inner_hi():
    print (name)

  return inner_hi #注意這邊是return

hi()
abc = hi ()
abc()
```

這時候呼叫`hi()`時，我們會得到裡面的`inner_hi()`
