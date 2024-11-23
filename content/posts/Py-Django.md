---
title: "Python-Django"
date: "2024-11-21"
author: Joanna Lei
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/django.png
# images:
#   - /img/cover.jpg
categories:
  - Learning Code
tags:
  - Python
# nolastmod: true
draft: false
---

使用 Django 框架建立網站

<!--more-->

## Django

Django 是什麼呢？在[Django 官網](https://www.djangoproject.com/ "前往Django官網")的介紹：

> Django 是一個高階 Python Web 框架，鼓勵快速開發和簡潔、務實的設計。它由經驗豐富的開發人員構建，解決了 Web 開發的大部分麻煩，因此您可以專注於編寫應用程序，而無需重新發 ​​ 明輪子。它是免費且開源的。

> Django is a high-level Python web framework that encourages rapid development and clean, pragmatic design. Built by experienced developers, it takes care of much of the hassle of web development, so you can focus on writing your app without needing to reinvent the wheel. It’s free and open source.

簡單來說就是一個框架，相較 Flasks 能處理更大型的專案。

### 安裝

(上課 11-21 上午最後半小時)  
\*開啟虛擬環之後，輸入下面的指令便可以安裝 Django (macOS)

```py
python -m pip install Django==5.1.3
```

### 建立專案

1.輸入下面的指令開啟專案：
**注意要在資料夾名稱後面加`.`才不會開在資料夾裡面**

```py
django-admin startproject mysite file-name .
```

2.文件裡面會生出一個檔案`manage.py` 執行它

```py
python manage.py
```

3.在終端機列出來的 list 可以看到一個 runserver，執行 runserver

```py
python manage.py runserver
```

4.成功執行的話會出現一段文字，裡面會有路徑`Starting development server at http://127.0.0.1:8000/`，如果`8000`這個 port 開啟不了話，我們可以自己指定一個 port 給它，用下面的指令執行：

```py
python manage.py runserver 8888
```

`8888`這個是自己設定的，也可以換別的數字。

5.cmd+click 進入網頁，成功連接的話會看到下面的綠色火箭
![成功頁面](https://dvmn.org/filer/canonical/1591095182/631/)

6.這步驟可以跳過，在設定改預設語言為中文，在`setting.py`裡找這個

```py
LANGUAGE_CODE = 'en-us' #預設
LANGUAGE_CODE = 'zh-Hant' #繁中
```

### 建立分頁

1.在`urls`裡的預設路徑

```py
urlpatterns = [
    path('admin/', admin.site.urls),
]
```

`'admin/'`代表網址列顯示的名字`http://127.0.0.1:8000/admin/`  
`admin.site.urls`表示這個頁面要**執行**什麼，為了方便管理，會拆出來放在另一個一資料夾

(上課 1121 下午)

2.設定自己的路徑

```py
urlpatterns = [
    path('/index', index),
]

from django.http import HttpResponse
#這個HttpResponse是傳送回應給瀏覽器看
def index(request):
   return HttpResoponse("index page")
```

3.把`def`拆出來放在另一個資料夾`views.py`方便日後做管理。  
`usrl.py`

```py
from django.contrib import admin
from django.urls import path
from .views import index

urlpatterns = [
    path('admin/', admin.site.urls),
    path('/index', index, name="index"),
]
```

`views.py`

```py
from django.http import HttpResponse

def index(resquest):
    return HttpResponse("Start Writting Your Resume")
```

4.建立 Template
在最外層新增一個`資料夾:Templates`，在`setting.py`裡把檔案掛到的`DIRS[]`這樣系統才會從這個資料夾裡面找檔案  
`setting.py`

```py
DIRS["Templates"]
```

在`views.py`設定`render`讓網頁渲染頁面  
`views.py`

```py
from django.http import HttpResponse
from django.shortcuts import render

def index(resquest):
    return render(request,"home.html")
```

`home.html`放在剛建立的`Templates`資料夾裡面

5.html 設定：

- ` <header>`重複志訓可以建立一個公版，之後使用 `{% extend "資料夾路徑" %}`匯入。
- 挖洞：在公版用`{% block "自己取名字" %}{% endblock %}`挖洞，之後的檔案在同樣的指令中放置要顯示的內容  
  `公版`

  ```html
  {% block "自己取名字" %} {% endblock %}
  ```

  `檔案`

  ```html
  {% block "自己取名字" %}

  <h1>XXXXX</h1>
  <p>nuo;bjkncdjfpenvjfl/e;nfvu oe'n jf/vfe</p>

  {% endblock %}
  ```

## MVC vs MTV

在軟體架構模式中，普遍使用 MVC 模式（Model–view–controller），它把軟體系統分為三個基本部分：模型（Model）、視圖（View）和控制器（Controller）。  
在這邊是由控制器（Controller）來決定使用者看的畫面。

### MVC

![MVC中文圖](https://www.infolight.com/news/Images/BOOK113/image001.png)
![MVC英文圖](https://media.geeksforgeeks.org/wp-content/uploads/20240704102850/MVC-Architecture.webp)

### MTV

而在 Django 裡的為 MTV 模式 (Modle-Template-View)，是由 Template 決定使用者看的畫面
![Django MTV](https://www.mropengate.com/2015/08/mvcdjangomtv.html)
兩者差別在看法不一樣，所以設計角度不一樣。

## 建立 app

一個專案裡面可以有很多個`app`應用程式（功能）

### 口訣：MTV+U

1.建立 app 指令：

```py
python manage.py startapp app_file_name
```

2.新增`urls.py`並建立 path

```py
from django.urls import path
from .views import home

urlpatterns = [
    path("",home),
]
```

這邊可以直接幫路徑取名字，方便之後再 html 連結時，可以快速的使用命名替代路徑作為連結的依據。

```py
app_name = "app_file_name"
urlpatterns = [
    path("",home, name="xxx"),
]
```

```html
<a herf=" {% url 'app_file_name:xxx'%}"></a>
```

3.在`views.py`建立

```py
from django.shortcuts import render

def home(request):
    return render(request,"app_file_name/home.html")
```

4.建立 template 資料夾，放 html 檔。  
放在 app 的`template資料夾`目前還沒有連動，要在`setting.py`裡將檔案掛在 APP 下

```py
INSTALLED_APPS = [
  "app_file_name"
]
```

5.建立網頁要渲染的 html 檔

6.在專案資料夾的`urls.py`加入 path

```py
from django.urls import path,include

path("app_file_name/", include("app_file_name.urls"))
```

使用`inclide`代表連接`app_file_name`資料夾裡`urls.py`的連結。

7.確定是否正確連接`http://127.0.0.1:8000/app_file_name/`，若是沒有，看錯誤訊息改正就可以完成。

### 執行步驟 list

基本的五步驟，若是有出現錯誤訊息，除了依據錯誤訊息改正之外，也可照下面步驟做確認

- M **"T"** V+U: 新增`Template資料夾`
- MT **"V"** +U: `views.py`定義要執行的內容
- MTV+ **"U"**: 設定路徑`path`
- app 登記在`setting.py`裡面的`INSTALLED_APPS`
- 在根目錄（最外層的`urls.py`）登記 app 入口路徑

## 路徑命名 REST

REST 全名 Representational State Transfer( 表現層狀態轉移)，統一的命名方式，他是一種設計風格，並不是一種標準。但目前業界普遍採用這種設計。

| 資源                                                  | GET                                                                                | PUT                                               | POST                                                                            | DELETE               |
| :---------------------------------------------------- | :--------------------------------------------------------------------------------- | :------------------------------------------------ | :------------------------------------------------------------------------------ | :------------------- |
| 一組資源的 URI，比如https://example.com/resources     | 列出 URI，以及該資源組中每個資源的詳細資訊（後者可選）。                           | 使用給定的一組資源替換當前整組資源。              | 在本組資源中建立/追加一個新的資源。 該操作往往返回新資源的 URL。                | 刪除**整組**資源。   |
| 單個資源的 URI，比如https://example.com/resources/142 | 取得指定的資源的詳細資訊，格式可以自選一個合適的網路媒體類型（比如：XML、JSON 等） | 替換/建立指定的資源。並將其追加到相應的資源組中。 | 把指定的資源當做一個資源組，並在其下建立/追加一個新的元素，使其隸屬於當前資源。 | 刪除**指定**的元素。 |

## 建立 Model

Model 主要在決定表單資料的框架。  
我們設計表單的架構，給使用者填入資料。

### Model

在`model.py`建立表格需要的欄位

```py
from django.db import models

class Resume (models.Model):
    title = models.CharField(max_length=50)
    skill = models.CharField(max_length=200)
    content = models.TextField(null=True)
    ccg = models.f
```

使用` .CharField``TextField `設定為文字欄位  
| 方法| 用途|參數/預設|
|:----|:-----|:----|
|.CharField()|文字輸入框|(max_length=50)|
|.TextField()|文字輸入區|(null=True)|
每個執行方法會有不同的預設，跑不動時可以看是不是需要的參數沒有放  
如果要設定必填(null=False)，讓使用者填有必要的就好。

### makemigration

當 modle 的框架建立好之後，在建立資料庫之前，必須先做 Migration（遷移）

```py
python manage.py makemigrations
```

執行完成會生出一個新的`migrations資料夾`裡面會紀錄所有執行 `makemigration`的步驟

```py
(.venv) Joanna@hanedahinase Django Practice % python manage.py makemigrations
Migrations for 'resumes':
  resumes/migrations/0001_initial.py
    + Create model Resume
```

這時候並還沒有執行，只是先建立描述檔。

在描述檔裡，會自動生成`id`

```py
 ('id', models.BigAutoField(
    auto_created=True,
    primary_key=True,
    serialize=False,
    verbose_name='ID'))
```

這個是系統為了抓資料，自動幫資料編號的指令

### migrate

1.建好描述檔之後，在執行`migrate`

```py
python manage.py migrate
```

2.這時候在根目錄的檔案`db.sqlite`裡面就會建好剛剛設定的 model
目前裡面的檔案是以位元組的方式呈現，要在 VS Code 裡面看到可讀的檔案，要加外掛`SQLite Viewer
`這樣點進檔案就可以看到東西了！

3.我們可以根據描述檔的編號，去復原動作

```py
python manage.py migrate app_file_name 0001
```

要小心在以建立資料庫的情況下，刪除欄位會將裡面的資料也一起刪除，所以刪除時要很小心。  
如果要看 migration 的狀態，可以執行`showmigration`查看列表

4.從終端機新增資料進去，看看是否設定都正確  
進到 Shell 裡新增資料：指令`python manage.py shell`

```py
>>> from resumes.models import Resumes
>>> Joanna = Resumes()
>>> Joanna.title = "CEO"
>>> Joanna.save()
```

---

# "edditing eara below"

## CRUD

### Creat 建立

1.在 html 設定表單

```html
form method="POST" action="{% url '路徑名稱'%}"></form>
```

`<form method="POST"`method 指用什麼方法`action="{% url 'resumes:new' %}"`action 指送到哪裡  
HTML 的 form 目前的版本只有`POST` `GET`兩種方法，如果沒有寫的話，預設是 get,對自己送

2.為防止 CSRF（Cross Site Request Forgery）跨站請求偽造 ，會需要 CSRF token，在檔案中的`form`插入指令

```html
<form>{% csrf_token %}</form>
```

這個指令會讓系統生成序號，確認這個送出表單是從本站被送出，沒有經過第三方傳送。

### Read 讀取

1.從`from action="{ url '接收路徑' }"`得到表單資料後，將表單寫入資料庫  
在`view.py`設定：

```py
def index(request):
    if request.POST:
        #準備寫入資料庫
        resume = Resume()
        resume.title = request.POST.get("title")
        resume.skill = request.POST.get("skill")
        resume.content = request.POST.get("content")
        resume.save()

        return HttpResponse("get information")
```

這時候從網頁新增的資料，就會在`db.sqlite`裡面出了。

2.接下來要讀取資料`views.py`，然後在頁面上顯示出來`index.html`。  
在`views.py`檔案

```py
def index(request):
    if request.POST:
     .
     .
     .
        return HttpResponse("get information")
    #讀取列表
    resumes = Resume.objects.all()
    return render(request,"index.html",{"resumes":resumes})
```

`Resume.objects.all()`抓出寫入 Resume 的所有物件  
`{"resumes":resumes}`字典
在`index.html`檔案

```html
<ul>
  {% for resume in resumes %}
  <li>{{ resume.title }}</li>
  {% endfor %}
</ul>
```

目前在畫面上可以看到資料 List 囉

3.建立一個新的頁面來顯示資料  
在`urls.py` 檔

```py
urlpatterns = [
  path("<int:resume_id>",file,name="file")
]
```

在`views.py` 檔，這邊避免亂數造成網頁壞掉，可以用`get_object_or_404`做個預防機制

```py
def file(request,resume_id):
  resume = get_object_or_404(Resume,id=resume_id)
    return render(request,"file.html",{"resume":resume})
```

建立`file.html`，用{{}}印出資料，再放到對應的 html 標籤裡

```html
<h1>履歷No.{{ reseme.id }}</h1>
{{ resume.title }} {{ resume.skill }} {{ resume.content }}
```

4.將 list 加入超連結，可以直連到頁面

```html
<a href="{% url 'resumes:file' resume.id %}">
  <li>{{ resume.title }}</li>
</a>
```

### Update 更新

在顯示已輸入資料的頁面中，增加更新的按鈕，並且連的一個新的頁面做更新。 1.在`file.html`檔中（顯示資料的頁面），幫按鈕家超連結，引導至更新的頁面

```html
<footer>
  <a href="{% url 'resumes:edit' resume.id %}"><button>編輯履歷</button></a>
</footer>
```

2.在`urls.py`中建立路徑 path

```py
 path("<int:resume_id>/edit",edit,name="edit")
```

3.在`views.py`中設定執行內容，基本上和`file`一樣。

```py
def edit(request,resume_id):
    resume = get_object_or_404(Resume,id=resume_id)

    return render(request,"edit.html",{"resume":resume})
```

4.再來建立`edit.html`，資料送回`file`，用`value="{{ resume.title }}`帶入之前填的資訊  
`textarea`的放在<textarea>內容這邊</textarea>

```html
{% extends "shared/layout.html"%} {% block "content" %}
<h1>修改履歷</h1>

<form method="POST" action="{% url 'resumes:file' resume.id%}">
  {% csrf_token %}<br />
  title <br />
  <input type="text" name="title" value="{{ resume.title }}" /><br />
  content <br />
  <textarea name="content">{{ resume.content }}</textarea>
  ...
  <button>更新</button>
</form>

{% endblock %}
```

5.最後`views.py`裡面設定`file`接收回傳的資訊

```py
def file(request,resume_id):
    resume = get_object_or_404(Resume,id=resume_id)

    if request.POST:
        resume.title = request.POST.get("title")
        resume.skill = request.POST.get("skill")
        resume.content = request.POST.get("content")
        resume.save()

        return redirect("resumes:index")

    return render(request,"file.html",{"resume":resume})
```

### Delete 刪除

1.在頁面加入刪除按鈕，並連結到刪除頁面
`file`

```html
<footer>
  <a href="{% url 'resumes:edit' resume.id %}"><button>編輯履歷</button></a>
  <a href="{% url 'resumes:delet' resume.id %}"><button>刪除履歷</button></a>
</footer>
```

2.到`urls.py`設定路徑

```py
 path("<int:resume_id>/delet",delet,name="delet")
```

3.到`views.py`設定執行`delet`

```py
def delet(request,resume_id):
    resume = get_object_or_404(Resume,id=resume_id)
    return render(request,"delet.html",{"resume":resume})
```

4.建立刪除頁面`delet.html`
**注意**POST 只能用表單執行，所以這邊的刪除需要用表單包起來。回傳到自己可以不用寫路徑`action=""`

```html
<h1>確認刪除履歷No.{{ resume.id }}</h1>
<footer>
  <a href="{% url 'resumes:file' resume.id %}"><button>取消刪除</button></a>

  <form method="POST" action="">
    {% csrf_token %}
    <br />
    <button>確認刪除</button>
  </form>
</footer>
```

5.在`views.py`設定`delet`接收到`POST`之後要做的事

```py
def delet(request,resume_id):
    resume = get_object_or_404(Resume,id=resume_id)

    if request.POST:
        resume.delete()
        return redirect("resumes:index")

    return render(request,"delet.html",{"resume":resume})
```

終於完成了!!!!!  
👏👏👏👏👏👏  
接下來要挑戰在 30 分鐘內完上面的步驟囉 😱
