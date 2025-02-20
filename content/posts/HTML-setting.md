---
title: "HTML-文件設定"
date: "2024-11-18"
author: Joanna Lei
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/HTML-Setting.png
# images:
#   - /img/cover.jpg
categories:
  - Learning Code
tags:
  - HTML
# nolastmod: true
draft: false
---

解析 HTML 開頭的那些咒語們

<!--more-->

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>xxxxxxxx</title>
    <link rel="stylesheet" href="styles/style.css" />
    <script src="scripts/todo.js" defer type="module"></script>
  </head>
</html>
```

在寫 HTNL 的時候，很開心的 keyin"!"，按下 enter，然後
咻～
上面的程式碼就長出來了！但是這些代表什麼意思呢？為了~~順利找到工作~~增加自己的知識，讓我們來看一下吧

---

```HTML
<!DOCTYPE html>
```

宣告 html 檔案類型，聲明版本為 HTML5，瀏覽器會以標準模式渲染網頁。

---

```html
<html lang="en"></html>
```

html：為文件的“根標籤”，文件中所有的標籤都必須在此標籤裡面。  
lang：為網頁主要使用語言，en 表示此 html 主要使用語言為英文。

這一行的功用是：  
 -搜尋引擎可根據 lang 來了解網頁的語言，優化結果  
 -讓使用者了解語言偏好  
 -有助於提升網頁 SEO 排名

---

```html
<head></head>
```

head：為 html 的標籤之一，中間會寫入關於網站的元信息(metadata)和其他非顯示於網頁內容上的資源。

---

```html
<meta charset="UTF-8" />
```

meta：代表定義頁面的元數據，ex:編碼、描述、關鍵字等。  
charset="UTF-8"：為指定文件的字符編碼為 UTF-8。  
UTF-8：為 unicode 的一部份，幾乎包含書寫系統中的字符，若無指定，會因預設的編碼無法讀取某些非英文字符（如中文）而出現亂碼。  
**目前 HTML5 規範推薦使用 UTF-8**，因具良好的兼容性，已成為網頁字符的編碼。

---

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
```

這段是用來控制網頁在移動設備上的顯示和縮放行為（在響應式網頁設計中尤為重要）  
name="viewport"：目的為設置**視口（Viewport）**屬性，特別針對移動裝置。  
content=：設定具體的屬性值。

- width=device-width：將視口的寬度設為設備的屏幕寬度，避免默認的縮放行為
- initial-scale=1.0：將頁面初始縮放比例為 1.0(100%)，即以原始比例顯示，不放大或縮小。

這段代碼的目的：

- 解決移動設備上的縮放問題：在移動設備的預設寬度為 980px，沒有設定的話需要手動放大縮小頁面。
- 提升使用體驗，在不同設備上都可以有好的可讀性和佈局。
- 配合 CSS 可以根據設備屏幕尺寸調整（做響應式設計）

---

```html
<title>xxxxxxxx</title>
```

title：為指定網頁的標題，顯示在瀏覽器標簽上。

---

```html
<link rel="stylesheet" href="styles/style.css" />
<script src="scripts/todo.js" defer type="module"></script>
```

link：連結到外部資源，這邊是連結 CSS 檔案。  
script：內嵌或飲用外部的 JavaScrip 文件。

---

以上就是基本的 HTML 檔案開頭會設定的資料。  
沒設定的話會怎樣嗎？  
其實不會耶！內容還是可以呈現在網站上，只是預設的功能，可能會讓你得到預想之外的東西。  
雖然一個“!”就可以幫我們把上面的資料叫出來，但在理解之後，若是遇到要做修改的時候，就知道從哪裡下手囉～
