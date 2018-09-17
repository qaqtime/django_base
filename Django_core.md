## Django的第一个案列

### 第一个引用template案列

关键文件路径：

E:\python\Lib\site-packages\django\django_demo\django_demo\settings.py

```
TEMPLATES = [

    {

        'BACKEND': 'django.template.backends.django.DjangoTemplates',

        'DIRS': [BASE_DIR+"/templates"],改处

        'APP_DIRS': True,

        'OPTIONS': {

            'context_processors': [

                'django.template.context_processors.debug',

                'django.template.context_processors.request',

                'django.contrib.auth.context_processors.auth',

                'django.contrib.messages.context_processors.messages',

            ],

        },

    },

]
```

#### 巨坑所在

> 这里'DIRS': [BASE_DIR+"/templates"],巨坑所在

```
INSTALLED_APPS = [

    'django.contrib.admin',

    'django.contrib.auth',

    'django.contrib.contenttypes',

    'django.contrib.sessions',

    'django.contrib.messages',

    'django.contrib.staticfiles',

    'oneblog'改处

]
```



E:\python\Lib\site-packages\django\django_demo\django_demo\urls.py

```
from django.contrib import admin

from django.urls import path

from oneblog.views import hello_view



urlpatterns = [

    path('admin/', admin.site.urls),

    path('hell/', hello_view)

]
```





E:\python\Lib\site-packages\django\django_demo\oneblog\views.py



```
from django.shortcuts import render

\# Create your views here.

def hello_view(request):

    return render(request,'hell_django.html', {

        'data': "Hello Django ",

    })
```



E:\python\Lib\site-packages\django\django_demo\templates\hell_django.html

<!DOCTYPE html>

```
<html lang="en">

<head>

    <meta charset="UTF-8">

    <title>Title</title>

</head>

<body>

    {{data}}

</body>

</html>


```

#### 快速建立项目：

但沒關係，可以使用指令的方式來建立，指令如下：

```
django-admin startproject django_demo（项目名称）
```

到django_demo文件夹中运行迷你服务器：

```
python manage.py runserver
```

127.0.0.1:8000即可看到



##### 大致主要图

![1537181017646](E:\python\Lib\site-packages\django\5_____djangoImg\1537181017646.png)



##### git官方大致流程

Views

請先在 templates 裡面新增一個 hello_django.html，並在裡面輸入下方程式碼 (下圖)

<!DOCTYPE html> <html lang="en"> <head>     <meta charset="UTF-8">     <title>Title</title> </head> <body>     {{data}} </body> </html>

![img](E:/YoudaoNote/qqAF77964FDFD312E20ABD490E2E6F36AC/3adc17f6f3f741709b257a7894e439db/2482e6a7067.jpeg)

hello_django.html 裡面的第 8 行，只是透過 views.py 傳值過來而已。

關於第 8 行 的用法，更多可以參考 [Django Templates](https://docs.djangoproject.com/en/1.10/ref/templates/)。

接著我們將 views.py 裡面新增下方程式碼 (下圖)

from django.shortcuts import render   # Create your views here. def hello_view(request):     return render(request, 'hello_django.html', {         'data': "Hello Django ",     }) 

![img](E:/YoudaoNote/qqAF77964FDFD312E20ABD490E2E6F36AC/542dac3c9e054f4480dc67da2e94f2ef/8342e6a7067.jpeg)

views.py 裡面的第 7 行，就是回傳給 hello_django.html 的資料。

注意，最後還必須設定 URLconf。

URLconf

請再將 urls.py 裡面增加一些程式碼，如下圖

from django.contrib import admin

from django.urls import path

from oneblog.views import hello_view



urlpatterns = [

    path('admin/', admin.site.urls),

    path('hell/', hello_view)

] 

![img](E:/YoudaoNote/qqAF77964FDFD312E20ABD490E2E6F36AC/dcb50c9e518a4f2ebd90ebe78f7a5477/9452e6a7067.jpeg)

簡單講，就是將 views.py import 進來 (第 18 行)，

並且設定他的 URL (第 22 行)

最後執行 Django ， 然後瀏覽 <http://127.0.0.1:8000/hello/>

你應該會看到如下圖

这里的坑就是这样的：

第一个demo：

E:\python\Lib\site-packages\django\django_demo\django_demo\settings.py

这是一个巨坑：

'DIRS': [os.path.join(BASE_DIR, 'helloworld/templates')],