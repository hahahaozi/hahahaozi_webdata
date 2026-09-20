---
title: hexo从入门到炸机
all_minifier: true
abbrlink: f5f6960b
tags:
  - 教程
  - hexo
date: 2020-08-09 16:20:01
categories: 教程
---
# 引言  
  自从换完电脑重新开启网站后，发现好多在原来的 ~教程贴~ 心理描写帖里并不能完全的使我回忆起并且重现。所以我开了这篇真·教程贴，一方面可以帮助萌新 ~重新踩坑~ ，另一方面可以让我回忆起当时的Error并可以在其他网站/重开网站时进行重现。
[原教程贴](/posts/4c40f6bb/)

----

# 第一章：安装
  本章节依据此文章操作[hexo从零开始到搭建完整-爱吃面包的兰兰-博客园](https://www.cnblogs.com/visugar/p/6821777.html)
## 前期配置
首先需要安装[Git](https://gitforwindows.org/)和[Node Js](https://nodejs.org/en/)(直接点击链接即可进入官网)。安装Node Js时，win7及以下版本请安装LTS（即稳定版），win10可安装Current（即最新版）。win7安装14.7.0Current版本时可能会出现安装错误。

----

### 安装Git
安装Git时，一路回车即可。安装成功后，可进入
>运行（win+r）-cmd 

输入 `git version`
若显示

	git version x.x.x xxxxxxxx.x

即为安装成功。如果显示其他，则……我也不知道怎么办……毕竟我是一次安装成功的……

----

### 安装Node Js
安装Node Js时，**不能一路回车！**。在Custom Setup这一步选择Add to PATH。安装好后依据上述方法打开cmd，输入`path`此时会显示

	path=D:/…… 

(盘符及路径依据你的设置而定，此处只是演示）
输入`node -v`
会返回当前安装版本的版本号。

另附：如果path没有显示路径，则需要自己设置。具体如何设置，请自行百度。（但我当时一路回车，看也没看，看到要选择设置的时候已经安装完了。path仍然显示路径）

----

### 安装hexo
**此步之后不再使用cmd**
在你要储存数据的路径下新建一个文件夹，自定义命名。如果你已经新建了一个文件夹，直接跳过就好，毕竟禁止套娃。
比如我要在 `C:\website data` 存储数据，就直接在文件夹内右键，选择 `Git Bath Here` 直接cd到该文件夹下，就不用再一步步切换盘符cd过来了。
然后输入命令`npm i -g hexo`进行hexo的安装（1分钟左右）。输入`npm i hexo-server`安装服务命令。后输入`hexo -v`即可查看hexo版本。
输入`hexo init`进行初始化(时间较长，请耐心等待)，初始化后会出现多个文件夹。初始化成功后会显示

	INFO  Start blogging with Hexo!
这时打开文件夹，会发现好多文件/文件夹。下面列出文件/文件夹用途。

>node_modules：所有的配置及插件全部在内，**最重要的的一个文件夹。**
>scaffolds：存放模板
>source：存放写的文章
>themes：存放主题
>_config.yml ：可用记事本打开，网站配置。**重要的配置文件。**
>package.json ：可用记事本打开，网站配置。没有要求不用更改。
>package-lock.json ：可用记事本打开，网站配置。没有要求不用更改。

下面依次输入

	hexo clean
	会返回 INFO  Deleted public folder.
	hexo generate
	会返回 INFO  28 files generated in 1.29 s 当然 文件数量和时间是改变的。

这是返回你的本地文件夹，会发现多了几个文件夹
>public： 这个文件夹是你的网站整合后的样子，clean后会自己消失。
>db.json ：我也不知道这是啥……应该是缓存文件把。

这些里面的东西不要动。实际动了也没用……

----

## 初步认识
### 设置Github库
新建一个Github账号，有的略过。新建一个repository（理解为建立一个新项目），name的格式为`yourname.github.io`，其中`yourname`为你github的名称，必须遵守这个格式，不然会出错。
eg：我的github ID是hahahaozi，那我的库名就是`hahahaozi.github.io`.
下面选择Public，创建。

----

### 配置Git
回到bash，输入

	git config --global user.name "yourname"
	git config --global user.email "youremail"

其中`yourname`和`youremail`改成你自己的名字和邮箱。后输入

	ssh-keygen -t rsa -C "youremail@example.com

用来创建ssh。这当中的`youremail@example.com`改成你的邮箱。
cd到ssh

	cd ~/.ssh
	cat id_rsa.pub

这时屏幕上会显示出以`ssh-rsa`开头的一串混合字符串，将输出结果全部复制下来。

**注**：cd完后要返回根文件夹哦，不然后续操作你看到的就是一堆报错信息。

----

### 配置Github
打开个人中心-setting-SSH and GPG key。在ssh中添加刚刚创建的ssh。
返回bash，检查是否成功

	ssh -T git@github.com

----

### 初识
	hexo server
	会返回 INFO  Hexo is running at http://localhost:4000 . Press Ctrl+C to stop. 
此时打开任意浏览器，输入`http://localhost:4000`即可看到原始模板。按`Ctrl+C`即可关闭服务器。在Git中，`Ctrl+C`具有强行终止的效果。

----

### 上传至Github
打开_config.yml文件，滑到最下面找到`# Deployment`，将下方的

	deploy:
	type:

替换为

	deploy:
	type: git
	repo: https://github.com/YourgithubName/YourgithubName.github.io.git
	branch: master

其中repo内，`YourgithubName`改为你Github的名字。保存，关闭。

打开bash，安装上传的插件。

	npm install hexo-deployer-git --save

安装好后进行上传

	hexo clean
	hexo generate
	hexo deploy

中途会跳出Github的登录框，按要求登陆即可。这是打开`http://yourgithubname.github.io`就可以看到你的网站了！

----
## 网站配置文件

下面来讲解以下网站配置文件`_config.yml`内的设置及用处。
```yaml
	# Hexo Configuration
	## Docs: https://hexo.io/docs/configuration.html
	## Source: https://github.com/hexojs/hexo/
	
	# Site
	 title: Hexo
	 subtitle: ''
	 description: ''
	 keywords:
	 author: John Doe
	 language: zh-CN
	 timezone: ''
	
	# URL
	## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
	 url: http://yoursite.com
	 root: /
	 permalink: :year/:month/:day/:title/
	 permalink_defaults:
	 pretty_urls:
	 trailing_index: true # Set to false to remove trailing 'index.html' from permalinks
	 trailing_html: true # Set to false to remove trailing '.html' from permalinks
	
	# Directory
	 source_dir: source
	 public_dir: public
	 tag_dir: tags
	 archive_dir: archives
	 category_dir: categories
	 code_dir: downloads/code
	 i18n_dir: :lang
	 skip_render:
	
	# Writing
	 new_post_name: :title.md # File name of new posts
	 default_layout: post
	 titlecase: false # Transform title into titlecase
	 external_link:
	   enable: true # Open external links in new tab
	   field: site # Apply to the whole site
	   exclude: ''
	 filename_case: 0
	 render_drafts: false
	 post_asset_folder: false
	 relative_link: false
	 future: true
	 highlight:
	   enable: true
	   line_number: true
	   auto_detect: false
	   tab_replace: ''
	   wrap: true
	   hljs: false
	prismjs:
	   enable: false
	   preprocess: true
	   line_number: true
	   tab_replace: ''
	
	# Home page setting
	# path: Root path for your blogs index page. (default = '')
	# per_page: Posts displayed per page. (0 = disable pagination)
	# order_by: Posts order. (Order by date descending by default)
	index_generator:
	 path: ''
	 per_page: 10
	 order_by: -date
	
	# Category & Tag
	default_category: uncategorized
	category_map:
	tag_map:
	
	# Metadata elements
	## https://developer.mozilla.org/en-US/docs/Web/HTML/Element/meta
	meta_generator: true
	
	# Date / Time format
	## Hexo uses Moment.js to parse and display date
	## You can customize the date format as defined in
	## http://momentjs.com/docs/#/displaying/format/
	date_format: YYYY-MM-DD
	time_format: HH:mm:ss
	## updated_option supports 'mtime', 'date', 'empty'
	updated_option: 'mtime'
	
	# Pagination
	## Set per_page to 0 to disable pagination
	per_page: 10
	pagination_dir: page
	
	# Include / Exclude file(s)
	## include:/exclude: options only apply to the 'source/' folder
	include:
	exclude:
	ignore:
	
	# Extensions
	## Plugins: https://hexo.io/plugins/
	## Themes: https://hexo.io/themes/
	theme: alpha-dust
	
	# Deployment
	## Docs: https://hexo.io/docs/deployment.html
	deploy:
	  type: ''
```

以上就是配置文件的内容，下面解释一下需要个性化设置的。

	# Site
	 title: Hexo
	 subtitle: ''
	 description: ''
	 keywords:
	 author: John Doe
	 language: zh-CN
	 timezone: ''

这部需要设置的比较多，`title`填写你网站的名字。`another`填写你，当然留空也没问题。`lauguage`填写`zh-CN`。下面的`timezone`填写`Asia/Shanghai`。

----

	# URL
	## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
	 url: http://yoursite.com

这部分只要将网址改为你的网站就可以了。

----

	# Extensions
	## Plugins: https://hexo.io/plugins/
	## Themes: https://hexo.io/themes/
	theme: alpha-dust

----

这部分将主题改为你的主题名字，名字见`themes`里的名字。

	# Deployment
	## Docs: https://hexo.io/docs/deployment.html
	deploy:
	  type: ''

这部分要改的比较多。

	# Deployment
	## Docs: https://hexo.io/docs/deployment.html
	deploy:
	  type: git
	  repo: https://github.com/yourname/yourname.github.io.git
	  branch: master

其中`yourname`为你Github的名字

----

# 第二章：开始鼓捣
下面开始，才是噩梦的存在。毕竟上面没啥变化，下面的么……一个主题一个配置。我也就按照自己的主题配置了。我的主题是[Ayer](https://github.com/Shen-Yu/hexo-theme-ayer)。你也可以[通过此处](https://hexo.io/themes/)来选取你喜欢的主题进行设置。
## 安装主题
这次换个主题，我找到了一个充满未来科技感的主题[Alpha-dust](http://www.codeblocq.com/assets/projects/hexo-theme-alpha-dust/)。我这次就用这个主题进行演示（后来发现这个主题比较基础，没有那么多的插件，很简单的一个模板）。首先在bash中输入安装命令来下载主题

	git clone  https://github.com/klugjo/hexo-theme-alpha-dust主题/ alpha-dust

----

## 配置主题

安装好后我们需要去`_config.yml`文件内将

	# Extensions
	## Plugins: https://hexo.io/plugins/
	## Themes: https://hexo.io/themes/
	theme: landscape

改为

	# Extensions
	## Plugins: https://hexo.io/plugins/
	## Themes: https://hexo.io/themes/
	theme: alpha-dust

关于主题的名称可以去`themes`文件夹中寻找。在配置文件中# 后的内容仅仅起到注释作用（#后要有一个空格）。
根据教程提示，下面步骤的配置文件在`\themes\alpha-dust\_config.yml`中完成。关于menu的设置我没有看出有什么区别，可能是因为教程是4年前的，而配置文件经过了更新所以不用自己添加。
下面是图标的设置，这个主题提供了一个图标的来源，可以选择自己喜欢的图标，也可以自己制作符合图标规定的图标。下面的是关于页脚和版权的设定。需要注意的是在`Social Account`中，我们可以更改最后两项即`email_url: `和`rss_url: `其他的都是标定的网址。另外如果你不想在你的网站上标明可以直接删掉这一段。这是你启动本地预览可以发现你的网站已经切换了模板。

----

## 新文章

在bash中输入

	hexo new xxx

即可创建新文章，新文章在目录`\source\_posts\`中，以.md的格式存储的。关于md的软件及语法可以去百度一下，下面是一篇有关md语法的介绍。
[md语法](http://itmyhome.com/markdown/index.html)

----

## 创建分类及标签页
bash中输入命令

	hexo new page categories

即可创建分类页面。打开`/source/categories/index.md`文件，将以下内容复制进去。

	---
	title: categories
	type: "categories"
	layout: "categories"
	---

这样就创建了分类。

----

	hexo new page tags

即可创建标签页页面，打开`/source/tags/index.md`文件，将以下内容复制进去。

	---
	title: tags
	type: "tags"
	layout: "tags"
	---

这样就创建了标签页。

----

好了，到这里所有的基础就完成了。

----

# 第三章：插件
[hexo插件市场](https://hexo.io/plugins/)

这个章节在于介绍各种插件的设置与使用。插件是最繁琐的部分，因为插件之间总有着各种各样的冲突，不仅仅是程序上的冲突，还有大小和重叠的问题。我右下角的看板娘就是当时一点点去改的尺寸。

还是喜欢我的Ayer主题……那么接下来的插件就先按照Ayer里给的插件进行说明，再加上我自己用的插件。
[Ayer中文说明](https://shen-yu.gitee.io/2019/ayer/)

**注意：更改配置文件或安装插件前建议将当前可正常运行的版本进行整体备份，以便恢复时使用。当安装插件启用后导致崩溃的，可将配置文件中相应部分删除或将ture改为false解决（我遇到的的确如此）。如无效，建议直接可正常运行的版本直接覆盖。主要覆盖文件夹为node_modules**

## 配置主题文件
要想网站设的好，配置文件少不了。下面我就直接贴出Ayer网站列举的Ayer主题配置文件说明。[配置文件说明](https://shen-yu.gitee.io/2019/ayer/#%E4%B8%BB%E9%A2%98%E9%85%8D%E7%BD%AE)
注意，是**主题配置文件**，不是网站配置文件。

	# 侧边栏菜单
	menu:
	 主页: /
	 归档: /archives
	 分类: /categories
	 标签: /tags
	 旅行: /tags/旅行/
	 关于我: /about
	
	# 站点次标题和打字动效
	# https://github.com/mattboldt/typed.js
	subtitle:
	 enable: true  # 是否开启动效
	 text: 面朝大海，春暖花开  # 显示的文字
	 text2: 愿你一生努力，一生被爱   # 滚动播放，如果不需要可以留空
	 text3: 想要的都拥有，得不到的都释怀  # 最多支持三段文字
	 startDelay: 0   # 延迟时间
	 typeSpeed: 200  # 打字速度
	 loop: true  # 是否循环
	 backSpeed: 100  # 回退速度
	 showCursor: true  # 是否显示光标
	
	# 网站图标和侧边栏logo
	favicon: /favicon.ico
	logo: /images/ayer-side.svg
	
	# 封面配置
	# enable-是否启用封面；path-封面背景图；logo-封面logo
	cover:
	 enable: true
	 path: /images/cover1.jpg  # /source/images目录下附送多张精美壁纸，可任意更换
	 logo: /images/ayer.svg  # 如果不要直接设置成false
	
	# 页面顶部进度条  
	progressBar: true
	
	# 文章配置
	# 文章太长，截断按钮文字(在需要截断的行增加此标记：<!--more-->)
	excerpt_link: 阅读更多...
	# 如果你嫌每篇文章手动加more标记比较麻烦，又不想在首页全文显示，可以把excerpt_all设置成true，这样首页只会显示文章归档
	excerpt_all: false
	
	# 是否开启代码复制按钮
	copy_btn: true
	# 是否开启文章分享按钮
	share_enable: true
	# 国内的社交平台(If you are not in China, maybe you prefer to set:false)
	share_china: true
	# 文章分享文字
	share_text: 分享
	
	# 分页文字
	nav_text:
	 page_prev: 上一页
	 page_next: 下一页
	 post_prev: 上一篇
	 post_next: 下一篇
	
	# 文章页是否显示目录
	toc: true
	
	# 文章中的图片是否支持点击放大
	image_viewer: true
	
	# https://github.com/willin/hexo-wordcount
	# 是否开启字数统计(关闭请设置enable为false)
	# 也可以单独在md文件里Front-matter设置`no_word_count: true`属性，来自定义关闭字数统计
	word_count:
	 enable: true
	# 只在文章详情显示(不在首页显示)
	 only_article_visit: true
	
	# 打赏
	# 打赏type设定：0-关闭打赏； 1-文章对应的md文件里有reward:true属性，才有打赏； 2-默认开启所有文章均有打赏，如果有些文章你不需要，请在文章对应的md文件里设置no_reward:true
	reward_type: 2
	# 打赏wording
	reward_wording: '请我喝杯咖啡吧~'
	# 支付宝二维码图片地址，跟你设置logo的方式一样。比如：/images/alipay.jpg
	alipay: /images/alipay.jpg
	# 微信二维码图片地址
	weixin: /images/wechat.jpg

	# 版权声明
	# 版权声明type设定：0-关闭版权声明； 1-文章对应的md文件里有copyright: true属性，才有版权声明； 2-所有文章均有版权声明
	copyright_type: 2

	# 是否启用搜索
	search: true

	# RSS订阅(先安装hexo-generator-feed插件，再去博客根目录config进行配置)
	# 不想显示可以直接留空
	rss: /atom.xml

	# 是否启用黑夜模式开关
	darkmode: true

	# 动态背景效果: 0-关闭，1-动态线条(跟随鼠标)
	canvas_bg: 0

	# 自定义鼠标样式，直接替换/images/mouse.cur文件
	mouse:
	 enable: false
	 path: /images/mouse.cur

	# 鼠标点击效果：0-关闭，1-爱心，2-爆炸烟花，3-粒子烟花
	click_effect: 0

	# 页面宽度自定义（不建议修改，可能造成布局混乱），article_width文章宽度，sidebar_width侧边栏宽度
	layout:
	 article_width: 80rem
	 sidebar_width: 8rem
  
	# GitHub Ribbons-封面右上角的forkme，换样式直接在source/images目录下替换forkme图片
	github: 
	# (关闭请设置为false)
	 url: https://github.com/Shen-Yu/hexo-theme-ayer

	# 网易云音乐插件
	music:
	 enable: false
	 # 播放器尺寸类型(1：小尺寸、2：大尺寸)
	 type: 1
	 id: 22707008  # 网易云分享的音乐ID(更换音乐请更改此配置项)
	 autoPlay: true  # 是否开启自动播放

	# 访问量统计(不蒜子)
	busuanzi:
	 enable: true

	# 友盟cnzz统计(url填js代码src链接)
	cnzz:
	 enable: true
	 url: #

	# Google Analytics
	google_analytics: ''
	# 百度统计
	baidu_analytics: ''

	# Mathjax数学公式
	mathjax: true

	# Katex数学公式(allpost设置为false时只有头部设置math:true的文章才开启)
	# 需要更换hexo渲染器，npm un hexo-renderer-marked -S && npm i hexo-renderer-markdown-it-katex -S
	katex:
	 enable: false # true
	 allpost: true
	 copy_tex: false

	# 网站成立年份(默认为 2019，若填入年份小于当前年份，则显示为 2018-2019 类似的格式)
	since: 2020

	#是否显示页脚信息(建议保留，有助于本主题的推广)
	pageFooter: true

	#ICP备案信息尾部显示
	icp:
	enable: false
	url: 'http://www.beian.miit.gov.cn/' # 备案链接
	text: '浙ICP备88888888' # 备案信息

	# 评论：1、Valine(推荐)；2、Gitalk

	# 1、Valine[一款快速、简洁且高效的无后端评论系统](https://github.com/xCss/Valine)
	# 启用Valine必须先创建leancloud应用， 注册账号后获取 id|key 填入即可
	leancloud:  
	 enable: true
	 app_id: #
	 app_key: #
	# Valine配置(如果有些文章你想关闭评论，请在文章对应的md文件里设置no_valine:true)
	valine:
	 enable: true # 是否启用
	 avatar: monsterid # 头像样式(https://valine.js.org/avatar.html)
	 placeholder: 给我的文章加点评论吧~ # placeholder

	# 2、Gitalk(https://github.com/gitalk/gitalk)
	gitalk:
	 enable: false # true
	 clientID: # GitHub Application Client ID
	 clientSecret: # Client Secret
	 repo: # Repository name
	 owner: # GitHub ID
	 admin: # GitHub ID

下面说明一下各个配置的设置。

### 侧边框菜单
	# 侧边栏菜单
	menu:
	 主页: /
	 归档: /archives
	 分类: /categories
	 标签: /tags
	 旅行: /tags/旅行/
	 关于我: /about

这部分是关于你侧边框的设置，你可以任意更改名称，也可以任意增添。只要注意在设置完路径后通过bash创建新分栏即可。

----
### 首页动态效果
	# 站点次标题和打字动效
	# https://github.com/mattboldt/typed.js
	subtitle:
	 enable: true  # 是否开启动效
	 text: 面朝大海，春暖花开  # 显示的文字
	 text2: 愿你一生努力，一生被爱   # 滚动播放，如果不需要可以留空
	 text3: 想要的都拥有，得不到的都释怀  # 最多支持三段文字
	 startDelay: 0   # 延迟时间
	 typeSpeed: 200  # 打字速度
	 loop: true  # 是否循环
	 backSpeed: 100  # 回退速度
	 showCursor: true  # 是否显示光标

这部分是关于首页打字效果的设置。实际需要设置的就是三个text后面的汉字部分，如果不启用请将`enable: true`改为`enable: false`，对速度不满意也可以调整速度。配置文件中已经说明了各行的意义。

----
### 网站图标
	# 网站图标和侧边栏logo
	favicon: /favicon.ico
	logo: /images/ayer-side.svg

这部分是修改网站的图标，跟上面一样，如果有就替换掉。logo的地址：`\themes\hexo-theme-ayer\source\images` favicon的地址：`\themes\hexo-theme-ayer\source\`。

----
### 主页图片
	# 封面配置
	# enable-是否启用封面；path-封面背景图；logo-封面logo
	cover:
	 enable: true
	 path: /images/cover1.jpg  # /source/images目录下附送多张精美壁纸，可任意更换
	 logo: /images/ayer.svg  # 如果不要直接设置成false

这部分是关于封面的设置，同样你在`\themes\hexo-theme-ayer\source\images`下可以看到一堆图片，可以随意选择。如果要上传自己的图片也可以设置为相同尺寸和格式后导入该路径进行设置。

----
### 文章进度条
	# 页面顶部进度条  
	progressBar: true

这个就是显示阅读进度的小条条，不需要可以改为`false

----
### 文章缩略
	# 文章配置
	# 文章太长，截断按钮文字(在需要截断的行增加此标记：<!--more-->)
	excerpt_link: 阅读更多...
	# 如果你嫌每篇文章手动加more标记比较麻烦，又不想在首页全文显示，可以把excerpt_all设置成true，这样首页只会显示文章归档
	excerpt_all: false

如果关闭这项设置，在主页会显示部分内容，通过`<!--more-->`标记进行断页。如果关闭后文章内没有截断标记，则主页会显示全部内容。开启后主页只会显示标题，像我的主页一样，。

----
### 分享设置
	# 是否开启代码复制按钮
	copy_btn: true
	# 是否开启文章分享按钮
	share_enable: true
	# 国内的社交平台(If you are not in China, maybe you prefer to set:false)
	share_china: true
	# 文章分享文字
	share_text: 分享

这部分是关于分享的。`分享`二字可以自由发挥。

----
### 分页
	# 分页文字
	nav_text:
	 page_prev: 上一页
	 page_next: 下一页
	 post_prev: 上一篇
	 post_next: 下一篇

这部分是分页文字。

----
### 显示目录
	# 文章页是否显示目录
	toc: true
这个我也没搞懂是啥……可能是侧边框？

----
### 图片放大
	# 文章中的图片是否支持点击放大
	image_viewer: true

如果开启，图片可以以独立图层的方式展示出来。

----
### 文章字数统计
	# https://github.com/willin/hexo-wordcount
	# 是否开启字数统计(关闭请设置enable为false)
	# 也可以单独在md文件里Front-matter设置`no_word_count: true`属性，来自定义关闭字数统计
	word_count:
	 enable: true
	# 只在文章详情显示(不在首页显示)
	 only_article_visit: true

此部分是关于统计信息的设置，不用可以设置为`false`。另外，字数统计真的是字数统计，英文是不算的……本文2.5w字，这个才统计了8.3k……

----
### 打赏设置
	# 打赏
	# 打赏type设定：0-关闭打赏； 1-文章对应的md文件里有reward:true属性，才有打赏； 2-默认开启所有文章均有打赏，如果有些文章你不需要，请在文章对应的md文件里设置no_reward:true
	reward_type: 2
	# 打赏wording
	reward_wording: '请我喝杯咖啡吧~'
	# 支付宝二维码图片地址，跟你设置logo的方式一样。比如：/images/alipay.jpg
	alipay: /images/alipay.jpg
	# 微信二维码图片地址
	weixin: /images/wechat.jpg

如果你要开启二维码打赏功能，记得**更改路径下的二维码照片**，不然小钱钱可到不了你的手里哦~

----
### 文章版权声明
	# 版权声明
	# 版权声明type设定：0-关闭版权声明； 1-文章对应的md文件里有copyright: true属性，才有版权声明； 2-所有文章均有版权声明
	copyright_type: 2

版权声明。

----
### 搜索设置
	# 是否启用搜索
	search: true

启用搜索时需要安装搜索插件，不需要时请`false`。

----
### RSS订阅设置
	# RSS订阅(先安装hexo-generator-feed插件，再去博客根目录config进行配置)
	# 不想显示可以直接留空
	rss: /atom.xml

同样，需要插件支持。

----
### 黑夜模式
	# 是否启用黑夜模式开关
	darkmode: true

如果不启用直接`false`即可。

----
### 页面动态效果
	# 动态背景效果: 0-关闭，1-动态线条(跟随鼠标)
	canvas_bg: 0

即可以跟随鼠标晃动的线条……装饰效果。如果追求速度建议关闭，毕竟是个真·小破站。
刚刚开启试了试，在静态是会颤抖，看着特别难受。不建议开启。

----
### 鼠标样式
	# 自定义鼠标样式，直接替换/images/mouse.cur文件
	mouse:
	 enable: false
	 path: /images/mouse.cur

可以这是箭头的样式，你可以选择游戏内的，或者是各种奇奇怪怪的样子。

----
### 点击特效
	# 鼠标点击效果：0-关闭，1-爱心，2-爆炸烟花，3-粒子烟花
	click_effect: 0

鼠标点击后出现的特效。同样，追求速度的话不建议开启。

----
### 页面尺寸设置
	# 页面宽度自定义（不建议修改，可能造成布局混乱），article_width文章宽度，sidebar_width侧边栏宽度
	layout:
	 article_width: 80rem
	 sidebar_width: 8rem

这个设置没动过……乖乖听话。（乖巧.jpg）

----
### 首页绶带设置
	# GitHub Ribbons-封面右上角的forkme，换样式直接在source/images目录下替换forkme图片
	github: 
	# (关闭请设置为false)
	 url: https://github.com/Shen-Yu/hexo-theme-ayer

右上角的绶带图片（应该是，我没有更新。）

----
### 音乐插件设置（网易云）
	# 网易云音乐插件
	music:
	 enable: false
	 # 播放器尺寸类型(1：小尺寸、2：大尺寸)
	 type: 1
	 id: 22707008  # 网易云分享的音乐ID(更换音乐请更改此配置项)
	 autoPlay: true  # 是否开启自动播放

这是个神坑啊！网易云音乐插件！注意不能存放歌单ID，不能播放**有版权限制**的音乐。具体怎样查看音乐是否有版权？去网易云网页版找到你想播放的音乐，进入歌曲详细页，点击光碟下方`生成外链播放器`，如果不能生成则说明此歌曲不能播放。选择`iframe插件`，下方HTML代码框会自动生成代码。

	<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="//music.163.com/outchain/player?type=2&id=1376873330&auto=1&height=66"></iframe>

我们只需要

	type=2&id=1376873330

这一串，将`type=`后的纯数字填入配置文件中，将`id=`后的纯数字填入`id`后，这样就可以了。自动播放则是指打开网页是否自动播放。

#### 个人解决方法
我的Ayer版本还存在着分离的情况，在配置文件中只有是否启用网易云音乐，剩下的配置则是在`themes\hexo-theme-ayer\layout\_partial\music.ejs`文件中。以下是我的文件配置。

	<div id="music">
    <%# "bottom:120px; left:auto;position:fixed;  width:85%" %>
    <% var defaultHeight = theme.music.type == 1 ? '32' : '66'; %>
    <% var defaultIframeHeight = theme.music.type == 1 ? '52' : '86'; %>
    <iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="//music.163.com/outchain/player?type=2&id=1376873330&auto=0&height=66"></iframe>
	</div>
	
	<style>
    #music {
        position: fixed;
        right: 15px;
        bottom: 0;
        z-index: 998;
    }
	</style>


----
### 统计设置
	# 访问量统计(不蒜子)
	busuanzi:
	 enable: true

这部分是页脚的统计信息。

	# 友盟cnzz统计(url填js代码src链接)
	cnzz:
	 enable: true
	 url: #

这个好像是需要注册的，我就没有整。和上面的不蒜子都是统计客流量的插件。

	# Google Analytics
	google_analytics: ''
	# 百度统计
	baidu_analytics: ''

上面两个一个是谷歌的统计插件，一个是百度的统计插件。介于google的复杂设置就不进行说明，实际很简单。百度的……算了吧……

----
### 数学公式
	# Mathjax数学公式
	mathjax: true

该主题支持数学公式，只是我不会用……

	# Katex数学公式(allpost设置为false时只有头部设置math:true的文章才开启)
	# 需要更换hexo渲染器，npm un hexo-renderer-marked -S && npm i hexo-renderer-markdown-it-katex -S
	katex:
	 enable: false # true
	 allpost: true
	 copy_tex: false

跟上方一样，也支持公式，但需要按照说明额外安装插件。

----
### 网站年份
	# 网站成立年份(默认为 2019，若填入年份小于当前年份，则显示为 2018-2019 类似的格式)
	since: 2019

没啥说明。

----
### 页脚信息
	#是否显示页脚信息(建议保留，有助于本主题的推广)
	pageFooter: true

具体内容是页脚的`Powered by Hexo Theme Ayer`这串信息。

----
### ICP备案信息设置
	#ICP备案信息尾部显示
	icp:
	enable: false
	url: 'http://www.beian.miit.gov.cn/' # 备案链接
	text: '浙ICP备88888888' # 备案信息

这个没有就关了吧……别到时候被请喝茶了……

----
### 评论设置
	# 评论：1、Valine(推荐)；2、Gitalk

	# 1、Valine[一款快速、简洁且高效的无后端评论系统](https://github.com/xCss/Valine)
	# 启用Valine必须先创建leancloud应用， 注册账号后获取 id|key 填入即可
	leancloud:  
	 enable: true
	 app_id: #
	 app_key: #
	# Valine配置(如果有些文章你想关闭评论，请在文章对应的md文件里设置no_valine:true)
	valine:
	 enable: true # 是否启用
	 avatar: monsterid # 头像样式(https://valine.js.org/avatar.html)
	 placeholder: 给我的文章加点评论吧~ # placeholder

	# 2、Gitalk(https://github.com/gitalk/gitalk)
	gitalk:
	 enable: false # true
	 clientID: # GitHub Application Client ID
	 clientSecret: # Client Secret
	 repo: # Repository name
	 owner: # GitHub ID
	 admin: # GitHub ID

这个主题提供了两套评论系统，我用的是Gitalk，后面会在选修插件开一节讲如何设置。（这个也是个坑，要不是碰巧碰到一篇文章我都不知道http://和https://有这么大的区别）

---
### 目录
另外添加一个，如果你希望网站在右侧读取你本篇文章的并自动构建目录的话，在主题配置文件最下方加入以下代码

	# Toc
	 toc: true

如果你不希望某篇文章出现目录，则在该篇文章的头里加入

	no_toc: true

即可取消该篇文章的目录。

----

配置文件就是这些，下面开始讲各种插件的安装及应用。

## 必修插件

### hexo-generator-searchdb（搜索插件）
此插件是支持整个网站搜索的关键，必备插件。[hexo-generator-searchdb网址](https://github.com/theme-next/hexo-generator-searchdb)
打开bash，输入指令安装。

	npm install hexo-generator-searchdb

在网站配置文件中添加以下内容。注意是**网站配置文件而非主题配置文件**。

	# hexo-generator-searchdb
	search:
	 path: search.xml
	 field: post
	 format: html

不需要更改，直接粘贴到文件莫即可。

----
### hexo-abbrlink（文章唯一永久链接）
此插件是为应对各种乱窜和过长的网址而准备的。特别是涉及本地图片时，如果按照默认命名规则，网址不仅长，而且链接时会链接不上。拥有这个插件后会解决这个问题。[hexo-abbrlink网址](https://github.com/Rozbo/hexo-abbrlink)
打开bash，输入指令安装。

	npm install hexo-abbrlink --save

将网站配置文件中

	# URL
	## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
	permalink: 

改为

	# URL
	## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
	permalink: posts/:abbrlink.html

然后将以下部分贴入网站配置文件中。

	# abbrlink config
	abbrlink:
	  alg: crc32      #support crc16(default) and crc32
	  rep: hex        #support dec(default) and hex
	  drafts: false   #(true)Process draft,(false)Do not process draft. false(default) 
	# Generate categories from directory-tree
	# depth: the max_depth of directory-tree you want to generate, should > 0
	auto_category:
      enable: true  #true(default)
      depth:        #3(default)
      over_write: false 
	 auto_title: false #enable auto title, it can auto fill the title by path
	 auto_date: false #enable auto date, it can auto fill the date by time today
	 force: false #enable force mode,in this mode, the plugin will ignore the cache, and calc the abbrlink for every post even it already had abbrlink.

以下为实例演示，更改内容为`alg`和`rep`

----

	crc16 & hex
	https://post.zz173.com/posts/66c8.html
	
	crc16 & dec
	https://post.zz173.com/posts/65535.html
	
	crc32 & hex
	https://post.zz173.com/posts/8ddf18fb.html
	
	crc32 & dec
	https://post.zz173.com/posts/1690090958.html

----
可以根据需要进行更改。**局限性：crc16的最大帖子数是65535**

打开`\scaffolds\post.md`，对头进行更改，在头中加入

	abbrlink:

即可。
**需要注意**的是，新建一篇文章后是不会获得唯一连接的。如果你想要插入本地图片需要先`hexo generate`后文章头会自动生成唯一连接。

## 选修插件
### hexo-generator-feed（RSS订阅连接）
此插件用于生成RSS订阅连接，如果不需要可以略过。[hexo-generator-feed网址](https://github.com/hexojs/hexo-generator-feed)
打开bash，输入指令安装。

	npm install hexo-generator-feed --save

在网站配置文件中添加以下内容。注意是**网站配置文件而非主题配置文件**。

	#hexo-generator-feed
	feed:
	 type: atom
	 path: atom.xml
	 limit: 20
	 hub:
	 content:
	 content_limit: 140
	 content_limit_delim: ' '
	 order_by: -date
	 icon: icon.png
	 autodiscovery: true
	 template:

没有什么更改的，保存即可。

----
### hexo-blog-encrypt（文章加密）
此插件用于给文章设置密码，不需要可以略过。[hexo-blog-encrypt网址](https://github.com/MikeCoder/hexo-blog-encrypt)
打开bash，输入指令安装。

	npm install --save hexo-blog-encrypt

需要设置`\scaffolds\post.md`模板文件，打开后在头内加入

	password: 

这样创建新页面时会自动添加设置密码的属性，如果不设置密码可留空。

----
### hexo-helper-live2d（二次元看板娘）
此插件为装饰用插件，不需要可以略过。[hexo-helper-live2d网址](https://github.com/EYHN/hexo-helper-live2d)
打开bash，输入命令安装主程序

	npm install --save hexo-helper-live2d

之后打开**网站配置文件**添加以下代码

	# hexo-helper-live2d
	live2d:
	 enable: true
	 scriptFrom: local
	 pluginRootPath: live2dw/
	 pluginJsPath: lib/
	 pluginModelPath: assets/
	 tagMode: false
	 debug: false
	model:
	 use: live2d-widget-model-wanko
	display:
	 position: right
	 width: 150
	 height: 300
	mobile:
	 show: true
	react:
	 opacity: 0.7

这仅仅安装了主程序，我们还需要从网站上下载model来挑选我们喜欢的看板娘。[model网址](https://github.com/xiazeyu/live2d-widget-models)
同样在bash中输入命令下载。下载后的model储存在`node_modules`文件夹中。此时我们需要将上述代码中

	model:
	 use: live2d-widget-model-wanko

改为你下载的包的名字。之后就可以看到看板娘在你的主页盯着你啦！

----

### Gitalk（评论插件）
此插件实现了评论，原理为在网站的库下建立Issues。[Gitalk网址](https://github.com/gitalk/gitalk)
打开bash，输入命令安装。

	npm i --save gitalk

然后前往[GitHub Application](https://github.com/settings/applications/new)进行申请。域名和回调地址均填写你的网站的网址。**注意，网址需填写https://，否则回调失败不会登陆**

由于Gitalk已经在主题中配置好，我们只需要在主题配置文件中更改以下内容即可启用Gitalk。

	# 2、Gitalk(https://github.com/gitalk/gitalk)
	gitalk:
	 enable: false # true
	 clientID: # GitHub Application Client ID
	 clientSecret: # Client Secret
	 repo: # Repository name
	 owner: # GitHub ID
	 admin: # GitHub ID

`enable`来选择是否启用，`clientID`内填入GitHub Application Client ID.，`clientSecret`填入GitHub Application Client Secret.，`repo`填写你的网站域名，`owner`填写你Github的ID，`admin`也是填入你Github的ID。

----
### hexo-tag-bilibili（bilibili视频）
此插件可以让你将b站小视频转至你的网站。[hexo-tag-bilibili网址](https://github.com/Z4Tech/hexo-tag-bilibili)
打开bash，输入命令安装。

	npm install --save hexo-tag-bilibili

打开网站配置文件添加以下代码

	# hexo-tag-bilibili
	bilibili:
	  width: 452
	  height: 544

使用方式：在文章中添加以下代码

	{% bilibili [av_id] %}
	{% bilibili [av_id] [page] %}

单p时两种形式任意一种均可，但当多p是采用第二种形式。

----

# 尾声
好了，基本就是这些了。如果以后发现了新奇的小玩意还会开新章说明的~
更新时间：2020/8/12 10:27:39 