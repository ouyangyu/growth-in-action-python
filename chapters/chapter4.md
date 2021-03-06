更多功能
===

在Django框架中，内置了很多应用在它的"contrib"包中，这些包括：

 - 一个可扩展的认证系统
 - 动态站点管理页面
 - 一组产生RSS和Atom的工具
 - 一个灵活的评论系统
 - 产生Google站点地图（Google Sitemaps）的工具
 - 防止跨站请求伪造（cross-site request forgery）的工具
 - 一套支持轻量级标记语言（Textile和Markdown）的模板库
 - 一套协助创建地理信息系统（GIS）的基础框架

这意味着，我们可以直接用Django一些内置的组件来完成很多功能，先让我们来看看怎么完成一个简单的评论功能。


静态页面
---

添加到``INSTALLED_APPS``

```
INSTALLED_APPS = (
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'django.contrib.sites',
    'django.contrib.flatpages',
    'django.contrib.sitemaps',
    'django_comments',
    'rest_framework',
    'blogpost'
)
```


添加URL

```python
url(r'^pages/', include('django.contrib.flatpages.urls')),
```

添加中间件

``django.contrib.flatpages.middleware.FlatpageFallbackMiddleware``到``MIDDLEWARE_CLASSES``

数据库迁移

```
Operations to perform:
  Apply all migrations: contenttypes, auth, admin, sites, blogpost, sessions, flatpages, django_comments
Running migrations:
  Rendering model states... DONE
  Applying flatpages.0001_initial... OK
```

创建模板

```
{% extends 'base.html' %}
{% block title %}关于我{% endblock %}

{% block content %}
<div class="mdl-cell mdl-cell--12-col">

</div>
{% endblock %}
```

从后台添加URL

![admin-flatpages-create.jpg](images/admin-flatpages-create.jpg)

高级选项

![flatpages-advance-option.png](images/flatpages-advance-option.png)


评论功能
---

在早期的Django版本(1.6以前)中，Comments是自带的组件，但是后来它被从标准组件中移除了。因此，我们需要安装comments这个包：

```
pip install django-contrib-comments
```

再把它及它的版本添加到``requirements.txt``，如下所示：

```
django==1.9.4
selenium==2.53.1
fabric==1.10.2
djangorestframework==3.3.3
djangorestframework-jwt==1.7.2
django-cors-headers==1.1.0
django-contrib-comments==1.7.1
```

接着，将``django.contrib.sites``和``django_comments``添加到``INSTALLED_APPS``，如下:

```python
INSTALLED_APPS = (
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'django.contrib.sites',
    'django_comments',
    'rest_framework',
    'blogpost'
)
```

然后做一下数据库迁移我们就可以完成对其的初始化：

```
Operations to perform:
  Apply all migrations: contenttypes, admin, blogpost, auth, sites, sessions, django_comments
Running migrations:
  Rendering model states... DONE
  Applying sites.0001_initial... OK
  Applying django_comments.0001_initial... OK
  Applying django_comments.0002_update_user_email_field_length... OK
  Applying django_comments.0003_add_submit_date_index... OK
  Applying sites.0002_alter_domain_unique... OK
(growth-django)
```

然后再添加URL到urls.py:

```
url(r'^comments/', include('django_comments.urls')),
```

现在，我们就可以登录后台，来创建对应的评论，但是这是时候评论是不会显示到页面上的。所以我们需要对我们的博客详情页的模板进行修改，在其中添加一句:

```html
{% render_comment_list for post %}
```

用于显示对应博客的评论，最近我们的模板文件如下面的内容所示：

```
{% extends 'base.html' %}
{% load comments %}

{% block head_title %}{{ post.title }}{% endblock %}
{% block title %}{{ post.title }}{% endblock %}

{% block content %}
<div class="mdl-card mdl-shadow--2dp">
    <div class="mdl-card__title">
        <h2 class="mdl-card__title-text"><a href="{{ post.get_absolute_url }}">{{ post.title }}</a></h2>
    </div>
    <div class="mdl-card__supporting-text">
        {{post.body}}
    </div>
    <div class="mdl-card__actions">
        {{post.posted}} - By {{post.author}}
    </div>
</div>

{% render_comment_list for post %}

{% endblock %}
```

遗憾的是，当我们刷新页面的时候，页面报错了，原因如下所示：

![site_id_issue.jpg](images/site_id_issue.jpg)

我们还需要定义一个``SITE_ID``，添加下面的代码到``settings.py``文件中即可：

```python
SITE_ID = 1
```

然后，我们就可以从后台创建评论：

![create-comment-backend.jpg](images/create-comment-backend.jpg)

Sitemap
---

我们在之前的文章中提到过SEO的重要性，这里只是简单地对Sitemap的内容进行展开。

### 站点地图介绍

Sitemap译为站点地图，它用于告诉搜索引擎他们网站上有哪些可供抓取的网页。常见的Sitemap的形式是以xml出现了，如下是我博客的sitemap.xml的一部分内容：

```
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
<url>
  <loc>https://www.phodal.com/blog/mezzanine-add-new-page/</loc>
  <lastmod>2014-08-03</lastmod>
  <changefreq>Monthly</changefreq>
  <priority>0.2</priority>
</url>
</urlset>
```

从上面的内容中，我们可以发现它包含了下面的一些XML标签：

 - urlset，封装该文件，并指明当前协议的标准。
 - url，每个URL实体的父标签。
 - loc，指明页面的URL
 - lastmod（可选），内容最后的修改时间
 - changefreq（可选），内容的修改频率，用于告知搜索引擎抓取频率。它包含的值有：``always``、``hourly``、``daily``、``weekly``、``monthly``、``yearly``、``never``
 - priority（可选），范围是从0.0~1.0，搜索引擎用于对你网站在搜索结果的排序，即内部的优先级排序。需要注意的是如果你把所有页面的优先级设置为1，那么它就和没有设置的效果是一样的。

从上面的内容中，我们可以发现：

 > 站点地图能够提供与其中列出的网页相关的宝贵元数据：元数据是网页的相关信息，例如网页的最近更新时间、网页的更改频率以及网页相较于网站中其他网址的重要程度。 ——内容来自 Google Sitemap帮助文档。

就先这样简单地介绍了，接着我们就可以实战了。

### Sitemap实战


### 提交到搜索引擎

