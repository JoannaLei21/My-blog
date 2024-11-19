---
title: "Python-Set"
date: "2024-11-19"
author: Joanna Lei
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/Set.png
# images:
#   - /img/cover.jpg
categories:
  - Learning Code
tags:
  - Python
# nolastmod: true
draft: false
---

## Set 集合

<!--more-->

### Set 集合是什麼

集合的特性：  
1.集合裡的元素不會重複。  
2.集合裡的元素沒有順序。

### 建立集合

1.使用{}

```py
s1 = {1,2,3,3,4,3,4}
print(s1) #{1,2,3,4}

type(s1) #<class "set">
```

2.使用`set()`

```py
s2 = set([1,2,3,3,4,3,4])
print(s2) #{1,2,3,4}
```

### 集合的作用

透過集合裡面不重複的特性，可以篩選掉重複的值，但要注意篩出來的結果不一定會按照原來的順序排列。  
另外集合不接受不可雜湊的物件：

```py
s5 = {[1,2],3,4}

TypeError:unhashable type: "list"
```

當放入不可雜湊的物件`[1,2]`會飽出錯誤訊息。

### 空集合={}?

之前提的的物件皆有空值  
`[]` 空串列，`()` 空 Tuple，那空集合是`{}`嗎？  
答案是 NO! `{}`是空字典。而空集合必須使用`set()`

```py
s = set()
#這樣才會得到一個空集合
```

### 複製集合

集合有兩種方式可以做複製： 1.使用`set()`  
2.使用`.copy()`

```py
all = {1,2,3,4,5}
s1 = all.copy
s2 = set(all)
```

集合因為沒有順序的關係，因此無法使用切片來複製。

---

## 交集、聯集、差集的運算

在開始消耗腦細胞之前，先來張示意圖，複習一下數學課：
![圖片名稱](https://steam.oxxostudio.tw/webp/python/basic/set-01.webp)

### 交集

是兩個共同有的東西，使用`&`、`.intersection()`

```py
s1 = {1,3,5,7,9}
s2 = {3,6,9,12,15}

s1 & s2 #{3,9}
S1.intersection(S2)#{3,9}
```

另外可以用`.isjisdoint()`來判斷是否有重複(交集)

```py
s1 = {1,3,5,7,9}
s2 = {3,6,9,12,15}
s3 = {2,4,6,8}

s1.isjisdoint(s2) #False 有交集
s1.isjisdoint(s3) #True 無交集
```

### 聯集

是兩個所有的東西，使用`|`、`.union()`

```py
s1 = {1,3,5,7,9}
s2 = {3,6,9,12,15}

s1 | s2 #{1,3,5,6,7,9,12,15}
S1.union(S2)#{1,3,5,6,7,9,12,15}
```

### 差集

是兩個所有的東西，使用`-`、`.different()`  
**注意**這邊先後順序會有差別

```py
s1 = {1,3,5,7,9}
s2 = {3,6,9,12,15}

s1 - s2 #{1,5,7}
S1.different(S2)#{1,5,7}

s2 - s1 #{6,12,15}
S2.different(S1)#{6,12,15}
```

---

## 子集合、超集合、嚴格子集

之後再補充 python:910

### 子集合

### 超集合

### 嚴格子集

---

## 集合推導式

### 容易混淆的`{}`

集合推導式長這樣：

```py
s = {n for n in range(5)}
type(s) # <class "set">
```

但注意，如果裡面帶的是 key:value，就會變成是字典推導式

```py
dict = {n:n for n in range(5)}
dict # {0:0, 1:1, 2:2, 3:3, 4:4}
```

---

## 冷凍集合

在集合中，可以使用`forzenset()`讓集合裡的物件無法被變更，像是 Tuple 的效果。  
因為 forzenset 為不可變的，所以屬於一種可“雜湊物件”。
