---
title: "VUE"
date: "2024-12-02"
author: Joanna Lei
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/H.png
# images:
#   - /img/cover.jpg
categories:
  - Learning Code
tags:
  - JavaScript

# nolastmod: true
draft: true
---

VUE

<!--more-->

`<script setup>` 在.vue 檔案裡面才有作用  
import { ref } from 'vue' 從 vue 匯入`ref`function ref 是一個監聽的作用
`v-model` vue 的指令 這個是最常用到的指令

## Vue 最大的特色

1.關注資料  
2.資料在畫面上的什麼地方

## 原生 JS 事件監聽的步驟

1.抓到他  
2.監聽他  
3.取值  
4.塞回去

## Vue 基本

1.監聽  
2.狀態  
3.迴圈

## 注意

1. `.value`放置位置

```vue
<script setup>
import { ref } from "vue";

const msg = ref("Hello World!");

const inputHandler = (event) => {
  msg.value = event.target.value;
};
</script>

<template>
  <h1>{{ msg }}</h1>
  <input @input="inputHandler" />
</template>
```

使用`msg.value`要放在`<script>`，不是放在`template`

2. `{{ n }}`不能放在屬性裡面

```
<input
value="{{ n }}"
@input="inputHandler" />
```

上面是錯誤的，正確的是下面

```
<input
v-bind:value=" n "
@input="inputHandler" />
```

3.自訂義的元件使用兩個以上的單字組合

`<style scope>`是指定樣式僅限於自己使用，

## 縮寫

- V-on : @ (事件)
- V-bind: 不用打，留`:`就好 (只讀取不回送資料/只拿不寫)
- V-model: (只讀取也回送資料/又拿又寫)

## 建立新的 vue 專案

`npm init vue@latest 專案目錄名稱`

## 差別

computed 和一般 function 雖然可以得到一樣的結果，但 computed 不用加()，且無法帶參數，只會執行一次。 通常情況下資料只會"只出不進“
function 需要加()`{{function()}}`，可以帶參數，並且會依照指令的次數執行。

另外一種方式：watch()
