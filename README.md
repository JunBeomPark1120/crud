# CRUD
`<>`는 변수를 의미하고 생성하고 싶은 이름을 설정할 수 있음.

1. 프로젝트 폴더 생성
2. 프로젝트 폴더로 이동 / vscode 실행
    - `.gitignore`, `README.md` 생성

3. django 프로젝트 생성
    - `<pjt-name>` 에는 생성하고 싶은 프로젝트의 이름을 작성함
```bash
django-admin startproject <pjt-name> .
```

4. 가상환경 설정
```bash
python -m venv venv
```

5. 가상환경 활성화
```bash
source venv/Scripts/activate
```

6. 가상환경에 django설치
```bash
pip install django
```

7. 서버 실행 확인
```bash
python manage.py runserver
```

8. 앱 생성
```bash
django-admin startapp <appname>
```

9. 앱 등록 => `setting.py`
```python
INSTALLED_APPS = [
    ...
    <app.name>
]
```

10. `url.py` => `views.py => `templates/.html` 순서로 코드를 작성

# Model

1. 모델 정의(`models.py`)
    - 모델의 이름은 기본적으로 단수형태

```python
from django.db import models

# Create your models here.
class Post(models. Model):
    title = models.CharField(max_length=100)
    content = models.TextField()
```

2. 번역본 생성
```bash
python manage.py makemigrations
```

3. DB에 반영
```bash
python manage.py migrate
```

4. SQL 스키마 확인
```bash
python manage.py sqlmigrate posts 0001
```

5. 생성한 모델 admin에 등록
```python
from django.contrib import admin
from .models import Post
# Register your models here.

admin.site.register(Post)
```

6. 관리자 계정 생성
```bash
python manage.py createsuperuser
```

## CRUD 로직 작성

### 1. Read

- 전체 게시물 출력
```python
def index(request):
    posts = Post.objects.all()
    
    context = {
       'posts' : posts,
    }
    return render(request, 'index.html', context)
```

- 하나의 게시물 출력
```python
def index(request):
    posts = Post.objects.all()
    
    context = {
       'posts' : posts,
    }
    return render(request, 'index.html', context)
```
### 2. Create

- 사용자에게 입력 할 수 있는 폼을 제공
```python
def new(request):
    return render(request, 'new.html')
```

-사용자가 입력한 데이터를 가지고 DB에 저장하는 로직
```python
def create(request):
    title = request.GET.get('title')
    content = request.GET.get('content')
    
    post = Post()
    post.title = title
    post.content = content
    post.save()
    
    return redirect(f'/posts/{post.id}/')
```
### 3. Delete

-

### 4. Update