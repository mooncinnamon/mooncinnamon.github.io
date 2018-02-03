Django URL관련 주석

Pycharm에서 Django 프로젝트를 만들다 보면 url.py 부분에 상당히 긴 주석을 볼 수 있다.

```
"""monitoring URL Configuration

The `urlpatterns` list routes URLs to views. For more information please see:
    https://docs.djangoproject.com/en/2.0/topics/http/urls/
Examples:
Function views
    1. Add an import:  from my_app import views
    2. Add a URL to urlpatterns:  path('', views.home, name='home')
Class-based views
    1. Add an import:  from other_app.views import Home
    2. Add a URL to urlpatterns:  path('', Home.as_view(), name='home')
Including another URLconf
    1. Import the include() function: from django.urls import include, path
    2. Add a URL to urlpatterns:  path('blog/', include('blog.urls'))
"""
```

무려 15줄에 이르는 긴 주석이다. 해석해보면

```
"""[프로젝트명] url 설정법

'urlpatterns' 리스트는 url을 view로 routing  합니다. 자세한 내용은 아래 url을 참조해 주세요.

	https://docs.djangoproject.com/en/2.0/topics/http/urls/

예시:

Funtinon Views:

1. from my_app import views 를 import 하세요.
2. urlpatterns에 URL을 추가하세요. ex) path( ' ', views.home, name='home' )

Class-bases view:

1. from opther_app.view import Home을 import 하세요.
2. urlpatterns에 URL을 추가하세요. ex) path( ' ', Home.as_view( ), name='home')

Including anoter URLconf

1. from django.urls import include, path 를 import function에 import 하세요.
2. urlpatterns에 URL을 추가하세요: path( ' blog/ ', include('blog.urls') )

"""
```



번역해보니 별 내용 없다. 일단 2.0으로 변경되면서 url 대신 path를 쓴다는 사실을 알 수 있다.

