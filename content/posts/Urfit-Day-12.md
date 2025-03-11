---
title: "Urfit Day 12"
date: "2025-03-07"
author: Joanna Lei
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/D12-Job.png
# images:
#   - /img/cover.jpg
categories:
  - My Coding Life
tags:
  - Job
# nolastmod: true
draft: false
---

### Day-12 交作業
  
<!--more-->
  
## 今日進度
### 交作業
**練習**
1. 練習設定query，只用一個`memberId`,找出這個相關的`phone` & `是否vaild`。  
```ts
// example
const GetMemberPhones =  gql`
query getMemberPhone($memberId: String!) {
  member(where: { id: { _eq: $memberId } }) {
    id
    member_phones {
      is_valid
      phone
    }
  }
}

variables: {
 "memberId": "222222"
}
```
**在Hasurq裡面`_in`, `_eq`代表意思？**  
這些是運算子，他們負責透過不同的方式來進行過濾。  
比較運算子用於比較同一類型的值。例如，比較兩個數字、兩個字串、兩個日期等。

- 透過比較值進行過濾  
相等運算子：等於`_eq`, 不等於`_neq`:
過濾或檢查空值：`_is_null` 
大於或小於運算子：大於`_gt`, 小於`_lt`, 大於等於 `gte`, 小於等於`_lte`  
基於清單的搜尋運算子：`_in`, `_nin`  

- 按布林表達式過濾  
根據某些標準不匹配進行篩選：`_not`  
在同一個查詢中使用多個篩選器： `_and`, `_or`

- 按文字過濾(較複雜)：  
包含文字`_like`, 不包含文字`_nlike`, 包含文字不分大小寫`_ilike`, 不包含文字不分大小寫`_nilike`,    
```gql
query UsersWithNameLike {
  users(where: { name: { _ilike: "%john%" } }) {
    id
    name
  }
}
```
開頭為`_similar`, 開頭不為`_nsimilar`,  
```gql
<!-- 取得名字以 A 或 C 開頭的作者清單： -->
query AuthorsWithAorC {
  authors(where: {name: {_similar: "(A|C)%"} }) {
    id
    name
  }
}
```
與正規表示式相符`_regex`, 與正規表示式不相符`_nregex`, `_iregex`, `_niregex`,   
```gql
query ArticlesWithRegex {
  articles(where: {title: {_regex: "[ae]met"} }) {
    id
    title
  }
}
```
**上面他們跟SQL對應的關係是？ **

**他們分別吃什麼類型＆吐出什們類型 **

**GraphQL的基礎型別有哪些？**（進階：如何自訂義型別）
`json`, `jsonB`, `Integer`, `Float`, `Double`, `Text`, `Boolean`,`Date`, `Time`, Timestamp` 

**參考文件**  
[Hasura Doc](https://hasura.io/docs/3.0/graphql-api/queries/filters/index)
### 拿到的票ing
- 表單更新資訊狀態後，會花很多時間重新抓資料，需要優化效能

### React:
[鐵人賽React文章：從 Hooks 開始，讓你的網頁 React 起來](https://ithelp.ithome.com.tw/articles/10216355)

- Day 17


### 會議 
- 部署會議：同事們特忙，因為上禮拜沒有部署。我在旁邊做GraphQL的資料整理。


### 明天進度
- 週末來查詢之前還沒回答的問題們
- 繼續完成手上的票

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
- 
 
## 今日心得



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

Q：如何在要的時候，用useMutations打要的query出去
Q:什麼時候用fetch, 什麼時候用useMutation, useQuery?
有四種呼叫API的方式，它們的差異，適用於的地方