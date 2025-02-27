---
title: "Urfit Day 07"
date: "2025-02-25"
author: Joanna Lei
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/D7-Job.png
# images:
#   - /img/cover.jpg
categories:
  - My Coding Life
tags:
  - Job
# nolastmod: true
draft: false
---

### Day-7 三元運算燒腦中
  
<!--more-->
  
## 今日進度

### 拿到的票  

### React:
[鐵人賽React文章：從 Hooks 開始，讓你的網頁 React 起來](https://ithelp.ithome.com.tw/articles/10216355)

- Day 14: 快速看過。介紹CSS-in-JS套件：emotion  
- Day 15: 用emotion設定樣式，並帶入SVG  
- Day 16: useState


### 會議  
- 例會（約10分鍾）：簡單報告週一進度
 

### 明天進度
- 

### 回答出來的問題
- **Q: useState & useEffect的差別是？**  
  說到useState & useEffect，這兩個是在React16.8中新增的功能`Hook`， 這個新功能可以讓我們不用寫class Component就能使用state以及其他功能。  
  
  useState 是資料狀態管理，主要在偵測資料是否做出變化。  
  基本結構：
  ```js
  const [state, setState] = useState(initialState)
  ```

  ---
  useEffect 是副作用(side effect)處理，副作用如資料獲取、訂閱或手動方式修改React Component DOM。  
  基本結構：
  ```js
  useEffect(callback, array)
  ```

  由於是在處理副作用side effect，而目前對副作用並不知道它是什麼，所以先暫停一下，來了解一下什麼是副作用side effect。    
  [Side effect 影片介紹(英文)](https://www.youtube.com/watch?v=KVTyPpUNWz4)

  side effect在程式設計中指的是一個函式除了回傳值之外，還影響外部狀態的行為。這可能包括：

  修改全域變數或外部變數
  改變 DOM
  進行 I/O 操作（例如發送 HTTP 請求、寫入檔案）
  設定計時器（如 setTimeout 或 setInterval）

  **純函式（Pure Function）**則是相反的概念，它不應該產生任何 Side Effect，只依賴輸入並回傳輸出。

  而上面提到的資料獲取(API請求)、訂閱或手動方式修改DOM，是在React中，最常見的副作用例子。  
  而因為 React 組件本身應該是純函式，所以 React 會建議將這些副作用放入 useEffect。



### 待回答的問題們  
- Q.1: stateless？
- Q.2: 查名詞 ：Template string 模板字串``
- Q.3: 什麼是Migration/ Migrate (回答不出來要被打屁屁了＠＠)
- Q.4: nullish vs falsy

### 遇到的問題
- 迷失在資料當中
  今天找資料的時候發現，有些資料是在亂寫，不過能發現它在亂寫，也代表自己有一定的知識儲備，才能分辨出來。只是在找資料的時候會發現，中文的資料，大家切入的點幾乎會相同，英文的也是，然而中文和英文切入的點會不一樣。  
  今天在找關於uesEffect的時候，在關於side Effect這塊迷路了。  
  - 中文的資料會直接提side Effect的例子如抓API資料等等。  
  - 而英文的資料，會先帶到pure function, impure function, 再說到side Effect，然後舉例符合這個特點的有抓API資料等等。  
  兩者比較起來，英文的切入點，讓我比較清楚。  
  或許有人會問，那這有什麼問題，你就去看英文資料不就好了？  
  其實迷失在資料之中，最大的問題不是找不到資料，而是花很多時間。可能很認真的花了很多時間精力去讀資料，但還是不懂，要在繼續找資料，無限循環直到找到自己能懂的資料。  
  那，有什麼解決辦法嗎？  
  一個是問Ai，再去找資料驗證。  
  另一個是找到資料後，有前輩可以問的話，先確定自己找的方向是對的，不需要等到全部弄懂才問。因為對方可以直接告訴你關鍵字是什麼，這時候再去查詢會更快。  
  所以今天也犯了一個小錯誤，希望能得到完整的答案＆理解，再去回覆主管的問題。會說是錯誤是因為，自己怕沒全弄懂就去問，會被覺得很笨＠＠，或是怕被對方貶低，所以花了很多時間在找資料。後來把自己理解的稍微整理一下，主管馬上點出這個觀念在運用上會需要特別注意的概念，這時候再回去找資料補足，馬上就更加清晰了。

## 今日心得
有些事，雖然知道也不一定做得到（反省），對於自己的知識儲備不足的焦慮，同時又擔心被怕被看扁，真的很矛盾，明明這時候最因該不恥上問（誰說只有下問才會覺得羞恥 哈哈）。但又不能完全自己沒努力就一直問別人，這樣又會被討厭。所以需要抓一個平衡，或許上午查資料，下午就要把自己上午理解的先和主管確認一下，看看有沒有走錯方向，也順便確認沒有看到的重點。減少在資料海洋中浪費的時間～