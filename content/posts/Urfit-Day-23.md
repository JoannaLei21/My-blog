---
title: "Urfit Day 23"
date: "2025-03-24"
author: Joanna Lei
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/D23-Job.png
# images:
#   - /img/cover.jpg
categories:
  - My Coding Life
tags:
  - Job
# nolastmod: true
draft: false
---

### Day-23 轉來轉去
  
<!--more-->
  
## 今日進度
手上的票應該要結束了，但是卡在型別沒辦法被正確帶入＠＠  
今天一個一個把會用到日期的地方，將型別印出來，逐一檢查到底在哪兒型別跑掉了。  
還好算順利，找到卡住的地方，順利解決問題～


### 拿到的票
- Done: 付款與訂單效期調整-前端樣式調整

### React:
[鐵人賽React文章：從 Hooks 開始，讓你的網頁 React 起來](https://ithelp.ithome.com.tw/articles/10216355)

- Day 17


### 會議 
- 立會: 簡單報告目前的進度


### 明天進度
- 推PR
- 拿新的票

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
- Q.8: 資料庫 Constraints unique / PK
- Q.9: useMemo, memonize(一種快取的方式), 閉包

### 遇到的問題
- 型別轉換
手上的票會剛好處理到前後端，所以一開始在前端設定了日期，型別是Moment，在傳給後端之前，把它轉成 `Date` 。  
照理想上，後端吃 `Date` 就可以運作，但是因為在驗證時，資料全部被轉成 `String` ，所以當我想要把日期用 `.toISOString()` 轉成標准日期時，就出錯了。  
為什麼呢？因為 `.toISOString()` 吃的是 `Date` ，但它接到的卻是 `String` 。  
為了這個找了好久，才找到原來是在驗證的時候，日期的型別被轉掉了。  
處理的方法是，將驗證過後的資料，用解構賦值的方式，將日期從 `string` 轉為 `Date` ，然後在要傳出去的地方再用`.toISOString()` 轉成標準時間。  
或許你會和我有一樣的疑問，最後如果要的就是 `String` ，為什麼不直接用，還要先轉成 `Date` 再轉成 `String` ？  
原因是，在資料丟到後端的時後，就是 `Date` ，定義中的描述也是 `Date` ，那如果之後有人要使用這個日期，第一直覺也會認為型別就是 `Date` ，然後就會遇到我今天碰到的問題，要逐一排除才會發現，原來在某個地方它竟然變成 `String` 了！  
所以這邊又回到一個核心的概念：code不是當下可以跑就好，要預想之後的情或或是下一個人要使用的時候，是否能快速的取用不用做調整。

## 今日心得
呼～又完成一張票覺得放鬆不少，過程中彎彎繞繞，雖然很頭大但也因此對型別更了解了！而且這次用useState變得更順手了呢 嘿嘿～