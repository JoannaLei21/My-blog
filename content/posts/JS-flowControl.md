---
title: "JavaScripts-Flow Control"
date: "2024-10-28"
author: Joanna Lei
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/flowControl.png
# images:
#   - /img/cover.jpg
categories:
  - Learning Code
tags:
  - JavaScript
# nolastmod: true
draft: false
---

## 流程控制 Flow Control

## <!--more-->

### 目的

當我們希望程式能依照不同的語法來決定程式執行的順序時，
就可以使用流程控制工具。

### 定義：

流程控制是指在程式執行時，個別的指令執行或求值的順序。  
基本上，程式執行是由上而下，一行一行的執行。  
當有流程控制指令，如：if, else/ Switch 時，會依照指令裡的指示去判斷情況，執行符合設定條件的內容。  
JavaScript 中將流程控制再細分為「條件判斷控制」與「迴圈控制」。  
這會先來看看「條件判斷控制」

---

## 條件判斷控制

在條件判斷中，有下面兩種語法可以讓程式判別條件，並執行指令

### If..., else...

在設定條件判斷時，在對用法還不熟悉的階段，我們可以先把條件用口語敘述的方式寫下來。  
ex: 如果不是男生，就是女生。  
寫出來之後，我們再來用程式語言表達

```js
let gender = 1;

if (gender == 1) {
  console.log("男");
} else {
  console.log("女");
}
```

這邊，我們宣告一個變數 gender 的值為 1，如果資料回傳的值為 1，則會印出"男"，其他只要不是 1 的值，皆會印出"女"。  
如果要得到除了男或女之外的回答，我們可以用 else if 來增加判別條件，一樣先寫出我們要的判斷式  
ex: 如果不是男生，或是女生，就是多元性別。

```js
let gender = 1;

if (gender == 1) {
  console.log("男");
} else if (gender == 2) {
  console.log("女");
} else {
  console.log("多元性別");
}
```

同上面的範例，我們增加了：如果資料回傳的值為 2，則印出"女"，其他只要不是 1 或 2 的值，就印出 "多元性別"。  
else if 並沒有次數限制，可以在判斷式中增加多項的條件做使用。

### Switch

如果覺得上面 if…, else 的寫法太多分支的話，可以使用 switch 語法。  
用上述的範例來轉換

```js
let gender = 1;

switch (gender) {
  case 1:
    console.log("男");
    break;

  case 2:
    console.log("女");
    break;

  default:
    console.log("多元性別");
    break;
}
```

每個 case 都對應 break，代表這個分支結束了。如果沒有加，所有的結果都會被印出來。  
最後面的 defaulf 可寫可不寫，代表上面都不成立時印出的結果，像是 else 的功能。

---

## 變化運用

了解了基礎的指令表述方式，接下來我們可以使用簡單的附加條件，來讓判斷式的使用更加靈活

### 同一結果，複數條件

在設定條件時，會遇到必須同時滿足兩個條件，才得出結果時，我們可以使用 and/ or/ not 來增加敘述。其表示符號為：  
and: `&&`
or: `||`
not: `!==`

範例：

```js
let age = 5;

if (age < 18) {
  console.log("小朋友");
} else if (age > 18 && age <= 20) {
  console.log("未成年");
} else {
  console.log("成年人");
}

(age > 18 && age <= 20)(18 < age <= 20);
```

當年齡介於 18~20，用（大於等於 18 而且 小於等於 20）來表述。  
這邊或許會有疑問(age > 18 && age <= 20)是否能寫成(18< age <= 20)，
從字面上可以看出兩個語意是相同的，但如果用(18< age <= 20)，JS 在跑完(18< age )就結束了!  
可以試試看，當輸入 age = 21 時，一樣會被判定為"未成年"。  
這就是為什麼必須使用&&來使判斷時會滿足兩個指定的條件。

### 實作練習

了解了概念及基本的用法後，實際練習到熟練是非常重要的，特別是 if 在 JS 裡面很常被拿來運用。
讓我們先從簡單的題目，來記住 if 的用法吧！

1.練習題：判斷基數或偶數  
（結果顯示"基數"或"偶數"）  
提示：偶數的判定可以用"取餘數為 0"

```js
let num = prompt("請輸入一個數字：");

if (num % 2 == 0) {
  console.log("偶數");
} else {
  console.log("基數");
}
```

2. 練習題：檢查年齡是否符合喝酒標準  
   （結果顯示"可以喝酒"或"不可以喝酒"）

```js
let age = prompt("請輸入您的年齡：");

if (age >= 18) {
  console.log("可以喝酒");
} else {
  console.log("不可以喝酒");
}
```

3. 練習題：分數分級的判定  
   結果顯示：90 分以上"A", 80–89 分"B", 70–79 分"C", 60–69 分"D",60 分以下"F"）

```js
let score = 70;

if (score > 90) {
  console.log("A");
} else if (score >= 80 && score <= 89) {
  console.log("B");
} else if (score >= 70 && score <= 79) {
  console.log("C");
} else if (score >= 60 && score <= 69) {
  console.log("D");
} else {
  console.log("F");
}
```

4.進階練習題：計算輸入的年份是否為閏年  
提示：年份可以被 4 整除而不被 100 整除，但又可以被 400 整除  
第一種解法，用 if 裡面再包 if 條件

```js
let year = prompt("請輸入年份")

if(year % 4 == 0){
  if(year % 100 !== 0){
    if(year % 400 == 0){
     console.log("閏年")
     }else{
    console.log("平年")
}else{
    console.log("閏年")
}else{
    console.log("平年")
}
```

第二種解法，用&& ||連接條件

```js
let year = prompt("請輸入年份");

if ((year % 4 == 0 && year % 100 !== 0) || year % 400 == 0) {
  console.log("閏年");
} else {
  console.log("平年");
}
```

---
