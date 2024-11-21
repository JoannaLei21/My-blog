---
title: "Basic knowledge- Terminal"
date: "2024-11-21"
author: Joanna Lei
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/terminal.PNG
# images:
#   - /img/cover.jpg
categories:
  - Learning Code

tags:
  - Basic knowledge
# nolastmod: true
draft: false
---

## 終端機指令集合區 🥷

<!--more-->

### 終端機是什麼

在古老的時代~~喂！！～～電腦很貴，不像現在幾乎每個人都有電腦可以用。公司內部通常會有一台大型的電腦主機，其它人要使用這部電腦就是自己拿螢幕跟鍵盤去接，然後在上面做事情，這些末端的操作設備便統稱之「終端機」。  
終端機本身通常不是一部電腦，它沒有運算能力，僅用來顯示資料及輸入資料所有的計算都是在主機上處理的。  
[上面文句擷取自-為你自己學 Git](https://gitbook.tw/chapters/command-line/command-line "前往")

![以前的終端機](https://cdna.artstation.com/p/assets/images/images/034/244/186/large/sergiusz-w-4-f.jpg?1611779462)

現在的終端機，在電腦上，是一個比網頁視窗小，黑黑的一片的視窗，它的 icon 者這樣
![終端機](https://help.apple.com/assets/65DFB7A79DFEC61A7A0517AC/65DFB7A793CD15C0410BA37D/zh_TW/d94aa1c4979b25e9ffbda97fcbae219a.png)

認真說，在沒學寫程式之前，對它有莫名的恐懼感，雖然它上面的符號感覺有點賣萌，但總覺好像輸入錯什麼電腦就會爆炸之類的 😶‍🌫️  
接觸之後發現，就算輸入錯什麼，頂多它不會理你而已，只能說人對未知的東西，第一時間的感知就是恐懼啊！

## 常用的指令們

好的又離題了，這篇只是想紀錄一下平常會用到的指令，因為還不太熟所以擠下來方便自己腦袋短路的時候可以來這邊抓資料，這邊皆以`ios`為主

### 基本

| 指令           | 說明               | 範例/註記          |
| :------------- | :----------------- | :----------------- |
| cd             | 切換目錄           | cd Desktop /到桌面 |
| pwd            | 取得目前所在的位置 |                    |
| clear          | 清除畫面上的內容   |                    |
| ls             | 列出目前的檔案列表 |                    |
| mkdir          | 建立新的目錄       |                    |
| touch          | 建立檔案           |                    |
| cp             | 複製檔案           |                    |
| mv             | 移動檔案           |                    |
| rm             | 刪除檔案           |                    |
| com + N        | 新增視窗           | 快捷鍵             |
| opt + Comd + I | 編輯背景色         | 快捷鍵             |

[mac 官方文件：終端機的快捷鍵](https://support.apple.com/zh-tw/guide/terminal/trmlshtcts/mac "前往官網")

### python

| 指令          | 說明                    | 範例/註記 |
| :------------ | :---------------------- | :-------- |
| which python  | 找到 python 在什麼地方  |           |
| which python3 | 找到 python3 在什麼地方 |           |
| python3       | 進入 REPL               | 會顯示>>> |
| exir()        | 離開 REPL               |           |
| ctrl + d      | 離開 REPL               | 快捷鍵    |

### pyenv

讓我們在同一台電腦安裝不同的 Python 版本，像是工具箱，管 Python。  
安裝 pyenv 不是安裝 python，如果專案有需求可以再安裝（自己目前沒有裝）
| 指令 | 說明 | 範例/註記 |
| :------- | :------ | :--- |
| pyenv -v | 查看版本 | |
| pyenv versions | 查看有哪些版本 | 若顯示*system 表示只有系統內建的版本|
| pyenv install --list | 查看有哪些版本可以安裝 | 只有數字的為 python|
| pyenv install 3.12.4 | 安裝 python 版本 | |
| pyenv shell 3.12.4 | 切換 python 版本 | 切好會在 versons 顯示*3.12.4|
| pyenv global 3.12.4 | 預設 python 版本 | 關掉終端機再開時會用的版本|

### venv

虛擬環境，可在各自的環境（檔案）裡裝需要的套件。  
管理套件。
| 指令 | 說明 | 範例/註記 |
| :------------------ | :----------- | :------------------ |
| python -m venv .venv | 載入內建虛擬模組 | 會自動新增一個資料夾 |
| source .venv/bin/activate | 進入虛擬環境 | 終端機名字前面會顯示(.venv) |
| pip list | 查看有裝的套件 | 會顯示 list 出來 |
| deactivate | 退出虛擬環境 | 會顯示 list 出來 |
| pip install xxx | 安裝 xxx 套件 | 依照套件給的名字安裝，會在 lib 資料夾裡面 |
| pip freeze | 列出有安裝的套件＆版本 | |
| pip freeze > requirements.text | 輸出 list | |
| pip install -r requirements.text | 安裝 .text 裡面的套件 | -r 讀取，網站部署時會用到|

### poetry

虛擬環境，可在各自的環境（檔案）裡裝需要的套件。  
管理套件。
| 指令 | 說明 | 範例/註記 |
| :------------------ | :----------- | :------------------ |
| pipx install poetry | 安裝 | 官方文件指令 |
| poetry new file-name| 用 poetry 開新專案 | 會自動長很多東西出來 |
| poetry init| 手動開檔案後，cd 至檔案執行設定 | 會有設定，可全部 enter |
| poetry init -n| 手動開檔案後，cd 至檔案執行設定 | 全部預設 |
| poetry shell| 進入虛擬環境 | 終端機名字前面會顯示(fileName-pyVersion) |
| poetry add requests| 安裝套件 requests | |
| poetry remove requests| 移除套件 requests | |
| pip list | 查看有裝的套件 | 會顯示 list 出來 |
| poetry show | 查看有裝的套件 | 會顯示 list 出來 |
| poetry show --tree | 查看套件樹狀結構 | 會顯示 list 出來 |
| poetry env info | 查看套件裝到哪 | |
| poetry config --list | 查看 poetry 設定檔 | |
| poetry config virtualenvs.in-project true | 更改預設 | 安裝的套件會顯示出來 |
