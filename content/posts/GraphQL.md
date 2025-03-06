---
title: "GraphQL"
date: "2025-03-05"
author: Joanna Lei
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/GraphQL.png
# images:
#   - /img/cover.jpg
categories:
  - Learning Code
tags:
  - REACT
# nolastmod: true
draft: false
---

## GraphQL 是什麼？

<!--more-->

### 定義
GraphQL 不是框架，不是資料庫，是由 Facebook 開發的一個查詢語言。  
允許客戶端 自行定義查詢內容，只獲取需要的資料，而不是由後端決定回傳哪些欄位。

[GraphQL 官網傳送門](https://graphql.org/)

### 三大特點
1. 單一端點（通常是 /graphql）
一次Connection，所有請求都發送到同一個 URL，透過查詢語言來決定獲取哪些資料。
2. 客戶端決定需要哪些欄位
只獲取所需欄位，避免回傳不必要的資料。
3. 支援關聯查詢（Nested Query）
可以一次查詢多個關聯資料，減少 API 請求數量。
### 缺點
1. 開發與維護成本較高:GraphQL 的學習曲線較陡，開發者需要熟悉`Schema設計`、`Resolver開發`、`權限管理`等概念。
2. 伺服器負擔大：查詢過於靈活，可能造成效能問題。多層關聯查詢（Nested Query），可能會導致 `N+1` 查詢問題。  
3. 權限管理複雜：需要額外設定存取權限，避免資料洩漏。
4. 快取不容易：所有請求都用`POST`發送到同一個端點（/graphql），導致無法直接用 HTTP Cache，需要額外快取機制。
5. 文件較難維護：API 沒有固定路徑，開發者需要探索 Schema。

## 熟悉又陌生的API
這邊暫停一下，來複習一下什麼是API  
[影片傳送門](https://www.youtube.com/embed/zvKadd9Cflc?si=TXw9Gluol8XNFyU1)  
API Application Programming Interface 應用程式介面，扮演應用程式和應用程式之間的橋樑。  


## Restful API是什麼
### 定義
REST（Representational State Transfer）是一種 API 設計風格，透過 HTTP 方法（GET、POST、PUT、DELETE） 來操作資源（Resource）。每個資源都有一個固定的 URL，並透過不同的 HTTP 方法來對資源進行操作。  
### 範例 
如果我們的應用程式管理「活動（events）」，REST API 可能會這樣設計：  
|操作	| HTTP 方法|	URL|	說明|
|:--|:--|:--|:--|
|取得所有活動	|GET	|/events	|取得活動清單|
|取得單一活動	|GET|	/events/{id}	|取得特定活動|
|新增活動|	POST|	/events	|創建新活動|
|更新活動|	PUT|	/events/{id}|	修改特定活動|
|刪除活動	|DELETE	|/events/{id}|	刪除活動|


### 優點
- 使用標準的 HTTP 方法，簡單直觀。
- 獨立的 API 端點，每個 URL 都代表一個特定資源。
### 缺點
- 可能會有多個 API 請求，例如要同時取得「活動」和「活動的創建者」資訊時，前端可能需要呼叫兩個 API。
- 回傳的資料可能過多或過少，後端決定回傳哪些欄位，前端不能自訂。

## GraphQL vs Restful API
### 差異分析
|比較項目	|RESTful API	|GraphQL|
|:--|:--|:--|
|端點（Endpoint）|	多個端點（/events、/users）	|單一端點（/graphql）|
|查詢方式	|固定的 API 路由	|客戶端自訂查詢|
|回傳欄位|	由後端決定	|由前端決定|
|請求數量|	可能需要多次請求（N+1 問題）|	一次請求可獲取多層資料|
|即時訂閱（Subscription）	|需要 WebSocket 或輪詢|	內建支援 Subscription|
|適用場景	|簡單、結構固定的 API	|需要靈活查詢、多對多關聯|
### 適用於
- REST 適合：簡單、標準化 API，像是小型應用、後台管理系統。
- GraphQL 適合：需要靈活查詢的應用，如前端需求多變的 行動應用、社交平台、電商系統。


## 延生工具
在專案中，會用到其他的工具來幫助我們更好的使用GraphQL

### Apollo GraphQL
**是一組用於構建GraphQL應用程序的工具**  
[Apollo GraphQL官網傳送門](https://www.apollographql.com/)  
  
用途：  
Apollo 是一個完整的 GraphQL 生態系統，包含：  
- Apollo Client（用於前端）
- Apollo Server（用於後端）

特點：
- Apollo Client：幫助 React、Vue、Angular 等前端框架輕鬆管理 GraphQL 查詢和快取。
- Apollo Server：提供後端 GraphQL 伺服器，可與 Express、NestJS、Koa 等後端框架整合。


### Hasura
**是一種連接到數據庫和微服務的開源引擎，並為其自動生成GraphQl API**  
[Hasura官網傳送門](https://hasura.io/)  
用途：  
Hasura 是一個 開源的 GraphQL 引擎，可以自動從 PostgreSQL（或其他支援的資料庫）生成GraphQL API，省去手寫 Resolver 的工作。  
  
特點：  
- 不需要手寫 GraphQL 伺服器，直接連接資料庫生成 API。
- 支援存取控制（Permissions），可以根據用戶權限來限制 API 存取。
- 適合快速開發後端，特別適用於 需要 GraphQL 但不想自己寫 Resolver 的開發者。

### Hasura vs Apollo

1. Hasura在GraphQL API之上提供了許多其他功能，例如對GraphQL訂閱的支持並在數據庫事件上觸發Webhooks。

2. Hasura允許我們在現有數據庫和微服務的頂部構建GraphQl API，而無需編寫任何後端代碼。這可以使使用GraphQL變得更容易，尤其是如果您已經熟悉現有數據模型。

3. 另一方面，Apollo更專注於提供用於構建基於GraphQL的應用程序的工具，例如用於從Frontend應用程序進行GraphQl查詢的客戶端庫和用於執行這些查詢的服務器。

4. 可以一起使用Hasura和Apollo來構建基於GraphQL的應用程序。在這種情況下，Hasura將提供後端GraphQL API，我們可以使用Apollo的客戶端庫和服務器來構建前端應用程序，並處理諸如緩存和性能優化之類的內容。


## 參考資源
[What is Hasura? What are the differences between Hasura and Apollo Graphql?](https://dev.to/furkangulsen/what-is-hasura-what-are-the-differences-between-hasura-and-apollo-graphql-40dk)