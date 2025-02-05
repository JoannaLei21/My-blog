---
title: "資料庫"
date: "2024-12-11"
author: Joanna Lei
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/H.png
# images:
#   - /img/cover.jpg
categories:
  - Learning Code
tags:
  - Database
# nolastmod: true
draft: true
---

12/11 資料庫筆記

<!--more-->

## SQL

資料庫裡面會有很多 table
SQL (Structured Query Language)，結構化查詢語言 專門來管理資料的
SQL92 標準規範

## 目前比較大的

Oracle 壽險 銀行 大企業（最貴）  
MSSQL 微軟出的  
MySQL(被 Oracle 買走 ) fork-> MariaDB / PostgreSQL(效能好一些些，五倍)/ SQLite 開源（免費）

比較常用的 MySQL/ PostgreSQL 適合多人專案  
SQLite 比較適合個人使用，部署到線上多人使用會被鎖住（djanjo 裡的是預設這個）

## 資料庫 指令

`creeat database "file-name"` 新增資料庫  
`dorp database "file-name"`刪除資料庫（資料會完全砍掉，不要隨便用）

## 資料型態

文字：CHAR / VARCHAR (VARiable CHAR )/text
數字：integer/decimal
時間：date/datetime
BLOB =Binary Large OBject
其他型態

SQLite 沒有布林值型態
INT vs INTEGER =>是一樣的  
CHAR (用來放確定的長度，像是身分證字號) vs VARCHAR（當內容沒有寫滿，會省去上下的格子，在最前面加使用格子的長度，如地址會使用）

DDL 資料定義語言/ DML 資料操作語言（新增修改刪除）

insert into table
(欄位,) /省略不寫得話就是照每個欄位的順序填/
values
("值")

## READ

### 找帶有空值的資料

```
SELECT *
FROM heroes
WHERE age ISNULL
```

### 搜尋關鍵字 **like**

```
SELECT *
FROM heroes
WHERE description LIKE "背心%"
```

用%代表....
like 是精準比對，一般搜尋功能不會用 like 做搜尋，因為不確定使用這會如何下關件字  
elastic search 模糊搜尋（ web -> ES <-DB )

### 找中間

```
SELECT \*
FROM heroes
WHERE age BETWEEN 10 AND 25
```

### 找兩個條件 找 S 跟找 A

```
SELECT \*
FROM heroes
WHERE hero_level = "S" OR hero_level = "A"
WHERE hero_level IN ('s','A')

```

### 篩選條件

```
SELECT *
FROM heroes
WHERE hero_level <> "S" AND hero_level <> "A"
WHERE  hero_level NOT IN ('S','A')
```

## UPDATE

```
UPDATE heroes
SET age = 10, gender = 'F'
WHERE id = 25
```

更新的指令順序是固定的，**一定要記得下 WHERE，不然會全部更改**

## DELETE

```DELETE FROM  heroes
WHERE hero_level = 'C'
```

## 資料庫的強項在計算資料，有提供計算的語法

### 算件數

```
SELECT  COUNT(*)
From heroes h
WHERE  hero_level = "A"
```

### 分組

```
SELECT  hero_level, AVG(age)
From heroes
Group by hero_level
```

### 排序

```
SELECT *
From heroes
WHERE  hero_level = "S"
ORDER BY hero_rank DESC
```

ORDER 的指令在 WHERE 後面  
DESC 是反向，正向不用寫

### 限制資料的筆數＆做分頁

```
SELECT *
From heroes
LIMIT 10
OFFSET 10
```

OFFSET 0, 10, 20, 30 ->第一頁, 第二頁, 第三頁, 第四頁

## 不同表單之間的查詢

```
SELECT *
From monsters
WHERE kill_by = (
	SELECT id
	From heroes
	WHERE name = '埼玉'
  WHERE name LIKE '% N %'
)
```

## 多個表格的參照關係

## Pr Key 主鍵

是某個資料表的一個欄位（無限定型態，也可以多個欄位組合在一起，變成複合式 PK）
不可以是空的  
不會重複

### Forign Key 外部鍵：

是某個資料表的一個欄位  
參照到另一個 資料表的主鍵
目的：用來確認咁資料表的紀錄跟被對照到的表格資料是對的起來的
跟 Pk 不同，FK 不需要是獨一無二的

上面的兩個 KEY 主要在管理 資料完整性 data integrity

## 交集 Join

### inner join 交集

共有的

```
SELECT *
From t1
JOIN t2
ON t1.username = t2.name
```

### left join

以 from 表單為主，會列出為主的表單，參考的有一樣的會列出來

```
SELECT *
From t1
LEFT JOIN t2
ON t1.username = t2.name
```

```
SELECT h.name, m.name
From battle_histories bh
JOIN heroes h, monsters m
ON bh.hero_id = h.id AND bh.hero_id = m.id
```

### right join

django_debug_toolbar

## 面試題

資料庫的正規化

## SQL 注入 SQL injection

利用 SQL 的規則漏洞，填入讓程式判別為正確的指令，因而能正常登錄
被稱為駭客的填空遊戲
大部分的 model 會做一層保護，避免這樣的狀況
