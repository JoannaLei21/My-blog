---
title: "Line Pay Api串接"
date: "2024-12-21"
author: Joanna Lei
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/LinePay.png
# images:
#   - /img/cover.jpg
categories:
  - Learning Code
  - Job Hunting
  - My Coding Life
tags:
  - Project
# nolastmod: true
draft: flase
---

使用 Django 串接 Line Pay

<!--more-->

## 關於串接 Line Pay 這回事

### 使用 Postman？

很多資源介紹如何串 Line Pay Api，讓 Line Pay 在結帳頁面出現，並連接到消費者的 Line 帳號，連動 LinePay 進行付款。  
大部分的資源皆是透過 `Postman`來進行串接，基本的步驟很簡單，設置記個基本參數基本就可以搞定。
今天要介紹的，是使用`Django`來直接串接 Line Pay，涉事的東西稍微多一些。  
或許你會有疑問，為什麼有簡單的工具放著不用，難道 Django 不能串 Postman？  
這個問題我詢問了 Ai，答案是“可以”！但尚未實際驗證。那差別呢？來看 Ai 怎麼說

### 具體差別比較

|        功能        | 使用 Postman                 | 不使用 Postman                         |
| :----------------: | :--------------------------- | :------------------------------------- |
|    測試啟動時間    | 快速（幾分鐘即可測試）       | 需要設置前端或撰寫測試代碼，較耗時     |
|      重複測試      | 支援儲存請求並快速重複測試   | 重複測試需要多次操作或執行測試代碼     |
| 錯誤診斷與回應分析 | 提供即時可視化回應，方便檢查 | 需要檢查日誌或打印資料                 |
|      測試範圍      | 聚焦於後端 API 的行為        | 涵蓋整個系統，包括前端、後端與整合流程 |
|    開發進度需求    | 適合後端獨立測試             | 前後端需進一步整合後測試               |
| 持續測試自動化能力 | 不支援（需手動測試）         | 可透過撰寫代碼實現自動化測試流程       |

總結:

- 開發早期：Postman 是測試後端 API 的最佳工具，能快速測試並檢查回應，適合單獨測試後端邏輯。
- 開發後期：整合前端後，可進行全流程測試，不使用 Postman 更貼近用戶實際操作；同時建議撰寫單元測試或集成測試代碼，為長期維護提供保障。

所以雖然說使用 Postman 能省事一些，但身為一個目標百萬年薪的工程師，還是蠻值得了解一下原理自己寫 code 的，對吧～

## 串接前準備

在正式開始寫 code 之前，需要先準備好下面的必要資料

### 1.申請[Line Pay Sandbox](https://developers-pay.line.me/zh/sandbox)

- 申請完後，登入 Line Pay 輸入寄到 Email 的驗證碼
- 在左側選單中，從`管理付款連結` 點進 `管理連結金鑰`
- 點選查詢，並填入傳至 Email 的驗證碼
- 下方顯示出`channel ID`和`channel secret key`，建議先複製至`.env`，因為頁面過一段時間會自動登出，要再重輸帳密，小麻煩
  ![LinePayCreat](/images/LinePayCreat.png)

### 2.申請臨時伺服器[ngrok](https://ngrok.com/)

- 申請後，進行 Email 驗證並登入
- 在頁面左側有表單，找到第二行`Stepup & Installation`
- 選擇你的裝置，並按照順序跑指令，我使用 macOS，指令有三個:  
  1.安裝`brew install ngrok`  
  2.跑`ngrok config add-authtoken <your token>`  
  3.進入`ngrok http http://localhost:8080`
- 完成上面步驟，在終端機就會出現 ngrok 的介面
  ![nrgok](/images/ngrok.png)

## 開始串接

準備好之後，我們就可以開始了！
這邊會編輯的檔案有：

- `setting.py` 串接.env、HOSTS、CSRF
- `.env` 放置環境變數
- `view.py` 設定功能
- `urls.py` 設定路徑
- `checkout.htnl` 建立 Line 付款頁面，會連線到 Line 的系統
- `error.html` 建立付款失敗頁面，沒有連線成功時會出現

### 1.最簡單的 html

準備燒腦前，可以先把無腦的 html 給建立出來，會有兩個頁面，這邊先設定最簡單的架構，樣式可以之後調整。  
放置位置`/yourapp/templates/payment/xxx.html`

1.`checkout.htnl`

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <!-- 改tiltle -->
    <title>LINE Pay Checkout</title>
    <link rel="stylesheet" href="{% static 'dist/bundle.css' %}" />
    <script type="module" src="{% static 'dist/bundle.js' %}"></script>
  </head>
  <!-- 後面再加樣式 -->
  <body>
    <h1>LINE Pay 測試結帳</h1>
    <form method="POST">
      {% csrf_token %}
      <button type="submit">前往付款</button>
    </form>
  </body>
</html>
```

頁面長這樣，只有兩行字
![checkout.html](/images/checkout.png)

2.`error.html`

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <!-- 改tiltle -->
    <title>LINE Pay Error</title>
    <link rel="stylesheet" href="{% static 'dist/bundle.css' %}" />
    <script type="module" src="{% static 'dist/bundle.js' %}"></script>
  </head>
  <!-- 後面再加樣式 -->
  <body>
    <h1>付款失敗</h1>
    <p>{{ message }}</p>
  </body>
</html>
```

### 2..env 環境變數

這邊有些重要的 Key，我們不想公開，所以不會放上 git，
確定`.env`已經被加入`.gitignore`，如果有成功加入`.env`在目錄裡會呈現灰色

```py
#貼上剛剛在Line Pay 後台得到的，<>不用打
LINE_CHANNEL_ID= <你的channel id>
LINE_CHANNEL_SECRET_KEY= <你的channel secret_key>

#測試用的，大家都一樣
LINE_SANDBOX_URL=https://sandbox-api-pay.line.me
LINE_REQUEST_URL=/v3/payments/request

# 放剛剛ngrok第 3 點出現的路徑位置
HOSTNAME=127.0.0.1:8080
```

### 3.setting.py

```py

# 載入.env
import environ
env = environ.Env()
environ.Env.read_env()

ALLOWED_HOSTS = env('HOSTNAME')

#LINE PAY API 的 CSRF_TRUSTED_ORIGINS
CSRF_TRUSTED_ORIGINS = [f"https://{env('HOSTNAME')}"]
```

這邊如果有串其他的 API 或第三方服務，如 google 登入，在`ALLOWED_HOSTS = `可能會打架

- google 登入:`ALLOWED_HOSTS = os.getenv('ALLOWED_HOSTS', '*').split(',')`
- Line Pay :`ALLOWED_HOSTS = env('HOSTNAME')`

這個時候，我們可以這麼處理，來同時包含兩種設定

```py
# google登入：獲取 ALLOWED_HOSTS 的值，默認為 '*'
allowed_hosts_env = os.getenv('ALLOWED_HOSTS', '*').split(',')

# LINE PAY API 的
line_pay_hostname = env('HOSTNAME')

# 合併兩者的值
ALLOWED_HOSTS = allowed_hosts_env + [line_pay_hostname]
```

### 4.`urls.py` 設定路徑

```py
from django.urls import path
from .views import request_payment

app_name="你的app名字"
urlpatterns = [
    path('request/', request_payment, name='request_payment'),
]
```

### 5.`view.py` 設定功能

這邊對我來說是最複雜的地方，如果使用 Postman，在對應的位置放入需要的值就好，這邊我們需要自己設定

```py
#基本的
from django.shortcuts import render, redirect
from pathlib import Path

#line pay 會用到的：
import uuid
import json
import hmac
import hashlib
import base64
import environ
import requests

#連接.env變數
BASE_DIR = Path(__file__).resolve().parent.parent
env = environ.Env()
environ.Env.read_env()

```

會有兩個需要設定：`header`&`body`

1.設定`header`，官方文件有說 header 需要的東西，在這邊會需要幫這些資料加密
[官方文件](https://developers-pay.line.me/zh/online/pre-requisites)截圖：
![headerSetting](/images/headerSetting.png)
官網上有 JavaScrip 的程式碼，彈 Django 是使用 Python，所以我們來設定程式碼：

```py
#line pay API header
def create_headers(body, uri):
    #帶入在.env的資訊
    channel_id = env('LINE_CHANNEL_ID')
    secret_key = env('LINE_CHANNEL_SECRET_KEY')

    #生成隨機的UUID並轉為文字格式，為防止重複提交
    nonce = str(uuid.uuid4())
    #header 轉換成json格式
    body_to_json = json.dumps(body)

    # 組裝簽名
    message = secret_key + uri + body_to_json + nonce

    #轉二進制，後續雜湊時使用
    binary_message = message.encode()
    binary_secret_key = secret_key.encode()

    #雜湊，使用SHA256
    hash = hmac.new(binary_secret_key, binary_message, hashlib.sha256)

    #將hash轉為Base64編碼的字符串
    signature = base64.b64encode(hash.digest()).decode()

    #官方文件中設定的，把剛設定好的變數帶入
    headers = {
        "Content-Type": "application/json",
        "X-LINE-ChannelId":channel_id,
        "X-LINE-ChannelSecret":secret_key,
        "X-LINE-Authorization-Nonce": nonce,
        "X-LINE-Authorization": signature,
    }
    return headers

```

2.設定`body`

```py
#line pay API body
def request_payment(request):
    if request.method == "POST":

        # 設定訂單與付款資訊
        order_id = f"order_{str(uuid.uuid4())}"
        package_id = f"package_{str(uuid.uuid4())}"

        #設定商品資訊，會出現在Line Pay請款頁面資訊中
        payload = {
            'amount': 399,
            'currency': 'TWD',
            'orderId': order_id,
            'packages': [{
                'id': package_id,
                'amount': 399,
                'products': [{
                    'id': '1',
                    'name': '方案Ｂ超好揪',
                    'quantity': 1,
                    'price': 399,
                }]
            }],
            'redirectUrls': {
                'confirmUrl': f"https://{env('HOSTNAME')}/payment/confirm",
                'cancelUrl': f"https://{env('HOSTNAME')}/payment/cancel"
            }
        }

    # 發送 API 請求
        uri = env('LINE_REQUEST_URL')
        headers = create_headers(payload, uri)
        url = f"{env('LINE_SANDBOX_URL')}{uri}"
        response = requests.post(url, headers=headers, data=json.dumps(payload))

        # 根據狀態，處理回應
        if response.status_code == 200:
            data = response.json()
            if data['returnCode'] == '0000':
                return redirect(data['info']['paymentUrl']['web'])
            else:
                return render(request, "payment/error.html", {"message": data['returnMessage']})
        else:
            return render(request, "payment/error.html", {"message": f"Error: {response.status_code}"})

    return render(request, "payment/checkout.html")
```

## 測試

設定之後，就可以開 server，到前面設定的路徑去看頁面
![checkout.html](/images/checkout.png)

### 成功連接

按下`前往付款`，成功的話會進入下面的頁面（Line 系統頁面）
![connectLinePay.html](/images/connectLinePay.png)
掃描 QR Code 或是登入後，會進到付款頁面（Line 系統頁面）
![test](/images/line-test-checkout.jpg)

### 連接失敗

但如果按下`前往付款`，看到的是錯誤頁面，代表連線沒有成功，需要再看看設定哪邊有問題

成功之後就是來和其他的 app 做串接，下一篇在介紹囉
