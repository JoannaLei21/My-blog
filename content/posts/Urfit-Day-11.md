---
title: "Urfit Day 11"
date: "2025-03-06"
author: Joanna Lei
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/D11-Job.png
# images:
#   - /img/cover.jpg
categories:
  - My Coding Life
tags:
  - Job
# nolastmod: true
draft: false
---

### Day-11 大病初癒&生日
  
<!--more-->
  
## 今日進度
- 今天繼續處理上次的票，之前試著查資料但還是找不到自己卡在哪，所以直接求救同事＠＠。  
然後就開始在程式碼裡繞來繞去...  
結論是，還沒解完手上的票 哈哈哈，然後多了很多思考題（笑）
- 補週一的1小時
### 拿到的票ing
- 表單更新資訊狀態後，會花很多時間重新抓資料，需要優化效能

### React:
[鐵人賽React文章：從 Hooks 開始，讓你的網頁 React 起來](https://ithelp.ithome.com.tw/articles/10216355)

- Day 17


### 會議 
- 部署會議：同事們特忙，因為上禮拜沒有部署。我在旁邊做GraphQL的資料整理。


### 明天進度
- 繼續完成手上的票 
- 練習題目＆查資料

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
- 不知道手上的票實際上要怎麼做。求救同事但基於一些原始程式的設定，後來要用別的方法去操作，所以原先的做法砍掉，哎對...又回到原點，哈哈。最大的困擾因該是，知道自己不懂，但不知道哪裡不懂。  
基礎不夠？原理沒通？還是要改程式碼沒摸熟？或是對整個框架沒理解怎麼運作？  
也有個可能就是，ALL!! (默默看上面那些沒回答出來的問題...)
 
## 今日心得
發燒完回來動腦，感覺小腦袋一下就冒煙了。  


## 作業
1. 練習設定query，只用一個`memberId`,找出這個相關的`phone` & `是否vaild`。  
```ts
// example
const GetMemberPhones =  gql`
query GetMemberPhones($memberIdList: [String!]) {
  member_phone(where: { member_id: { _in: $memberIdList } }) {
    id
    member_id
    phone
    is_valid
  }
}
```
2. 
    A:在Hasurq裡面，有`_in`, `_eq`的選項，他們代表什麼意思？  
    B:上面他們跟SQL對應的關係是？  
    C:他們分別吃什麼類型＆吐出什們類型  
3. GraphQL的基礎型別有哪些？（進階：如何自訂義型別）  
4. 了解網頁的`七層協定`，如HTTP協定、封包等等  
5. 延伸思考：為什麽要有型別？ 關於override  
6. 進階題：記憶體配置  


