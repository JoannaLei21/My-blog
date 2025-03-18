---
title: "Unsupported architecture"
date: "2025-03-17"
author: Joanna Lei
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/unsupported.png
# images:
#   - /img/cover.jpg
categories:
  - My Coding Life
tags:
  - Job
  - Basic knowledge
draft: false
---

## 不被支援的架構

<!--more-->
### 為什麼會有這篇

算是俗話說的，萬事起頭難嗎？哈哈哈  
為了避免未來再次遇到相同問題時不知所措，也希望幫助其他開發者，我決定整理這次的處理過程，記錄問題的成因與解決方案。  

### 遇到的問題
在要開啟專案的時候出現了錯誤，錯誤訊息非常簡短  
```js
error Unsupported architecture
```
這導致專案無法正常執行，無論是啟動伺服器還是運行開發環境，都被這個錯誤擋住。

### 錯誤原因

這個錯誤通常與系統架構與執行環境不匹配有關。經過排查，發現問題可能來自於以下幾個方面：

- Node.js 版本與系統架構不匹配：

我使用的是Mac M4處理器，系統是 arm64 架構，而有些套件可能是為 x86_64 編譯的。

或者，我當前使用的 Node.js 版本與專案需要的不一致，導致執行時發生錯誤。

---

- 依賴套件不支援當前架構：

某些 NPM 套件可能是針對特定架構編譯的，因此在 x86_64 環境下無法正常運行。

### arm64 x86_64
簡單的瞭解一下 `arm64` `x86_64` 是目前在電腦架構中，最主要被使用的兩個架構。

|特性|	ARM64 (AArch64)|	x86_64 (AMD64)|
|:--|:--|:--|
|架構類型	|RISC（精簡指令集）|	CISC（複雜指令集）|
|功耗	|低功耗、省電	|相對較高功耗|
|性能	|效率高、適合並行運算	|單核性能較強|
|應用場景|	手機、平板、伺服器、嵌入式設備	|桌機、筆電、伺服器|
|指令集	|簡單、固定長度指令|	複雜、可變長度指令|
|相容性	|舊版 ARM 可能不支援 64 位應用	|舊版 x86 可執行 64 位模式|
|廠商|	Apple（M 系列）、Qualcomm、Ampere、Broadcom|	Intel、AMD|
|代表 CPU	|Apple M1/M2/M3、高通 Snapdragon|	Intel Core、AMD Ryzen|


## 解決方法

1. 先讓電腦的使用架構，從 `arm64`切換到 `x86_64` 。  
2. 刪除原本 `arm64` 4架構下安裝的node version
3. 指定nvm使用 `x86_64` 安裝要使用的node version
4. 切換到剛安裝的version，並確認為 `x86_64` 版本
5. 啟動專案

### 安裝Rosetta
專案可能有部分依賴是針對 `x86_64` 架構，而你的 Mac 是 `Apple Silicon`（M 系列），因此系統要求透過 `Rosetta` 轉譯才能執行。

1.安裝 `Rosetta` 
```js
$softwareupdate --install-rosetta --agree-to-license
```
2.確認 Rosetta 是否可用
```js
$/usr/bin/arch
```
如果回傳 `arm64` ，代表你目前運行的是 `Apple Silicon` 原生架構。

如果你想要以 `x86_64`（Intel）模式運行某些應用程式，可以用這個指令：
```js
$arch -x86_64 zsh
```
### 查詢版本

首先先查看目前使用的架構為何？
```js
$node -p process.arch
```
會出現 `arm64` 或 `x86_64` ，需要在 `x86_64` 。

查詢已安裝的node版本
```js
$nvm ls
```
會顯示已安裝的版本，但不會特別註明是哪個架構的：
```js
       v16.20.2
       v18.20.7
->     v22.12.0
default -> 22 (-> v22.12.0)
iojs -> N/A (default)
unstable -> N/A (default)
node -> stable (-> v22.12.0) (default)
stable -> 22.12 (-> v22.12.0) (default)
lts/* -> lts/jod (-> N/A)
lts/argon -> v4.9.1 (-> N/A)
lts/boron -> v6.17.1 (-> N/A)
lts/carbon -> v8.17.0 (-> N/A)
lts/dubnium -> v10.24.1 (-> N/A)
lts/erbium -> v12.22.12 (-> N/A)
lts/fermium -> v14.21.3
lts/gallium -> v16.20.2
lts/hydrogen -> v18.20.7
lts/iron -> v20.19.0 (-> N/A)
lts/jod -> v22.14.0 (-> N/A)
```

查詢目前版本是給哪個架構使用的

```js
$which node | xargs file
```
會出現下面的訓息，在最後面會顯示 `arm64` 或 `x86_64` 。
apple
```js
/Users/your-user-name/.nvm/versions/node/v22.12.0/bin/node: Mach-O 64-bit executable arm64
```
x86
```js
/Users/your-user-name/.nvm/versions/node/v18.20.7/bin/node: Mach-O 64-bit executable x86_64
```

### 安裝x86_64版本
先將原本的版本卸載，安裝之後再切換過去
```js
$nvm uninstall 18
$nvm install 18 --arch=x86_64
$nvm use 18
```


### 重新安裝專案依賴

刪除node並重新安裝
```js
$rm -rf node_modules package-lock.json
$yarn install
```

必要時也可清快取
```js
$yarn cache clean
```

## 還是有問題

### 沒裝到x86_64版本
在過程中，我使用指令，指定安裝 `x86_64` 架構使用的版本18
```js
$nvm install 18 --arch=x86_64
```
但是在安裝完成後，確認版本時
```js
which node | xargs file
```
顯示的卻是
```js
/Users/your-user-name/.nvm/versions/node/v22.12.0/bin/node: Mach-O 64-bit executable arm64
```
恩？怎麼會這樣，明明只定了為什麼安裝下來的還是 `arm64` 架構使用的？

### 解決的方法
造成這個狀況，可能有兩個原因
1. 原本安裝的arm64版本沒被刪除  
我們只需要將原本的刪除再重裝一次，就OK，記得先切到另一個版本再刪除，不然會被卡住。  
例如：我正在使用18測試，但沒有成功，需要刪除18重裝，這時候需要先切換到16（或其他），才能將18刪除。

2. 系統預設 `arm64`  
因為系統預設就是 `arm64` 所以系統還是以預設可以使用的版下載，這時候需要確定系統切換到 `x86_64` 。

A.先刪除現有版本
```js
$nvm uninstall 18.20.7
```
B.以 `x86_64` 模式執行 `nvm install` 。使用 `Rosetta 2` 來執行 nvm 安裝
```js
$arch -x86_64 zsh -c "nvm install 18.20.7"
```
C.確認是否成功安裝 `x86_64` 版本
```js
$which node | xargs file
```
D.應該要顯示：
```js
/Users/your-user-name/.nvm/versions/node/v18.20.7/bin/node: Mach-O 64-bit executable x86_64
```
## 另一個錯誤
如果，在步驟B就出現下面的錯誤訊息，恭喜你跟我一樣XD
```js
zsh:1: command not found: nvm
```
這個錯誤的原因是，當你用 arch -x86_64 zsh -c "nvm install 18.20.7" 啟動 x86_64 環境時，nvm 沒有被載入。這通常是因為 nvm 只在 arm64 的 shell session 中載入，而 x86_64 的 shell session 沒有載入 nvm 的環境變數。

有兩個解決方法
1. 在 `x86_64` 環境內手動載入 `nvm`

A.開啟 `x86_64` 終端
```js
$arch -x86_64 zsh
```
這時候已經進入 `x86_64`
B.手動載入 `nvm`
```js
$export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
```
C.安裝 Node.js 18.20.7（x86_64 版本）
```js
$nvm install 18.20.7
```
D.確認版本
```js
$which node | xargs file
```

---

2. 在 `Rosetta 2` 環境內開啟新終端  
如果你經常需要在 x86_64 環境下使用 Node.js，建議開啟一個 完全使用 Rosetta 2 的終端來執行所有操作。
  
A. 開啟 x86_64 Terminal
B. 前往 Finder ➝ 應用程式 ➝ 工具程式 ➝ Terminal (終端機)
C. 右鍵 ➝ 取得資訊
D. 勾選 使用 Rosetta 2 開啟
E. 重新開啟終端，然後再安裝 Node.js：
```js
$nvm install 18.20.7
```
這樣未來你每次開啟這個終端時，都會自動以 x86_64 模式運行，避免 nvm 版本不符的問題。

## 小結
