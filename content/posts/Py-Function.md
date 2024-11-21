---
title: "Python-Function"
date: "2024-11-19"
author: Joanna Lei
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/py-Function.png
# images:
#   - /img/cover.jpg
categories:
  - Learning Code
tags:
  - Python
# nolastmod: true
draft: false
---

## 在 Python 裡的函數-待補充

<!--more-->

### 函數定義

### 函數格式

從 JavaScript 來到 Python，在之前一直被老師唸的縮排，現在老師終於不用再唸了～因為換 python 跟你說ダメ！來看一下 Python 接受的格式

```py
def hi():
  print("Hi Python")
```

有縮排在代表這是在這個 function 裡做的事情。沒有縮排就會壞掉呦，我們老師非常喜歡這個設定。  
另外在 function 裡面必須塞東西，如果沒有放東西也會壞掉，~~就是這麼任性~~但很貼心的是放什麼都可以，如果暫時不知道要放什麼，可以使用`pass`告訴它讓我先跳過，之後再回來寫。

### 參數 parameter

可以根據需要的去帶入參數，帶入幾個參數就會需要幾個引數 Argument，在 JavaScript 時可以不需要一個蘿蔔一個坑，但在 Python ダメ！

```py
def hi(NameA,NameB):
  print(f"Hello"{NameA},{NameB})

hi("Jojo","Anna")
```

當然也可以不設定參數，只是要記得，帶入時有幾個引數，在 function 就要有幾個參數。  
另外參數的命名，會以能立馬知道這時要做什麼的去命名，才不會看到函數時黑人問號。

## 關鍵引數 & 位置引數

在 Python 裡，對於引數的輸入格式，有一個貼心的小設定

### 位置引數 Positional argument

在輸入引數的時候，通常我們會根據位置來對應

```py
def hi(NameA,NameB):
  print(f"Hello{NameA},{NameB}")

hi("Jojo","Anna")
```

這邊`Jojo`會對應到`NameA`，而`Anna`會對應到`NameB`。
位置引數得順序，必須依照參數的順序，不然在函數的計算過程中會得到不一樣的結果。

### 關鍵引數 Keyword argument

但有些時候，為了避免使用者輸入錯誤的引數，我們可以要求在輸入引數的時候帶入參數名。

```py
def BMI(weight, height)
    print(height, weight)

BMI (weight= 50 , height = 165 )
BMI (height = 165, weight= 50 )
```

關鍵字引數的位置可以自由排序，因為已經指定參數了，順序就沒有關係了。

### 混合使用

位置引數和關鍵字引數可以一起使用，但有下面的規則：  
1.位置引數必須在關鍵字引數前面。  
2.`/`代表在此之前必須是位置引數，`*`代表在此之後必須是關鍵引數。

```PY
def printSomething(a,b,/,c,*,d,e):
  print(a,b,c,d,e)


printSomething(1,2,3,e=4,d=7)
printSomething(1,2,c=3,e=4,d=7)
```

在這邊`/`和`*`都不是參數，而是指定格式。  
中間沒有指定的`c`沒有限定，所以用哪個都可以。
除了我們在設定函數時看指定之外，在官方文件的資料中，去查詢函數時，也會使用` /``* `來表示這個函數的用法：

```py
sorted(iterable,/,*,key=none,reverse=False)
```

上面是`sorted()`的設定在`/`之前要填入可迭代的引數，`*`後面參數已經給值，代表這是預設值，不需再另外帶入引數，然而要更改預設值的話，就必須使用關鍵字引數做更改。

### 預設值的坑

預設值的目的是：普世價值，大家常用，宣告之後就可以不用一直重複做同一件事。
要特別注意，如果預設值設定為可變動的值（如空[]、random()），會因為 python 的**預設值在被定宜的時後，就會被決定了**

```py
def hi(a,nums=[]):
    nums.append(a)
    print(nums)

hi(1) #[1]
hi(2, ["a","b"]) #[a,b,2]
hi(3) #[1,3]
```

這邊`hi(3)` 並沒有再帶入關鍵字引數，因而會顯示預設值，而在執行`h1(1)`時，預設值就被定義了，所以在之後呼叫的`hi()`只要沒帶關鍵字引數，都會有`[1]`這個預設值。  
要避開這個坑，我們可以先將預設值設為`None`，然後在函數裡面加入判斷式

```py
def hey(a, nums=None):
    if nums is None:
        nums = []
    nums.append(a)

hi(1) #[1]
hi(2, ["a","b"]) #[a,b,2]
hi(3) #[3]
```

### `*`解決不確定引數的情況

如果要帶入的參數是不確定數量的資料時該怎麼辦？  
這個時候可以使用~~超級瑪利歐裡的無敵星星~~`*`來幫助我們

```py
def printNum(*Num):
  print(Num)

printNum(1) #(1,)
printNum(1,2,3,) #(1,2,3)
printNum(1,2,3,4,5) #(1,2,3,4,5)
```

`*`會吃下所有的**位置引數**，並把他們打包成 Tuple。

`*`只能吃位置引數，那關鍵字引數怎麼辦？  
`**`就讓兩個＊來搞定！

```py
def hi(*args, **kwargs):
   print(a,b)

hi(1,2,3,a=9,b=0) #
hi(4,x=1,y=3) #
```

## 用\*開箱 unpacking

待補充

## Docstring

待補充

## 回傳值

跟 JavaScript 一樣： 1.若是沒有`return`則函數沒有結果。  
2.只要遇到`return` 函數就結束了

### Early return
