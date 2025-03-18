---
title: "Urfit Day 15"
date: "2025-03-12"
author: Joanna Lei
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/D15-Job.png
# images:
#   - /img/cover.jpg
categories:
  - My Coding Life
tags:
  - Job
# nolastmod: true
draft: false
---

### Day-15 最後一步了！
  
<!--more-->
  
## 今日進度

### 拿到的票
- ing:表單更新資訊狀態後，會花很多時間重新抓資料，需要優化效能

### React:
[鐵人賽React文章：從 Hooks 開始，讓你的網頁 React 起來](https://ithelp.ithome.com.tw/articles/10216355)

- Day 17


### 會議 
- blooming：PM佈達這週需要做的事，並作需求說明。
- 模擬實作：今天提出要做的沒有很多，同事們直接處理，所以沒有進行。

### 明天進度
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
- Q.8: 資料庫 Constraints unique / PK
- Q.9: useMemo, memonize(一種快取的方式), 閉包

### 遇到的問題
- 解構賦值。因為要用useState的概念來更新資料，需要先找出可以使用，已設定好的useState。  
找找找，沒有找到下手的地方，只有找到最源頭有設定的useState。  
後來找同事求救，才知道找是找對了，但是沒看懂所以不知道怎麼用。於是就來到今日的小學堂：解構賦值。

- 將新的資料塞回去原始資料之後，在丟給setter。  
一開始沒弄懂，整理一下
```js
const [A, setA] = useState()
```
現在已經有資料A，但我們會對A資料中裡面的一小部分做更新，這時資料會變成`A.1`，接著就要把`A.1`丟給`setA()`這樣才會偵測資料有更新了。  

所以要先複製一個原始資料。
```js
const updatedMemberPhone = {...salesLead};
```
再來需要找出這筆資料的id
```js
const memberIndex = updatedMemberPhone.SalesLeadMember.findIndex(member => member.id === memberID)
```
如果有找到資料，則會回傳索引值，沒有則會回傳-1，因此來判斷如果!== -1，就將資料重新賦值
```js
const memberIndex = updatedMemberPhone.SalesLeadMember.findIndex(member => member.id === memberID)

if memberIndex !== -1 {
  updatedMemberPhone.SalesLeadMember[memberIndex].phones = data.member.member_phonse.map(newPhone => phoneNumber: newPhone.phone
    isValid: newPhone.is_vaild)
}
```
最後執行setter
```js
setSalesLead(updatedMemberPhone)
```
const XX = data.member.member_phonse.map(newPhone => phoneNumber: newPhone.phone
    isValid: newPhone.is_vaild)
const updatedSalesLead =  [...salesLead, {...SalesLeadMember.phones: XX} ]



## 今日心得
