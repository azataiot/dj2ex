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

![image-20181129213002054](https://ws3.sinaimg.cn/large/006tNbRwgy1fxpf9io2bwj311u04qaaz.jpg)

![image-20181129213025979](https://ws1.sinaimg.cn/large/006tNbRwgy1fxpf9es3gaj30zs07aq4b.jpg)

### Django migrate

` python manage.py migrate`

![image-20181129213208297](https://ws3.sinaimg.cn/large/006tNbRwgy1fxpf9ai3srj30zm0kc786.jpg)

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

![image-20181129221219392](https://ws2.sinaimg.cn/large/006tNbRwgy1fxpf90zt5hj31490u0doy.jpg)

## Projects and Applications

### Creating an Application

Let's Create our first Django Application.

`python manage.py startapp blog`



![image-20181129221552392](https://ws4.sinaimg.cn/large/006tNbRwgy1fxpe0v4vgnj310a036wf2.jpg)

![image-20181129221605540](https://ws4.sinaimg.cn/large/006tNbRwgy1fxpf8ug6hyj30jy0se0uu.jpg)

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

![image-20181129224323842](https://ws2.sinaimg.cn/large/006tNbRwgy1fxpf8g61bgj30y005idgt.jpg)

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

![image-20181129225055256](https://ws3.sinaimg.cn/large/006tNbRwgy1fxpf88vxiij315u04a0u5.jpg)

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

``` python
from django.contrib import admin

# Register your models here.

from django.contrib import admin
from .models import Post

@admin.register(Post)
class PostAdmin(admin.ModelAdmin):
    list_display = ('title','slug','author','publish','status')
```

![image-20181129230424610](https://ws3.sinaimg.cn/large/006tNbRwgy1fxpffeer9kj31ae0g67gp.jpg)

![image-20181129230328656](https://ws1.sinaimg.cn/large/006tNbRwgy1fxpffikjqij32d60de40b.jpg)

Let's customize the admin model with some more opthions:

``` python
from django.contrib import admin

# Register your models here.

from django.contrib import admin
from .models import Post

@admin.register(Post)
class PostAdmin(admin.ModelAdmin):
    list_display = ('title','slug','author','publish','status')
    list_filter = ('status','created','publish','author')
    search_fields = ('title','body')
    prepopulated_fields = {'slug':('title',)}
    raw_id_fields = ('author',)
    date_hierarchy = 'publish'
    ordering = ('status','publish')

```

![image-20181129231837451](https://ws2.sinaimg.cn/large/006tNbRwgy1fxpfu6e1r3j31np0u0grr.jpg)

![image-20181130101753626](https://ws2.sinaimg.cn/large/006tNbRwgy1fxpywelo4ij31c80jkqff.jpg)

![image-20181130101854432](https://ws4.sinaimg.cn/large/006tNbRwgy1fxpyx6xxl2j31c80em462.jpg)

## Working with Querry and managers

![image-20181130102013165](https://ws3.sinaimg.cn/large/006tNbRwgy1fxpyymlbmjj31ay0j248k.jpg)

### Creating Objects

Open python shell with this command:

` python manage.py shell`

Then type the following commands:

![image-20181130102713801](https://ws2.sinaimg.cn/large/006tNbRwgy1fxpz5uurnlj31es0d0gob.jpg)

![image-20181130102800205](https://ws3.sinaimg.cn/large/006tNbRwgy1fxpz6nat69j31aa05441x.jpg)

` user = User.objects.get(username='yaakovazat')`

![image-20181130102947004](https://ws4.sinaimg.cn/large/006tNbRwgy1fxpzam2npfj31aw06a77j.jpg)

Post:

``` python
post = Post(title ='another post',
            slug = 'another-post',
            body = 'this is the body',
            author = user)
```

![image-20181130103611838](https://ws3.sinaimg.cn/large/006tNbRwgy1fxpzf64x2tj315s04qq46.jpg)

`post.save()`

![image-20181130103818999](https://ws1.sinaimg.cn/large/006tNbRwgy1fxpzhgl2bvj31dc0hu12x.jpg)

### Updating Objects

``` python
>>> post.title = 'New title'
>>> post.save()
```

![image-20181130104303263](https://ws4.sinaimg.cn/large/006tNbRwgy1fxpzmchae8j31am05aq4m.jpg)

![image-20181130104316308](https://ws1.sinaimg.cn/large/006tNbRwgy1fxpzmjmw60j31sr0u0ag2.jpg)

![image-20181130104347361](https://ws1.sinaimg.cn/large/006tNbRwgy1fxpzn2l7r5j319c08cn13.jpg)

## Retriving Objects

![image-20181130104523824](https://ws3.sinaimg.cn/large/006tNbRwgy1fxpzosggmjj31c00hgwq7.jpg)

![image-20181130104614591](https://ws1.sinaimg.cn/large/006tNbRwgy1fxpzplti8yj30oo04qmxg.jpg)

``` python
>>> all_posts = Post.objects.all()
>>> all_posts
<QuerySet [<Post:New title>, <Post: Add our first post>]>
```

## Using the filter method

![image-20181130104845804](https://ws2.sinaimg.cn/large/006tNbRwgy1fxpzsah8emj319i0c8wir.jpg)

`Post.objects.filter(publish__year=2017)`

![image-20181130105002706](/Users/yaakovazat/Library/Application Support/typora-user-images/image-20181130105002706.png)

` Post.objects.filter(publish__year=2017, author__username='yaakovazat')`

![image-20181130105157121](https://ws2.sinaimg.cn/large/006tNbRwgy1fxpzvn638ij319y0fqgp6.jpg)

![image-20181130105246080](https://ws1.sinaimg.cn/large/006tNbRwgy1fxpzweg49uj30pa044t93.jpg)

![image-20181130105543514](https://ws4.sinaimg.cn/large/006tNbRwgy1fxq0axw77fj31720cc0uj.jpg)

## Using Exclude

![image-20181130110726766](https://ws4.sinaimg.cn/large/006tNbRwgy1fxq0bpcj2oj31ek0hiwm5.jpg)

``` python
>>> from site_blog.models import Post
>>> try_exclude = Post.objects.filter(publish__year=2018)\
... .exclude(title__startswith='New')
>>> try_exclude
<QuerySet [<Post: Add our first post>]>
>>> 
```



![image-20181130111303060](https://ws1.sinaimg.cn/large/006tNbRwgy1fxq0hlble6j30ro06ojs2.jpg)

## Using Order_by()

``` 
>>> try_order = Post.objects.order_by('title')
>>> try_order
<QuerySet [<Post: Add our first post>, <Post: New title>]>
>>> 
```

![image-20181130111521944](https://ws1.sinaimg.cn/large/006tNbRwgy1fxq0jy8ujvj31fc0ccadm.jpg)

![image-20181130111553415](https://ws2.sinaimg.cn/large/006tNbRwgy1fxq0kk36n0j31d40asjun.jpg)

`Post.objects.order_by('-title')`

##  Deleting Objects

![image-20181130111652001](https://ws4.sinaimg.cn/large/006tNbRwgy1fxq0litpvlj319o0dktc2.jpg)

Note:

![image-20181130111717898](https://ws1.sinaimg.cn/large/006tNbRwgy1fxq0ly9colj31a80e2dkf.jpg)

## Creating Model Manager

![image-20181130111941356](https://ws3.sinaimg.cn/large/006tNbRwgy1fxq0ogs83fj31cm0l2n8q.jpg)

1. Add custom manager

Edit the models.py :

``` python

class PublishedManager(models.Manager):
    def get_queryset(self):
        return super(PublishedManager,self).get_queryset()\.filter(status='published')



class Post(models.Model):
    objects = models.Manager()
    published = PublishedManager()
```

## Building list and detail views

