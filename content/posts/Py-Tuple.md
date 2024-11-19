---
title: "Python-Tuple"
date: "2024-11-19"
author: Joanna Lei
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/Tuple.png
# images:
#   - /img/cover.jpg
categories:
  - Learning Code
tags:
  - Python
# nolastmod: true
draft: false
---

## 什麼是**Tuple**

<!--more-->

### Tuple 的定義

中文稱作：元組/數組，中文從字面翻譯看起來，還是不是很清楚是什麼。  
可以直接使用英文稱呼，發音是 two-pull or top-pull  
它是一種可以裝很多值的資料型態，長這樣： `（ x, x , x )`

建立 Tuple 時，使用`()`，並用`,`把資料分開即可。  
看起來很像串列，只是 Tuple 是不可變的(Immutable)，跟字串一樣

### 建立 Tuple

Tuple 的格式是`（ x, x , x )` ，在當只有一個值的時候，要記得給它`,`，長這個樣子`(x,)`，當沒有`,`時，`(x)`就只是`x`，而非一個 Tuple。

另外，Tuple 的`()`是可以省略的，只是在閱讀上容易混亂，所以我還是會乖乖的給他穿上`()`

---

## 常用的 Tuple 操作

### 拿裡面的資料

Tuple 和串列一樣，資料的值是有順序的，使用索引值可以拿到裡面的資料。

```py
cat = ("小白","小黑","三花","胖橘")
cat[0] #"小白"
cat[-1] #"胖橘"
```

Tuple 裡面的值是不可以改變的，但整個 Tuple 可以重新指定(Reassignment)

```py
#嘗試改變會得到錯誤訊息
cat = ("小白","小黑","三花","胖橘")
cat[0] = "大白"

Traceback(most recent call last).
  File......
TypeError: "tuple" object does not support item assignment.

#重新指定(Reassignment)
cat = ("小白","小黑","三花","胖橘")
cat = ("white","black","flower","fatty")
```

Tuple 是可迭代物件，跟串列一樣，可以使用`for...in...`的方式

```py
cats = ("小白","小黑","三花","胖橘")
for cat in cats:
  print(cat)

#"小白"
#"小黑"
#"三花"
#"胖橘"
```

### 查詢方法

與串列的查詢方法幾乎相同

`.len()` 算個數  
`.count()` 算數量  
`.index()` 取的索引值

**注意**  
因為 Tuple 裡面的值是無法改變的，所以下面這些發法無法使用：  
`.append()`增加、 `.inser()`插入、`.remove()`刪除，使用的話會得到`AttributeError`的錯誤訊息

**特殊情況**  
雖然 Tuple 不能變動，但當帶入的值是一個可變動的資料時（如串列），那針對可變動的資料我們可以去改變它。

```py
cat = ("小白","小黑","三花","胖橘",["小貓A","小貓B","小貓B"])
#[]裡的值可以變動，不會因Tuple而被限制
```

### Tuple 的好處

Tuple 在使用上與串列類似，最大的差別在於 Tuple 是**不可變的**。  
這樣設定的好處是，當資料被當作參數在各個函數之間穿梭時，不用擔心會一不小心被哪個函數改到裡面的值～因為 Tuplr 不接受

---

## 複製 Tuple

複習一下串列的複製方法：

1.使用`list()`函數  
2.~~使用`.copy()`~~  
3.使用`copy`模組的`copy()`函式  
4.使用切片 slice

上面被劃刪除線的，就是 Tuple 無法使用的
**注意**  
雖然看起來是複製了一個 Tuple，但因為 Tuple 不能改，所以系統指到的資料會是同一個，也就是說不管複製幾次，系統資料都是指到同一個 Tuple 資料

## 動動腦

來看看下面的 Tuple 是否相等
Q1：相同的值

```py
t1 = (1,2,3)
t2 = (1,2,3)

t1 == t2
t1 is t2

#Ture 值相等
#False 位置不相等
```

Q2：空 Tuple

```py
t3 = ()
t4 = tuple()

t3 == t4
t3 is t4

#True 都是空的
#True ！？
```

這邊，最後的`t3 is t4`會得到 Ture 是因為，反正都是空的，也不能改變值，那就給你同一個位置就好，不用浪費空間。這是空 Tuple 才有的特性，實作上不太會運用到。

---

## 選串列還是 Tuple?

新手小白的我實在沒什麼感覺，好像串列的運用上更自由一些，所以這邊先照老師的建議來使用：  
**1.是否會變更資料：**

- 會變更使用串列。
- 不會變更使用 Tuple，確保使用過程中資料不會被變動。

**2.看囊括的資料型態決定：**

- 若為同質性(Homogeneous)如都是字串或數字時，用串列。
- 若為異質性(Heterogeneous)如同時有字串、數字、字典時，用 Tuple。
