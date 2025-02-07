---
title: "apple watch App"
date: "2025-02-06"
author: Joanna Lei
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/watchApp.png
#   - /img/cover.jpg
categories:
  - My Coding Life
tags:
  - Project
# nolastmod: true
draft: false
---

## Side Project: 製作一個apple Watch App

<!--more-->
### 緣起

在學習程式的過程中，同學傳了一則很有趣的[新聞](https://tw.news.yahoo.com/%E5%B0%8F%E4%B8%89%E8%80%8C%E5%B7%B2-%E8%87%AA%E5%AD%B8%E5%AF%AB%E7%A8%8B%E5%BC%8F%E5%8A%A0%E4%B8%8Aai%E5%8D%94%E5%8A%A9-%E6%88%90%E5%8A%9F%E9%96%8B%E7%99%BC%E8%A8%98%E5%B8%B3app-105802896.html?guccounter=1&guce_referrer=aHR0cHM6Ly93d3cuZ29vZ2xlLmNvbS8&guce_referrer_sig=AQAAAFH_AyM3oMtxdWPh1h1g9P0Kso1zZzkmXEtnPFqG79xjgVjN7Gr-toxih91nzpudiQ6T7NIxE138PeJUTiFdVhR7wGQjCqLOqPAw8yyBay0wr8dh1P6ULMFUOygoQ2CysW-TpQui5njS1W5EFFFxSSA346tvRup017kwFsl7d_Ur)，一個名叫海馬的小弟弟自學＋Ai輔助，建立了一個apple watch的記帳App。  
後來在[Webconf](https://webconf.tw/agenda)上，也有幸聽到他分享他自己製作App的心路歷程。  
在課程的專案結束之後，在思考要做什麼小專案，剛好快速面試時教室用了一個很可愛的蕃茄鐘，字季也很想要，但是好貴。這時候就想到不如自己做一個可愛的 apple watch 番茄鐘 App吧~  

當然，在apple watch上，已經有內建鬧鐘，也有支援番茄鐘的App，基於下面幾點，決定要製作自己的 apple watch 番茄鐘App:  
- 自己想練習
- 好奇為什麼一個10歲的小朋友就有能力自行製作
- 內建的計時器介面很一般，想要有可愛的介面
- 不想花錢單純為了買一個可愛的計時器
- 現有的番茄鐘App為中國開發，不想提供資料給開發者 

## 環境設定
### 下載Xcode
要製作Apple的App，首先要先找到[Apple Developer](https://developer.apple.com/)的網站，點進Developer後，可以直接按右邊的Download
![進入developer](/images/watchApp-0.png)
一開始會在Opearting Systems頁面，這不是我們要的，點旁邊的Application進入下面的頁面  
（之前以為在Opearting Systems的頁面下載，載超久然後檔案是開不了的）
![進入Applications](/images/watchApp-1.png)
下載會花一點時間，當時估時約18分鐘，可以先泡杯咖啡或研究一下其他的資料。  
下載好之後會是右邊的壓縮檔.xip，解壓縮後就可以看到左邊的Xcode檔案。  
![進入developer](/images/watchApp-2.png)
打開Xcode，便可以開始在本機執行安裝：  
這邊沒有勾選到，但之後需要也不用擔心，可以之後在程式裡面的設定下載
![進入developer](/images/watchApp-3.png)
![進入developer](/images/watchApp-4.png)

### 開新專案
由於是第一個專案，所以開啟安裝好的Xcode後，點選`Create New Project`
![開新專案](/images/creatProject-0.png)
接下來選擇我們要製作專案的類型，這邊選擇App
![選擇專案性質](/images/creatProject-1.png)
接這來設定專案的名稱、細項，在`team`可以登入自己的appleID，第一次登入的話會跳出設定的視窗，可以做一些外觀的調整。
![設定專案名稱細項](/images/creatProject-2.png)
設定好之好，會自動建立一個資料夾，可以自己選擇存放的位置
![選擇資料夾位置](/images/creatProject-3.png)
基本設定完成後，就可以開始解程式碼了！
![完成專案設定](/images/creatProject-4.png)

### 加入Watch介面
在上一個步驟，我們已經把專案建立起來了，但畫面上顯示的不是watch的介面  
這時候需要再做一個步驟，讓我們在編輯的時候，可以直接看到在watch呈現的樣子。  
在上方控制列，進入File-> New -> Target
![設定watch顯示介面](/images/targetWatch-0.png)
再調出來的視窗，上排的選項中點選`watchOS`，並選擇`App`
![選擇App](/images/targetWatch-1.png)
接著設定，這個watch App是以何種方式存在：  
- Watch-only App → 僅限於 Apple Watch 的 App 沒有 iPhone 版
- Watch App with New Companion iOS App → 建立新的 iOS App 及對應的 Watch App
- Watch App for Existing iOS App → 為現有的 iOS App 建立 Watch App
![設定名稱](/images/targetWatch-2.png)
設定好之後就可以看到介面上出現watch的樣式了！  
但因為一開始安裝的時候，我並沒有勾選到watch，所以現在需要按下watch下方的`get`來下載需要套件，這個下載也需要花一些時間，耐心等待一下囉～
![下載](/images/targetWatch-4.png)
![下載](/images/targetWatch-3.png)

在以為下載好watch，滿心期待開始要來寫程式之後，卻發現出現了錯誤！
![error-1](/images/watchError-1.png)
好吧，在寫程式的路上，沒有錯誤才奇怪，檢查了一下發現，watch必須依賴在iphone之下，所以除了安裝watch需要的套件之外，也需要安裝手機的套件（嗚嗚我的容量）

## App功能發想
在等待下載的期間，先來釐清一下自己要製作什麼樣式的App  
- 功能：參照番茄鐘，專注25分鐘休息5分鐘
- 介面：隨著時間的經過，番茄長出來。一開始只有外框線，時間滿了之後，會填滿，填滿的番茄可以收成，之後可以換不同的水果之類
- 設定：有自己的果籃，可以選則時間跑動的樣式，列如：番茄 西瓜之類。可以使用watch旁邊的轉輪增減時間。時間到



## 設計使用者介面

兩個重要的項目
WatchKit App: 負責存放資源、UI顯示  
Interface.storyboard：同 iOS，裡面有系統預設建立的視圖控制器  
Assets.xcassets：同 iOS，存放用到的資源項目  
info.plist：同 iOS，WatchKit App 相關設定  

WatchKit Extension: 負責程式呼叫、邏輯處理( * .swift)  
InterfaceController.swift：預設的視圖控制器程式  
ExtensionDelegate.swift：類似Swift的AppDelegate，Apple Watch App 啟動入口   NotificationController.swift：用於處理Apple Watch App上的推播顯示  
Assets.xcassets：這裡不使用，我統一放在WatchKit App的Assets.xcassets下  
info.plist：同 iOS，WatchKit Extension 相關設定  
PushNotificationPayload.apns：推播資料，可用在模擬器上測試推播功能  

## 功能設定

## 測試應用

## 提交至 App Store

## 參考資料：
[Harry Li-動手做一支 Apple Watch App 吧！](https://zhgchg.li/posts/e85d77b05061/)

