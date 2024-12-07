---
title: "Git"
date: "2024-11-30"
author: Joanna Lei
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/H.png
# images:
#   - /img/cover.jpg
categories:
  - Learning Code

tags:
  - Basic knowledge
# nolastmod: true
draft: true
---

用 Git 管理檔案

<!--more-->

## Git 是什麼

## 基本指令

| 指令              | 用途                           | 補充                                  |
| :---------------- | :----------------------------- | :------------------------------------ |
| git init          |                                |                                       |
| git status        | 狀態確認                       |                                       |
| git log           |                                |                                       |
| git reflog        | 操作記錄                       | 記錄所有 head 的移動                  |
| git add           |                                |                                       |
| git commit        |                                |                                       |
| git checkout      |                                |                                       |
| git switch        |                                |                                       |
| git branch        | 開分支（貼標籤紙）             | -b 開分支定指到它                     |
| git merge         | 合併                           |                                       |
| git rebase        |                                |                                       |
| git reset         | 變成 xx 的樣子                 | --mixed(預設)/--hard 三個參數 1:20:48 |
| ^                 | 在 X 的前一個                  |                                       |
| ~n                | 在 X 的前 n 個                 |                                       |
| git fetch         |                                |                                       |
| git pull          | 抓回來，並且合併（預設 merge） | = git fetch + auto git merge          |
| git pull --rebase | 抓回來，並且使用 rebase 合併   |                                       |
| git clone 路徑    | 下載網上的專案                 | 就不用下載 Download Zip               |

## 練習小遊戲

[線上練習](https://learngitbranching.js.org/?locale=zh_TW)

## 建立 SSH Key

[讓老師帶你做](https://www.youtube.com/watch?v=CeC_qyQHiCE)
