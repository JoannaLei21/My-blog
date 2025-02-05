---
title: "糖果題"
date: "2025-01-24"
author: Joanna Lei
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/candy.png
# images:
#   - /img/cover.jpg
categories:
  - Learning Code
tags:
  - JavaScript
  - Python
# nolastmod: true
draft: false
---

# 龍哥的糖果題

<!--more-->

## CANDY-001 V
題目：找出陣列裡最小的兩個值的總和  
例如：  
  [15, 28, 4, 2, 43] 印出 6  
  [23, 71, 33, 82, 1] 印出 24

```Js
function sumOfSmallestValues(arr) {
  // 實作程式碼寫在這裡
}

const list1 = [19, 5, 42, 2, 77];
const list2 = [23, 15, 59, 4, 17];

console.log(sumOfSmallestValues(list1)); // 印出 7
console.log(sumOfSmallestValues(list2)); // 印出 19
```

### JavaScript V

解題思路：  
1. 用Math.min找出最小值  
2. 將1用filter移出  
3. 用2找出最小值  
4. 將1和3相加  
```js
function sumOfSmallestValues(arr) {
    const min1 = Math.min(...arr);
    const cut1 = arr.filter((n) => n !== min1);
    const min2 = Math.min(...cut1);
    return min1 + min2;
}

const list1 = [19, 5, 42, 2, 77];
const list2 = [23, 15, 59, 4, 17];

console.log(sumOfSmallestValues(list1)); // 印出 7
console.log(sumOfSmallestValues(list2));
```

### Python V

解題思路： 
1. 排序  
2. 將前兩個索引值相加
```py
def sumOfSmallestValues(arr) :
    sortedArr = sorted(arr);
    return sortedArr[0] + sortedArr[1];

list1 = [19, 5, 42, 2, 77];
list2 = [23, 15, 59, 4, 17];

print(sumOfSmallestValues(list1)); 
print(sumOfSmallestValues(list2)); 
```
---
## CANDY-002
題目：請寫一小段程式，印出連續陣列裡缺少的字元
```js
const chars1 = ["a", "b", "c", "d", "f", "g"];
const chars2 = ["O", "Q", "R", "S"];

function missingChar(chars) {
  // 實作寫在這裡
}

console.log(missingChar(chars1)); // 印出 e
console.log(missingChar(chars2)); // 印出 P

// 提示：
// 可使用字串的 charCodeAt 方法...
```

### JavaScript V
解題思路：   
1. 當陣列裡的字元是連續時，charCodeAt()出來的unicode應當是連續的, 當後面的字元跳一號時，unicode會增加超過1  
2. 因此先判斷後位者的unicode印出來的字元，是否等於前一位的 unicode＋1印出來的字元  
3. 若不是則代表跳號，印出此字元  
```js
const chars1 = ["a", "b", "c", "d", "f", "g"];
const chars2 = ["O", "Q", "R", "S"];

function missingChar(chars) {
  for (let i = 1; i < chars.length; i++) {
    if (chars[i] !== String.fromCharCode(chars[i - 1].charCodeAt(0) + 1)) {
      return String.fromCharCode(chars[i - 1].charCodeAt(0) + 1);
    } 
  } 
};

console.log(missingChar(chars1)); // 印出 e
console.log(missingChar(chars2)); // 印出 P
```

### Python
解題思路：   
```py

```
---
## CANDY-003
題目：完成函數的內容，把陣列裡的 0 都移到最後面
```js
let list = [false, 1, 0, -1, 2, 0, 1, 3, "a"];

function moveZerosToEnd(arr) {
  // 程式碼寫在這裡
}

let result = moveZerosToEnd(list);
console.log(result); // 印出 [false, 1, -1, 2, 1, 3, "a", 0, 0]
```

### JavaScript V
解題思路： 
1. 先把0給抓出來  
2. 再塞回陣列最後面  
or   
1. 將陣列分成有0沒有0  
2. 兩個在連接再一起。
```js
let list = [false, 1, 0, -1, 2, 0, 1, 3, "a"];

function moveZerosToEnd(arr) {
  const withZero = arr.filter(a => a === 0);
  const withoutZero = arr.filter(a => a !== 0);
  return withoutZero.concat(withZero);
}

let result = moveZerosToEnd(list);
console.log(result);
```

### Python
解題思路： 
```py

```
---
## CANDY-004
題目：完成函數的內容，把傳進去的秒數變成平常人類看的懂的時間格式
```js
function humanReadableTimer(seconds) {
  // 實作在這裡
}

console.log(humanReadableTimer(0)); // 印出 00:00:00
console.log(humanReadableTimer(59)); // 印出 00:00:59
console.log(humanReadableTimer(60)); // 印出 00:01:00
console.log(humanReadableTimer(90)); // 印出 00:01:30
console.log(humanReadableTimer(3599)); // 印出 00:59:59
console.log(humanReadableTimer(3600)); // 印出 01:00:00
console.log(humanReadableTimer(45296)); // 印出 12:34:56
console.log(humanReadableTimer(86399)); // 印出 23:59:59
console.log(humanReadableTimer(86400)); // 印出 24:00:00
console.log(humanReadableTimer(359999)); // 印出 99:59:59
```

### JavaScript V
解題思路： 
1. 最終要呈現為00:00:00，因此宣告三個常數並要呈現為  hr : min : sec  
2. 依照時間單位換算 1小時=3600秒， 1分鐘=60秒(用Math.floor()求計算整數)，60除不盡的餘數為剩餘秒數  
3. 依照格式，要兩個數字，用padStar確保長度，而padStar針對字串作用，故最後return時，先將hr/min/sec轉字串後再套padStar  
```js
function humanReadableTimer(seconds) {
  const hr = Math.floor(seconds / 3600); 
  const min = Math.floor((seconds % 3600) / 60); 
  const sec = seconds % 60; 

  return `${hr.toString().padStart(2, '0')}:${min.toString().padStart(2, '0')}:${sec.toString().padStart(2, '0')}`;
}


console.log(humanReadableTimer(0)); // 印出 00:00:00
console.log(humanReadableTimer(59)); // 印出 00:00:59
console.log(humanReadableTimer(60)); // 印出 00:01:00
console.log(humanReadableTimer(90)); // 印出 00:01:30
console.log(humanReadableTimer(3599)); // 印出 00:59:59
console.log(humanReadableTimer(3600)); // 印出 01:00:00
console.log(humanReadableTimer(45296)); // 印出 12:34:56
console.log(humanReadableTimer(86399)); // 印出 23:59:59
console.log(humanReadableTimer(86400)); // 印出 24:00:00
console.log(humanReadableTimer(359999)); // 印出 99:59:59
```

### Python
解題思路： 
```py
```
---
## CANDY-005
題目：完成函數的內容，把傳進去的數字的每個位數平方之後組合在一起
```js
function squareDigits(num) {
  // 實作寫在這裡
}

console.log(squareDigits(3212)); // 印出 9414
console.log(squareDigits(2112)); // 印出 4114
console.log(squareDigits(387)); // 印出 96449
```

### JavaScript V
解題思路： 
1. 先將數字切分-數字加“”變字串，用.split切開並成為陣列
2. 平方-.map讓陣列內的數值平方
3. 陣列字元串起來-.join可以把陣列中的元素串接出來
```js
function squareDigits(num) {
  return (num + "" ).split("")
  .map(n => n * n)
  .join("")
}

console.log(squareDigits(3212)); // 印出 9414
console.log(squareDigits(2112)); // 印出 4114
console.log(squareDigits(387)); // 印出 96449
```

### Python
解題思路： 
```py
```
---
## CANDY-006
題目：找出在數字陣列裡跟其它元素不一樣的值
```js
function findDifferent(numbers) {
  // 實作寫在這裡
}

console.log(findDifferent([1, 1, 1, 1, 3, 1, 1, 1])); // 印出 3
console.log(findDifferent([2, 2, 2, 4, 2, 2])); // 印出 4
console.log(findDifferent([8, 3, 3, 3, 3, 3, 3, 3])); // 印出 8
```

### JavaScript V
解題思路： 
所有的陣列，只有一個異類，因此  
1.如果它在第一個索引值，那他一定不等於第二或第三索引值的元素  
2.如果它不在第一索引值，那它一定不等於第一索引值的元素  
```js
function findDifferent(numbers) {
    const repeatNumber =  numbers[0] === numbers[1] ? numbers[0] : numbers[2] ;
    return numbers.find( n => n !== repeatNumber ) ;
}


console.log(findDifferent([1, 1, 1, 1, 3, 1, 1, 1])); // 印出 3
console.log(findDifferent([2, 2, 2, 4, 2, 2])); // 印出 4
console.log(findDifferent([8, 3, 3, 3, 3, 3, 3, 3])); // 印出 8
```

### Python
解題思路： 
```py
```
---
## CANDY-007
題目：在某個數字陣列裡，可能藏有某個不合群的奇數或偶數，試著找出它！
```js
function findSomeDifferent(numbers) {
  // 實作寫在這裡
}

console.log(findSomeDifferent([2, 4, 0, 100, 4, 11, 2602, 36])); // 印出 11
console.log(findSomeDifferent([160, 3, 1719, 19, 11, 13, -21])); // 印出 160
```

### JavaScript V
解題思路：  
1. 陣列裡不是奇數就是偶數，因此先用filters分類  
2. 不合群的只有一個，因此陣列的不合群元素數量一定小於合群元素數量，用.length查  
3. 用if判斷，印出兩個陣列相比，元素少的  
```js
function findSomeDifferent(numbers) {
  const odd = numbers.filter(number => number % 2 !== 0);
  const even = numbers.filter(number => number % 2 === 0);

  if (odd.length < even.length) {
    return odd[0];
  } else {
    return even[0];
  }
}

console.log(findSomeDifferent([2, 4, 0, 100, 4, 11, 2602, 36])); // 印出 11
console.log(findSomeDifferent([160, 3, 1719, 19, 11, 13, -21])); // 印出 160
```

### Python
解題思路： 
```py
```
---
## CANDY-008
題目：傳入一字串，計算得分最高的字
  英文字母 a 得 1 分、b 得 2 分、c 得 3 分，以此類推。
  所有傳入的字都是小寫。

```js
function highestScoreWord(input) {
  // 實作寫在這裡
}

console.log(highestScoreWord("lorem ipsum dolor sit amet")); // 印出 ipsum
console.log(highestScoreWord("heyn i need a rubygem up to build this")); // 印出 rubygem
console.log(highestScoreWord("in time machine there are some bugs")); // 印出 there
```

### JavaScript V
解題思路： 
1. 傳入一字串，計算得分最高的字
2. 英文字母 a 得 1 分、b 得 2 分、c 得 3 分，以此類推。
```js
function highestScoreWord(input) {
  const separatedText = input.split(" ");
  const scores = separatedText.map((strin) =>
    strin.split("").reduce((sum, char) => sum + (char.charCodeAt(0) - 96), 0)
  );

  return separatedText[scores.indexOf(Math.max(...scores))];
}

console.log(highestScoreWord("lorem ipsum dolor sit amet")); // 印出 ipsum
console.log(highestScoreWord("heyn i need a rubygem up to build this")); // 印出 rubygem
console.log(highestScoreWord("in time machine there are some bugs"));
```

### Python
解題思路： 
```py
```
---
## CANDY-009
題目：移除網址中的錨點（Anchor）
```js
function removeAnchor(url) {
  // 實作寫在這裡
}

console.log(removeAnchor("5xcampus.com")); // 印出 5xcampus.com
console.log(removeAnchor("5xcampus.com/#about")); // 印出 5xcampus.com/
console.log(removeAnchor("5xcampus.com/courses/?page=1#about")); // 印出 5xcampus.com/courses/?page=1
```

### JavaScript V
解題思路： 
1. 使用.slice可以印出指定索引值之間的值
2. 用.indexOf找出錨點＃的索引值
3. 如果有＃，印出＃前的值
4. 如果沒有＃，印出整個值
```js
function removeAnchor(url) {
  let anchor = url.indexOf("#")
  if (anchor !== -1){
    return url.slice(0,anchor)
  }
  return url
}

console.log(removeAnchor("5xcampus.com")); // 印出 5xcampus.com
console.log(removeAnchor("5xcampus.com/#about")); // 印出 5xcampus.com/
console.log(removeAnchor("5xcampus.com/courses/?page=1#about")); // 
```

### Python
解題思路： 
```py
```
---
## CANDY-010
題目：把數字以 10 進位展開式呈現，數字均為大於 0 的正整數
範例：9527 變成 "1000 x 9 + 100 x 5 + 10 x 2 + 7"
```js
function expandedForm(num) {
  // 實作寫在這裡
}

console.log(expandedForm(8)); // 印出 8
console.log(expandedForm(25)); // 印出 10 x 2 + 5
console.log(expandedForm(148)); // 印出 100 x 1 + 10 x 4 + 8
console.log(expandedForm(1450)); // 印出 1000 x 1 + 100 x 4 + 10 x 5
console.log(expandedForm(60308)); // 印出 10000 x 6 + 100 x 3 + 8
```

### JavaScript V
解題思路： 
1. 先轉成字串並切開
2. 使用map做變化，不需要的變成“”
3. 用filter篩掉""，再用join把值組合起來
```js
function expandedForm(num) {
  const numStr = num.toString().split("");

  return numStr
    .map((digit, index) => {
      const tenN = 10 ** (numStr.length - index - 1);
      return digit !== "0"
        ? tenN === 1 ? `${digit}`: `${tenN} x ${digit}`: "";
    })
    .filter((item) => item !== "")
    .join(" + ");
}

console.log(expandedForm(8)); // 印出 8
console.log(expandedForm(25)); // 印出 10 x 2 + 5
console.log(expandedForm(148)); // 印出 100 x 1 + 10 x 4 + 8
console.log(expandedForm(1450)); // 印出 1000 x 1 + 100 x 4 + 10 x 5
console.log(expandedForm(60308)); // 印出 10000 x 6 + 100 x 3 + 8
```

### Python
解題思路： 
```py
```
---
## CANDY-011
題目：找出一個數字陣列裡，出現奇數次數的數字
範例：[1, 1, 0]，`0` 只有出現 1 次
     [5, 5, 8, 8, 8, 4, 4]，`8` 出現了 3  次
```js
function findOddElm(numbers) {
  // 實作寫在這裡
}

console.log(findOddElm([1, 1, 2])); // 印出 2
console.log(findOddElm([5, 4, 2, 1, 5, 4, 2, 10, 10])); // 印出 1
console.log(findOddElm([0, 1, 0, 1, 0])); // 印出 0
console.log(findOddElm([1, 1, 2, -2, 5, 2, -1, -2, 5])); // 印出 -1
console.log(findOddElm([20, 2, 2, 3, 3, 5, 5, 4, 20, 4, 5])); // 印出 5
```

### JavaScript V
解題思路：
發現了神奇的＾運算法 
a ^ b = a ^ b
a ^ a = 0
0 ^ b = b
相同的值異或會為0
因此將所有的值異或後，會留下出現次數為奇數的值
藉由reduce的特性從而能讓所有值異或，留下出現次數為奇數的值 
```js
function findOddElm(numbers) {
 return numbers.reduce((a,b) => a ^ b)
}

console.log(findOddElm([1, 1, 2])); // 印出 2
console.log(findOddElm([5, 4, 2, 1, 5, 4, 2, 10, 10])); // 印出 1
console.log(findOddElm([0, 1, 0, 1, 0])); // 印出 0
console.log(findOddElm([1, 1, 2, -2, 5, 2, -1, -2, 5])); // 印出 -1
console.log(findOddElm([20, 2, 2, 3, 3, 5, 5, 4, 20, 4, 5])); // 印出 5
```

### Python
解題思路： 
```py
```
---
## CANDY-012
題目：把數字加總，最終濃縮成個位數
範例：9527 => 9 + 5 + 2 + 7 => 23 => 2 + 3 => 5
     1450 => 1 + 4 + 5 + 0 => 10 => 1 + 0 => 1
```js
const numberReducer = (num) => {
  // 實作寫在這裡
};

console.log(numberReducer(9527)); // 印出 5
console.log(numberReducer(1450)); // 印出 1
console.log(numberReducer(5566108)); // 印出 4
console.log(numberReducer(1234567890)); // 印出 9
```

### JavaScript V
解題思路： 
1. 將數字轉為字串後用.split分開成為陣列  
2. 用.reduce加總，得到加總值  
3. 重複上面兩個步驟，直到加總值為個位數。因為不確定圈數，使用while迴圈  
```js
const numberReducer = (num) => {
  while (num >= 10){
    num = (num + "").split("").reduce((arr, cv) => Number(arr) + Number(cv));
  };
  return num;
};

console.log(numberReducer(9527)); // 印出 5
console.log(numberReducer(1450)); // 印出 1
console.log(numberReducer(5566108)); // 印出 4
console.log(numberReducer(1234567890)); // 印出 9
```

### Python
解題思路： 
```py
```
---
## CANDY-013
題目：根據台灣財政部所提供的公司統編驗證規則，計算統一編號是否正確
https://www.fia.gov.tw/singlehtml/3?cntId=c4d9cff38c8642ef8872774ee9987283

```js
function isValidVatNumber(vat) {
  // 實作寫在這裡
}

console.log(isValidVatNumber("10458575")); // true
console.log(isValidVatNumber("88117125")); // true
console.log(isValidVatNumber("53212539")); // true
console.log(isValidVatNumber("88117126")); // false
```

### JavaScript
解題思路： 
```js

```

### Python
解題思路： 
```py
```
---
## CANDY-014
題目：把鄰近的重複值去除，但仍照原本的順序排序  
範例："AAABBBDDDAABBBCC" -> ['A', 'B', 'D', 'A', 'B', 'C']
```js
function uniqueOrder(sequence) {
  // 實作寫在這裡
}

console.log(uniqueOrder("AABCC")); // [ 'A', 'B', 'C']
console.log(uniqueOrder("AAABBBCCBCC")); // [ 'A', 'B', 'C', 'B', 'C']
console.log(uniqueOrder([1, 2, 1, 2, 1])); // [ 1, 2, 1, 2, 1 ]
console.log(uniqueOrder([1, 1, 1, 2, 2, 2, 1])); // [1, 2, 1]
```
 
### JavaScript V
解題思路： 
1. 使用filter來篩選，後面的值若與前面的值一樣時則捨去  
2. 當引數不是陣列時，需要先將值切開，使用typeof檢查，如果是字串則下用split切開成陣列  
```js
function uniqueOrder(sequence) {
  if (typeof sequence === "string"){
    sequence = sequence.split("")
  }
  return sequence.filter((value, index) => value !== sequence[index - 1]);
}

console.log(uniqueOrder([1, 2, 1, 2, 1])); // [ 1, 2, 1, 2, 1 ]
console.log(uniqueOrder([1, 1, 1, 2, 2, 2, 1])); // [1, 2, 1]
console.log(uniqueOrder("AABCC")); // [ 'A', 'B', 'C']
console.log(uniqueOrder("AAABBBCCBCC")); // [ 'A', 'B', 'C', 'B', 'C']
```

### Python
解題思路： 
```py
```
---
## CANDY-015
題目：把原本的字串拆解成 2 個字元一組，若不足 2 個字則補上底線  
範例：  
"abcdef" -> ['ab', 'cd', 'ef']  
"abcdefg" -> ['ab', 'cd', 'ef', 'g_']
```js
function splitString(str) {
  // 實作寫在這裡
}

console.log(splitString("abcdef")); // ["ab", "cd", "ef"]
console.log(splitString("abcdefg")); // ["ab", "cd", "ef", "g_"]
console.log(splitString("")); // []
```

### JavaScript V
解題思路： 
1. 先判斷長度是否為偶數，如果不是則在最後加""  
2. 設定迴圈，用.slice切開字串，因為需要有東西裝保出來的結果，所以準備一個空陣列放入結果，最後再回傳陣列  
```js
function splitString(str) {
  let strIndex = str.length % 2 != 0 ? str.concat("_") : str;
  let result = [];
  for (let i = 0; i < strIndex.length; i = i + 2) {
    result.push(strIndex.slice(i, i + 2));
  }
  return result;
}

console.log(splitString("abcdef")); // ["ab", "cd", "ef"]
console.log(splitString("abcdefg")); // ["ab", "cd", "ef", "g_"]
console.log(splitString("")); // []
```

### Python
解題思路： 
```py
```
---
## CANDY-016
題目：把原本 snake_case 的字轉換成 camelCase 格式  
範例："hello_world" -> "helloWorld"
```js
function toCamelCase(str) {
  // 實作寫在這裡
}

console.log(toCamelCase("book")); // book
console.log(toCamelCase("book_store")); // bookStore
console.log(toCamelCase("get_good_score")); // getGoodScore
```

### JavaScript V
解題思路： 
1. 利用把字切開  
2. 使用迴圈讓索引值為1之後的首個字做大寫轉換，並把後面的小寫字加回來  
3. 使用join把陣列中的值轉為字串  
```js
function toCamelCase(str) {
  const words = str.split("_");
  for (let i = 1; i < words.length; i++) {
    words[i] = words[i][0].toUpperCase()+ words[i].slice(1);
  }
  return words.join("");
}

console.log(toCamelCase("book")); // book
console.log(toCamelCase("book_store")); // bookStore
console.log(toCamelCase("get_good_score")); // getGoodScore
```

### Python
解題思路： 
```py
```
---
## CANDY-017
題目：計算數字的 2 進位裡有幾個 1  
範例：5 -> 101 -> 2 個 1
```JS
function countBits(num) {
  // 實作寫在這裡
}

console.log(countBits(1234)); // 5
console.log(countBits(1450)); // 6
console.log(countBits(9527)); // 8
```

### JavaScript V
解題思路： 
1. 轉成二進位：使用 number.string (2)
2. 讓所有的  "1"  加總起來，因此用.split將值拆開成陣列，在用.reduce加總
3. 因為.split出來為字串，.reduce加總需要數字，因此加判斷式如果值為 "1" 則傳出數字 1 
```js
function countBits(num) {
  const bits = num.toString(2).split("");
  return bits.reduce((acc, cv) => acc + (cv === "1" ? 1 : 0));
}

console.log(countBits(1234)); // 5
console.log(countBits(1450)); // 6
console.log(countBits(9527)); // 8
```

### Python
解題思路： 
```py
```
---
## CANDY-018
題目：實作一個可以印出隨機整數的函數
```JS
console.log(randomNumber(50)); // 隨機印出 0 ~ 49 之間的任何一個數字
console.log(randomNumber(5, 30)); // 隨機印出 5 ~ 29 之間的任何一個數字
```

### JavaScript V
解題思路： 
1. 在js中，若引數少於參數，會出現undefined，因此設定如果只有一個引數時，min =0, max = 原本的引數  
2. 用Math.random 曲隨機數字，Math.floor取整數  
```js
function randomNumber(min, max) {
  if (max === undefined) {
    max = min;
    min = 0;
  }
  return Math.floor(Math.random() * (max - min) + min);
}

console.log(randomNumber(50)); // 隨機印出 0 ~ 49 之間的任何一個數字
console.log(randomNumber(5, 30)); // 隨機印出 5 ~ 29 之間的任何一個數字
```

### Python
解題思路： 
```py
```
---
## CANDY-019
題目：檢查是否為某個數字的平方數
```JS
function isSquare(num) {
  // 實作寫在這裡
}

console.log(isSquare(0)); // true
console.log(isSquare(4)); // true
console.log(isSquare(5)); // false
console.log(isSquare(100)); // true
console.log(isSquare(-4)); // false
console.log(isSquare(-1)); // false
```

### JavaScript V
解題思路：  
1. 反推平方會使用開更號，使用Math.sqrt可以得到變數開更號後的值  
2. 若得到的值為整數，即為某數字的平方數，使用Number.isInteger剛好判斷ture/false  
3. 平方出來的數字不會為負數，因此在最前面先加條件篩選掉  

```js
function isSquare(num) {
  if (num < 0) {
    return false;
  }
  return Number.isInteger(Math.sqrt(num));
}

console.log(isSquare(0)); // true
console.log(isSquare(4)); // true
console.log(isSquare(5)); // false
console.log(isSquare(100)); // true
console.log(isSquare(-4)); // false
console.log(isSquare(-1)); // false
```

### Python
解題思路： 
```py
```
---
## CANDY-020
題目：檢查字串的 x 跟 o 的數量是不是一樣多，不分大小寫
```JS
function xxoo(str) {
  // 實作寫在這裡
}

console.log(xxoo("ooxx")); // true
console.log(xxoo("xxoo")); // true
console.log(xxoo("xxooo")); // false
console.log(xxoo("xoox")); // true
console.log(xxoo("ooAA")); // false
console.log(xxoo("xoXoA")); // true
```

### JavaScript V
解題思路： 
1. 不分大小寫，所以先統一格式，用.toUpperCase()轉成大寫  
2. 用.filter，分別篩出X,O並計算數量  
3. 結果需回傳布林值，因此設定兩個變數的數量相等
```js
function xxoo(str) {
  const upperStr = str.toUpperCase().split("");

  const xCount = upperStr.filter((index) => index === "X").length;
  const oCount = upperStr.filter((index) => index === "O").length;

  return xCount === oCount;
}

console.log(xxoo("ooxx")); // true
console.log(xxoo("xxoo")); // true
console.log(xxoo("xxooo")); // false
console.log(xxoo("xoox")); // true
console.log(xxoo("ooAA")); // false
console.log(xxoo("xoXoA")); // true
```

### Python
解題思路： 
```py
```
---
## CANDY-021
題目：實作 Stack 資料結構
```JS
class Stack {
  // 實作寫在這裡
}

const stack = new Stack();
stack.push(123);
stack.push(456);
stack.push();
console.log(stack.size); // 印出 2

const item = stack.pop(); // 取出元素
console.log(item); // 印出 456

stack.pop(); // 繼續取出元素
console.log(stack.size); // 印出 0
```

### JavaScript
解題思路： 
```js

```

### Python
解題思路： 
```py
```
---
## CANDY-022
題目：實作 Queue 資料結構
```JS
class Queue {
  // 實作寫在這裡
}

const queue = new Queue();
queue.enqueue(123);
queue.enqueue(456);
queue.enqueue();
console.log(queue.length); // 印出 2

const item = queue.dequeue(); // 取出元素
console.log(item); // 印出 123

queue.dequeue(); // 繼續取出元素
console.log(queue.length); // 印出 0
```

### JavaScript
解題思路： 
```js

```

### Python
解題思路： 
```py
```
---
## CANDY-023
題目：算出 N 個數字的最大公因數
```JS
function calcGCD(...numbers) {
  // 實作程式碼寫在這裡
}

console.log(calcGCD(10)); // 10
console.log(calcGCD(103, 27)); // 1
console.log(calcGCD(21, 15, 18)); // 3
console.log(calcGCD(104, 96, 36, 88)); // 4
```

### JavaScript
解題思路： 
```js

```

### Python
解題思路： 
```py
```
---
## CANDY-024
題目：算出 N 個數字的最小公倍數
提示：可使用 023 計算最大公因數的函數
```JS
function calcLCM(...numbers) {
  // 實作程式碼寫在這裡
}

console.log(calcLCM(10)); // 10
console.log(calcLCM(103, 27)); // 2781
console.log(calcLCM(21, 15, 18)); // 630
console.log(calcLCM(104, 96, 36, 88)); // 41184
```

### JavaScript
解題思路： 
```js

```

### Python
解題思路： 
```py
```
---
## CANDY-025
題目：
  一般我們常見的四捨五入計算方式在統計上容易造成計算偏差
  於是有人推出了「銀行家捨入法」用來稍微平衡計算偏差
  計算方式是「四捨六入五成雙」
  當捨入計算位數剛好是 5 的時候，會算出離這個數字比較近的偶數
```JS
function bankersRounding(num, digits = 0) {
  // 實作程式碼寫在這裡
}

console.log(bankersRounding(0.4)); // 0
console.log(bankersRounding(0.6)); // 1
console.log(bankersRounding(0.5)); // 0
console.log(bankersRounding(1.5)); // 2
console.log(bankersRounding(1.24, 1)); // 1.2
console.log(bankersRounding(1.26, 1)); // 1.3
console.log(bankersRounding(1.25, 1)); // 1.2
```

### JavaScript
解題思路： 
```js

```

### Python
解題思路： 
```py
```