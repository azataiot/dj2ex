# Builing a Blog Application

## Installing Django

### Installing Virtual Environtment

We will use Python 3.x version in this Course. A virtual environtment is necessary when you have different projects using different python versions. By means of python virtual environtment, each of your projects uses different environtment and you will never see some strange problems. Its highly recommended that you should create your project with a virtual environtment.

In python 3.7 We do it like this:

`python3.7 -m pyvenv venv`

Run the following command to activate the virtual environtment:

` source venv/bin/activate`

### Install Django with pip

`pip install django`

You can install django with certain version by:

`pip install django==2.0.5`

### Check Django installtion

```bash
(venv)  ~/git/dj2ex/blog   master ●  python
Python 3.7.1 (default, Nov  6 2018, 18:46:03)
[Clang 10.0.0 (clang-1000.11.45.5)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> import django
>>> django.get_version()
'2.1.3'
>>>
```

![image-20181129212501042](https://ws4.sinaimg.cn/large/006tNbRwgy1fxpcn0g4lqj30vk090juy.jpg)

If we can see versions like above, that means we are successfully installed the django (django 2.1.3)

### Creating our first project

`django-admin startproject blog`

![image-20181129212637960](https://ws4.sinaimg.cn/large/006tNbRwgy1fxpcmvsvdlj30j00be0tr.jpg)

![image-20181129212747486](https://ws2.sinaimg.cn/large/006tNbRwgy1fxpcmu510tj316i07umzc.jpg)

![image-20181129212910017](https://ws1.sinaimg.cn/large/006tNbRwgy1fxpcoyde05j30ne02ot8w.jpg)

![image-20181129212925509](https://ws1.sinaimg.cn/large/006tNbRwgy1fxpcoxoejdj311o0420t4.jpg)

![image-20181129212939528](https://ws1.sinaimg.cn/large/006tNbRwgy1fxpcors1rej312w05c0tm.jpg)

![image-20181129213002054](/Users/yaakovazat/Library/Application Support/typora-user-images/image-20181129213002054.png)

![image-20181129213025979](/Users/yaakovazat/Library/Application Support/typora-user-images/image-20181129213025979.png)

### Django migrate

` python manage.py migrate`

![image-20181129213208297](/Users/yaakovazat/Library/Application Support/typora-user-images/image-20181129213208297.png)

## Running the development server

`python manage.py runserver`

### Project settings

within the settings file ,we can configure our django project.,

![image-20181129220445272](https://ws2.sinaimg.cn/large/006tNbRwgy1fxpdpvws7oj31720fqjve.jpg)

![image-20181129220515174](https://ws1.sinaimg.cn/large/006tNbRwgy1fxpdptshtqj315y09mjwa.jpg)



![image-20181129220829157](https://ws4.sinaimg.cn/large/006tNbRwgy1fxpduqu1w5j315e09440d.jpg)

![image-20181129220859060](https://ws4.sinaimg.cn/large/006tNbRwgy1fxpdu5tg5jj30us02y0ti.jpg)

![image-20181129220923911](https://ws3.sinaimg.cn/large/006tNbRwgy1fxpdu3wlquj30um02it91.jpg)

![image-20181129220938611](https://ws1.sinaimg.cn/large/006tNbRwgy1fxpduvk08vj30zu05aaar.jpg)

![image-20181129220952397](https://ws1.sinaimg.cn/large/006tNbRwgy1fxpduvq5hbj30zu05aaar.jpg)

![image-20181129221219392](/Users/yaakovazat/Library/Application Support/typora-user-images/image-20181129221219392.png)

## Projects and Applications

### Creating an Application

Let's Create our first Django Application.

`python manage.py startapp blog`



![image-20181129221552392](https://ws4.sinaimg.cn/large/006tNbRwgy1fxpe0v4vgnj310a036wf2.jpg)

![image-20181129221605540](/Users/yaakovazat/Library/Application Support/typora-user-images/image-20181129221605540.png)

![image-20181129221731945](https://ws4.sinaimg.cn/large/006tNbRwgy1fxpe2niezxj31940mgq9q.jpg)

![image-20181129221744313](https://ws1.sinaimg.cn/large/006tNbRwgy1fxpe2t6yrlj317w0jetgm.jpg)

### Designing the blog data shema

A model is a python class subclasses the `django.db.models.Model`

![image-20181129221952892](https://ws2.sinaimg.cn/large/006tNbRwgy1fxpe57hv0fj31b40byqc5.jpg)

#### Define a Post Model

```python
from django.db import models

# Create your models here.

from django.utils import timezone

from django.contrib.auth.models import User

class Post(models.Model):
    STATUS_CHOICE=(
        ('draft','draft'),
        ('published',('published')),
    )
    title = models.CharField(max_length=250)
    slug = models.SlugField(max_length=250,unique_for_date='publish')
    author = models.ForeignKey(User,on_delete=models.CASCADE,related_name='blog_posts')
    body = models.TextField()
    publish = models.DateTimeField(default=timezone.now)
    created = models.DateTimeField(auto_now_add=True)
    updated = models.DateTimeField(auto_now=True)
    status = models.CharField(max_length==10,choices=STATUS_CHOICE,default='draft')


    class Meta:
        ordering = ('-publish',)

    def __str__(self):
        return self.title
```

![image-20181129223227991](https://ws1.sinaimg.cn/large/006tNbRwgy1fxpei8y5rnj318a0o2aib.jpg)

![image-20181129223241065](https://ws3.sinaimg.cn/large/006tNbRwgy1fxpeie1ng9j31610u0ncr.jpg)

![image-20181129223450499](https://ws2.sinaimg.cn/large/006tNbRwgy1fxpekoxwj4j30u00wf4ij.jpg)

### Activating the Application

``` python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'site_blog.apps.SiteBlogConfig'
```

### Creating and Applying migrations

![image-20181129224224118](https://ws3.sinaimg.cn/large/006tNbRwgy1fxpeshpz3aj319g0c8guu.jpg)

`python manage.py makemigrations site_blog`

![image-20181129224323842](/Users/yaakovazat/Library/Application Support/typora-user-images/image-20181129224323842.png)

Lets sync our data base with the new model:

` python manage.py migrate `

![image-20181129224525921](https://ws1.sinaimg.cn/large/006tNbRwgy1fxpey3ehjrj30u4088gmv.jpg)

## Create an Administrator site for our Models

![image-20181129224631976](https://ws4.sinaimg.cn/large/006tNbRwgy1fxpey4t0mwj30se07et9w.jpg)

### Creating a super user

`python manage.py createsuperuser`

![image-20181129224744162](https://ws2.sinaimg.cn/large/006tNbRwgy1fxpey1t2l3j30u4088gmv.jpg)

![image-20181129224958144](https://ws1.sinaimg.cn/large/006tNbRwgy1fxpf0dpifqj31fi0dck2h.jpg)

### Add our model to the administrator site

![image-20181129225055256](/Users/yaakovazat/Library/Application Support/typora-user-images/image-20181129225055256.png)

``` python
from django.contrib import admin

# Register your models here.

from django.contrib import admin
from .models import Post

admin.site.register(Post)
```

![image-20181129225228811](https://ws3.sinaimg.cn/large/006tNbRwgy1fxpf2znorsj31yi0n6mzr.jpg)

![image-20181129225430943](https://ws3.sinaimg.cn/large/006tNbRwgy1fxpf6cybjoj319m0isq4l.jpg)

### Customize the way how are models displayed.

![image-20181129225541952](https://ws2.sinaimg.cn/large/006tNbRwgy1fxpf6aljp7j318c05egnr.jpg)