移动应用
===

依靠习惯我们还将用Ionic 2继续创建hello,world。

hello,world
---

开始之前我们需要先安装Ionic的命令行工具，后来我们需要用这个工具来创建工程。

```bash
npm install -g ionic@beta
```

如果没有意外，我们将安装成功，然后可以使用``ionic``命令:

它自带了一系列的工具来加速我们的开发，这些工具可以在后面的章节中学习到。

```
Available tasks: (use --help or -h for more info)

   start  ..........  Starts a new Ionic project in the specified PATH
   serve  ..........  Start a local development server for app dev/testing
   platform  .......  Add platform target for building an Ionic app
   run  ............  Run an Ionic project on a connected device
   emulate  ........  Emulate an Ionic project on a simulator or emulator
   build  ..........  Build (prepare + compile) an Ionic project for a given platform.

   plugin  .........  Add a Cordova plugin
   resources  ......  Automatically create icon and splash screen resources (beta)
		      Put your images in the ./resources directory, named splash or icon.
		      Accepted file types are .png, .ai, and .psd.
		      Icons should be 192x192 px without rounded corners.
		      Splashscreens should be 2208x2208 px, with the image centered in the middle.

   upload  .........  Upload an app to your Ionic account
   share  ..........  Share an app with a client, co-worker, friend, or customer
   lib  ............  Gets Ionic library version or updates the Ionic library
   setup  ..........  Configure the project with a build tool (beta)
   io  .............  Integrate your app with the ionic.io platform services (alpha)
   security  .......  Store your app's credentials for the Ionic Platform (alpha)
   push  ...........  Upload APNS and GCM credentials to Ionic Push (alpha)
   package  ........  Use Ionic Package to build your app (alpha)
   config  .........  Set configuration variables for your ionic app (alpha)
   browser  ........  Add another browser for a platform (beta)
   service  ........  Add an Ionic service package and install any required plugins
   add  ............  Add an Ion, bower component, or addon to the project
   remove  .........  Remove an Ion, bower component, or addon from the project
   list  ...........  List Ions, bower components, or addons in the project
   info  ...........  List information about the users runtime environment
   help  ...........  Provides help for a certain command
   link  ...........  Sets your Ionic App ID for your project
   hooks  ..........  Manage your Ionic Cordova hooks
   state  ..........  Saves or restores state of your Ionic Application using the package.json file
   docs  ...........  Opens up the documentation for Ionic
   generate  .......  Generate pages and components
```

现在，我们就可以用第一个命令``start``来创建我们的项目。


```bash
ionic start growth-blog-app --v2
```

在这个过程中，它将下载Ionic 2项目的基础项目，并执行安装命令。

```
Creating Ionic app in folder /Users/fdhuang/repractise/growth-blog-app based on tabs project
Downloading: https://github.com/driftyco/ionic2-app-base/archive/master.zip
[=============================]  100%  0.0s
Downloading: https://github.com/driftyco/ionic2-starter-tabs/archive/master.zip
[=============================]  100%  0.0s
Installing npm packages...
```

然后到``growth-blog-app``目录，我们会看到类似于下面的内容：

```
.
├── README.md
├── app
│   ├── app.js
│   ├── pages
│   │   ├── page1
│   │   │   ├── page1.html
│   │   │   ├── page1.js
│   │   │   └── page1.scss
│   │   ├── page2
│   │   │   ├── page2.html
│   │   │   ├── page2.js
│   │   │   └── page2.scss
│   │   ├── page3
│   │   │   ├── page3.html
│   │   │   ├── page3.js
│   │   │   └── page3.scss
│   │   └── tabs
│   │       ├── tabs.html
│   │       └── tabs.js
│   └── theme
│       ├── app.core.scss
│       ├── app.ios.scss
│       ├── app.md.scss
│       ├── app.variables.scss
│       └── app.wp.scss
├── config.xml
├── gulpfile.js
├── hooks
│   ├── README.md
│   └── after_prepare
│       └── 010_add_platform_class.js
├── ionic.config.json
├── package.json
└── www
    └── index.html
```

在这2.0版本的Ionic，页面开始以目录来划分，一个页面路径下有自己的``html``、``js``、``scss``。

 - ``tabs``负责这些页面间跳转
 - ``theme``则负责系统相应样式的修改
 - ``config.xml``带有相应的Cordova配置
 - ``hooks``则对系统添加和编译时进行一些预处理
 - ``ionic.config.json``则是ionic的一些相关配置选项
 - ``package.json``则存放相应的node.js的包的依赖
 - ``www``目录用于存放出最后构建出来的内容，以及一些静态资源

由于Angular 2.0使用的是Typescript，所以在这里我们将用typescript进行展示，因此我们的执行命令变成~~：

```
ionic start growth-blog-app --v2 --ts
```

``--ts``表示使用的是``typescript``来创建项目，安装的过程是一样的，不一样的是后面写的代码。

执行相应的起serve命令，我们就可以开始我们的项目了：

```bash
ionic serve
```

这时候Ionic将做一些额外的事，才能启动我们的服务，如：

 - 删除``www/build``目录下的文件
 - 编译SASS到CSS
 - 编译文件到HTML
 - 编译字体
 - 等等

最后，它将启动一个Web服务，URL为[http://localhost:8100](http://localhost:8100)

```bash
  Running 'serve:before' gulp task before serve
  [20:59:16] Starting 'clean'...
  [20:59:16] Finished 'clean' after 6.07 ms
  [20:59:16] Starting 'watch'...
  [20:59:16] Starting 'sass'...
  [20:59:16] Starting 'html'...
  [20:59:16] Starting 'fonts'...
  [20:59:16] Starting 'scripts'...
  [20:59:16] Finished 'scripts' after 43 ms
  [20:59:16] Finished 'html' after 51 ms
  [20:59:16] Finished 'fonts' after 54 ms
  [20:59:16] Finished 'sass' after 738 ms
  7.6 MB bytes written (5.62 seconds)
  [20:59:22] Finished 'watch' after 6.62 s
  [20:59:22] Starting 'serve:before'...
  [20:59:22] Finished 'serve:before' after 3.87 μs

  Running live reload server: http://localhost:35729
  Watching: www/**/*, !www/lib/**/*
  √ Running dev server:  http://localhost:8100
  Ionic server commands, enter:
    restart or r to restart the client app from the root
    goto or g and a url to have the app navigate to the given url
    consolelogs or c to enable/disable console log output
    serverlogs or s to enable/disable server log output
    quit or q to shutdown the server and exit
  ionic $
```

接着，就可以打开相应的Web页面，如下图所示：

![Ionic Web预览界面](./images/ionic-web-view.jpg)

### 构建应用

由于Ionic是基于Cordova的，我们需要安装Cordova业完成后续的工作。

```bash
sudo npm install -g cordova
```

为了构建不同的平台的应用，我们就需要添加不同的平台，如:

```bash
ionic platform add android
```

上面的命令可以为项目添加Android平台的支持，过程如下面的日志所示：

```
Adding android project...
Creating Cordova project for the Android platform:
	Path: platforms/android
	Package: io.ionic.starter
	Name: V2_Test
	Activity: MainActivity
	Android target: android-23
Android project created with cordova-android@5.1.1
Running command: /Users/fdhuang/repractise/growth-blog-app/hooks/after_prepare/010_add_platform_class.js /Users/fdhuang/repractise/growth-blog-app
```

最近，再执行``run``就可以在对应的平台上运行，如:

```
ionic run android
```

博客列表页
---

现在，让我们来结合我们的博客APP，做一个相应的展示博客的APP。

### 列表页

在上一个章节里我们已经有了一个博客详细的API，我们只需要获取这个API并显示即可。不过，让我们简单地熟悉一下显示数据的这部分内容：

```html
<ion-navbar *navbar>
  <ion-title>博客</ion-title>
</ion-navbar>

<ion-content class="blog-list">
  <ion-item *ngFor="#blogpost of blogposts">
    <h1 *ngIf="blogpost">
      {{blogpost.title}}
    </h1>

    <p *ngIf="blogpost">
      {{blogpost.body}}
    </p>
  </ion-item>
</ion-content>
```

上面是一个基本的详情页的模板，其中定义了一系列的Ionic自定义标签，如：

 - <ion-navbar> 显示在导航栏中的内容
 - <ion-content> 显示APP的内容
 - <ion-item> 即将博客成每一项

而从上面的内容中，我们可以看到：我们在ngFor中遍历了blogposts，然后显示每篇文章的标题和内容。对应的代码也就比较简单了:

```javascript
import {Page} from 'ionic-angular';

@Page({
  templateUrl: 'build/pages/blog/list/index.html',
  providers: [BlogpostServices]
})
export class BlogList {
  public blogposts;

  constructor() {

  }
}
```

但是我们要去哪里获取博客的值呢，先我们我们看完改造后听BlogList的Controller：


```javascript
import {Page} from 'ionic-angular';
import {BlogpostServices} from '../../../services/BlogpostServices';

@Page({
  templateUrl: 'build/pages/blog/list/index.html',
  providers: [BlogpostServices]
})
export class BlogList {
  private blogListService;
  public blogposts;

  constructor(blogpostServices:BlogpostServices) {
    this.blogListService = blogpostServices;
    this.initService();
  }

  private initService() {
    this.blogListService.getBlogpostLists().subscribe(
      data => {this.blogposts = JSON.parse(data._body);},
      err => console.log('Error: ' + JSON.stringify(err)),
      () => console.log('Get Blogpost')
    );
  }
}

```

我们初始化了一个blogListService，然后我们调用这个服务去获取博客列表。

```javascript
    this.blogListService.getBlogpostLists().subscribe(
      data => {this.blogposts = JSON.parse(data._body);},
      err => console.log('Error: ' + JSON.stringify(err)),
      () => console.log('Get Blogpost')
    );
```    

当我们获取到数据的时候，我们就解析这个数据，并将这个值赋予blogposts。如果这其中遇到什么错误，就会显示相应的错误信息。

现在，让我们创建一个获取博客的服务：

```
import {Inject} from 'angular2/core';
import {Http} from 'angular2/http';
import 'rxjs/add/operator/map';

export class BlogpostServices {
  private http;

  constructor(@Inject(Http) http:Http) {
    this.http = http
  }

  getBlogpostLists() {
    var url = 'http://127.0.0.1:8000/api/blogpost/?format=json';
    return this.http.get(url).map(res => res);
  }
}
```

### 详情页

```bash
ionic g page blog-detail --ts
```

```bash
app/pages/blog-detail/
├── blog-detail.html
├── blog-detail.ts
└── blog-detail.scss
```

修改``app.ts``添加Route:

```
const ROUTES = [
  {path: '/app/blog/:id', component: BlogDetailPage}
];

@App({
  template: '<ion-nav [root]="rootPage"></ion-nav>',
  config: {} 
})
@RouteConfig(ROUTES)
export class MyApp {
  rootPage:any = TabsPage;

  constructor(platform:Platform) {
    this.rootPage = TabsPage;
    this.initializeApp(platform)
  }


  private initializeApp(platform:Platform) {
    platform.ready().then(() => {
      StatusBar.styleDefault();
    });
  }
}
```

添加服务

```javascript

  getBlogpostDetail(id) {
    var url = 'http://localhost:8000/api/blogpost/' + id + '?format=json';
    return this.http.get(url).map(res => res);
  }
```  

添加Controller

```javascript
import {Page, NavController, NavParams} from 'ionic-angular';
import {BlogpostServices} from "../../services/BlogpostServices";

@Page({
  templateUrl: 'build/pages/blog-detail/blog-detail.html',
  providers: [BlogpostServices]
})
export class BlogDetailPage {
  private navParams;
  private blogServices;
  private blogpost;

  constructor(public nav:NavController, navParams:NavParams, blogServices:BlogpostServices) {
    this.nav = nav;
    this.navParams = navParams;
    this.blogServices = blogServices;

    this.initService();
  }

  private initService() {
    let id = this.navParams.get('id');
    this.blogServices.getBlogpostDetail(id).subscribe(
      data => {
        this.blogpost = JSON.parse(data._body);
        console.log(this.blogpost);
      },
      err => console.log('Error: ' + JSON.stringify(err)),
      () => console.log('Get Blogpost')
    );
  }
}
```



Profile
---

###Json Web Tokens

```
pip install djangorestframework-jwt
```

```
urlpatterns = patterns(
    '',
    # ...

    url(r'^api-token-auth/', 'rest_framework_jwt.views.obtain_jwt_token'),
)
```

```
constructor(http: Http, nav:NavController) {
  this.nav = nav;
  this.http = http;
  this.local.get('id_token').then(
    (data) => {
      this.user = this.jwtHelper.decodeToken(data).username;
    }
  );
}

login(credentials) {
  this.contentHeader = new Headers({"Content-Type": "application/json"});
  this.http.post(this.LOGIN_URL, JSON.stringify(credentials), {headers: this.contentHeader})
    .map(res => res.json())
    .subscribe(
      data => this.authSuccess(data.token),
      err => console.log(err)
    );
}

authSuccess(token) {
  this.local.set('id_token', token);
  this.user = this.jwtHelper.decodeToken(token).username;
}
```

```
logout() {
  this.local.remove('id_token');
  this.user = null;
}
```

Install Angular JWT

```bash
npm install angular2-jwt
```

### Profile

```
def list(self, request):
    search_param = self.request.query_params.get('username', None)
    if search_param is not None:
        queryset = User.objects.filter(username__contains=search_param)

    serializer = UserSerializer(queryset, many=True)
    return Response(serializer.data)
```

创建博客
---

权限管理

```python
SAFE_METHODS = ['GET', 'HEAD', 'OPTIONS']

class IsAuthenticatedOrReadOnly(BasePermission):
    """
    The request is authenticated as a user, or is a read-only request.
    """

    def has_permission(self, request, view):
        if (request.method in SAFE_METHODS or
            request.user and
            request.user.is_authenticated()):
            return True
        return False
class BlogpsotSerializer(serializers.HyperlinkedModelSerializer):
    class Meta:
        model = Blogpost
        fields = ('title', 'author', 'body', 'slug', 'id')


# ViewSets define the view behavior.
class BlogpostSet(viewsets.ModelViewSet):
    permission_classes = (permissions.IsAuthenticatedOrReadOnly,)
    queryset = Blogpost.objects.all()
    serializer_class = BlogpsotSerializer

```        


TODO
---

