---
title: "Urfit Day 09"
date: "2025-02-27"
author: Joanna Lei
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/D9-Job.png
# images:
#   - /img/cover.jpg
categories:
  - My Coding Life
tags:
  - Job
# nolastmod: true
draft: false
---

### Day-9 OMG 層層包疊
  
<!--more-->
  
## 今日進度

### 拿到的票  
- 表單更新資訊狀態後，會花很多時間重新抓資料，需要優化效能




### 模擬實作
- 
### React:
[鐵人賽React文章：從 Hooks 開始，讓你的網頁 React 起來](https://ithelp.ithome.com.tw/articles/10216355)

- Day 17


### 會議 
- 部署會議：週五放假，這週不執行部署


### 明天進度
- 補昨天早上的時數，完成手上的票

### 回答出來的問題
- **Q:**   


### 待回答的問題們  
- Q.1: stateless？
- Q.2: 查名詞 ：Template string 模板字串``
- Q.3: 什麼是Migration/ Migrate (回答不出來要被打屁屁了＠＠)
- Q.4: nullish vs falsy
- Q.5: upSert : upDate or insert/ onConflict 
- Q.6: 資料庫 Constraints unique / PK
- Q.7: 什麼是dependency injection依賴注入
- Q.8: upSert : upDate or insert/ onConflict 
- Q.9: 資料庫 Constraints unique / PK
- Q.10: useMemo, memonize(一種快取的方式), 閉包

### 遇到的問題
- 找不到要程式碼在哪。
要找最源頭抓到DATA的地方，但是卻一直跑去定義資料型別的地方。繞了老半天找不出個所以然才求救同事。才發現找錯地方了！  
資料在一個`<table>`裡，然後才知道原來在JSX裡面的標籤，其實都是一個函數。之前因問長得一樣，取名用法也一樣，所以會覺得在JSX裡的<button>, <div> 跟在HTML裡是一樣的，但其實不一樣（好暈）。

- useState的觀念不熟悉。
今天好不容易找到資料源，也看到有設定了useState，到要怎麼把它再放到我們要它運作的地方。  
說不熟悉，一個是層層包疊，弄的很暈。再來是需要理解原本的code寫的邏輯，然後忘記useState需要再將並更資料讓React知道。在之前看鐵人賽的Day7有提到，為什麼它不動，完全忘記了，哎呀呀。

- 怎麼從GraphQL抓出要的資料
知らないもん...あとで調べてみる。看不懂吧，就跟我看GraphQL一樣。

## 今日心得
啊啊啊啊啊啊啊  
好燒腦，以上。