# 장고 프로젝트 만들기

[1. 기본 세팅](#기본-세팅)

[2. ARTICLES](#articles-만들기)

​	[1) INDEX](#article-index)

# 기본 세팅

1) 가상환경

   ```python
   python -m venv venv
   ```

2) 인스톨

   ```python
   pip install -r requirements.txt
   ```

3) 프로젝트, 앱 만들기

   ```python
   django-admin startproject crud .
   python manage.py startapp articles
   python manage.py startapp accounts
   ```

4) settings.py

   ```python
   # INSTALLED_APPS에 추가
       'articles',
       'accounts',
       'django_extensions',
       
   # BASE templates 경로 추가
   'DIRS': [BASE_DIR / 'templates',],
       
   # 한글로 설정
   LANGUAGE_CODE = 'ko-kr'
   TIME_ZONE = 'Asia/Seoul'
   
   # 커스텀 유저로 만듬
   AUTH_USER_MODEL = 'accounts.User'
   ```

5) project url 연결

   ```python
   from django.urls import path, include
   urlpatterns = [
       path('admin/', admin.site.urls),
       path('articles/', include('articles.urls')),
       path('accounts/', include('accounts.urls')),
   ]
   ```

6) 각각의 앱에 templates/앱이름 , urls.py, forms.py 만들기

# ARTICLES 만들기

## ARTICLE INDEX

1. urls

2. views

3. templates

   