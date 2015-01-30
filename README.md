# 使用Bootstrap定制SharePoint网站页面

***本文相关代码： [https://github.com/shuishan-tech/sharepoint.withbootstrap]
(https://github.com/shuishan-tech/sharepoint.withbootstrap)***

***QQ群：413575985***

> 本文涉及以下三方面内容：
> 
> * 定义及推送母版页
> * 定义及推送网站页面
> * 页面中使用Bootstrap前端框架 

最近遇到一些SharePoint开发圈里的朋友，特别是刚接触SharePoint开发不久的朋友，总在问一个相同的问题：如何自定义SharePoint的页面？看似一个很简单的问题，但是问题如果再往深层次挖掘，提问者一般说来是想问：

- 如何能让一个SharePoint页面看起来不那么像SharePoint页面？
- 如何能定制一个漂亮现代的SharePoint网页？
- 如何能定制一个母版页（MasterPage）？
- 如何让SharePoint页面更互联网化？
- ……

以上看是围绕自定义页面扩展出来的的各种问题，在了解了原理之后，其实也没有复杂到哪儿去。

首先了解一下SharePoint对页面的分类：

1. 网站页面
	>并不存在于服务器上某个物理路径，是通过IIS调用SharePoint的服务器端机制可以访问的页面（文件内容可能位于数据库，位于Feature目录等）。

2. 应用程序页面
	>应用程序页面是服务器上磁盘上的物理文件，以SharePoint 2013为例，位于 %ProgramFiles%\Common Files\Microsoft Shared\web server extensions\15\TEMPLATE\LAYOUTS目录下。


接着，来看看一般进行SharePoint页面自定义有哪些途径。

1. 通过SharePoint Designer进行页面自定义。

	> 通过SharePoint Designer工具直接修改网站页面。
	>
	> 优点：学习成本低，快速，见效快。
	>
	> 缺点：只适合于修改已经存在的页面，不利于项目或者产品的部署分发。
2. 通过Visual Studio的SharePoint项目进行页面开发部署。
	>通过专业开发工具VS进行页面开发部署。
	
	>优点：一次开发，任意部署；理论上没有不可能实现的网页。
	
	>缺点：学习曲线陡；依赖专业的开发环境。

看到这儿您可能都要急了：啰嗦这么久，在SharePoint上究竟如何自定义一个网页？

嗯，之所以啰嗦是想把接下来要阐述的内容定个准确的目标：接下来要阐述的内容仅适用于***使用Visual Stuido进行SharePoint网站页面的自定义开发***。其实这才是真正的题目。

终于，我们来到了主题：如何自定义SharePoint网站页面？既然是网站页面，通俗说就是Web开发，那么逃不离几个元素：

* HTML
* CSS
* JavaScript

而SharePoint又是基于ASP.NET技术的微软产品，所以又逃不离以下N多的概念：

* MasterPage
* Page
* UserControl
* WebPart
* ……

我隐约记得我们是想做点儿漂亮的页面，如何能让网页更漂亮？我想列位心里都透亮透亮的：找个好美工，找个好前端，搞定！因为我们做SharePoint属于程序猿物种大类，而且可以划分为服务器端程序猿物种小类，向来和美工，前端被世人有意无意隔绝开（包括我们自己潜意识里，看到这里的SharePoint&前端大拿勿喷我，您属于超凡物种）。尘世间做漂亮网页无外乎这么几件事情：

* 合理的网页内容布局
* 合理的网页配色
* 合理的交互方式

这么几件事情，我们SharePoint程序猿究竟能不能？我的回答是：能。互联网在如今发展得如火如荼，借助一些优秀的前端开发框架，SharePoint程序猿也能做出美观大方的网页，下面我们请出今天的主角：Bootstrap。

## Bootstrap是谁？

Bootstrap是一个Web前端开发框架。

Bootstrap是Twitter开源的一套前端框架。

Bootstrap是最受欢迎的Web前端开发框架（没有之一，到目前2015-1-30为止，[Bootstrap](https://github.com/twbs/bootstrap)在github上是7.7w+ star, 2.9w+ forks）。

Bootstrap提供了一套CSS，JS帮助实现网页内容布局，页面配色，提供丰富的网页组件。在此基础上，有很多优秀的开发者贡献了自己的力量，在github上也开源了不少基于Bootstrap的页面布局，网页组件等。这些都是我们的福音。

Bootstrap主要包含三个方面的内容：

1. 全局CSS样式

	> 设置全局 CSS 样式；基本的 HTML 元素均可以通过 class 设置样式并得到增强效果，直白说就是页面的布局配色都帮您做好了，只需要在需要使用的地方设置css classname即可；还有先进的栅格系统。
2. 组件

	>组件其实就是一组Html元素+CSS组层的可复用的代码片段，Bootstrap包含了很多可复用的组件，包括字体图标、下拉菜单、导航、警告框、弹出框等更多功能。
3. JavaScript插件

	>jQuery 插件为 Bootstrap 的组件赋予了“生命”。可以简单地一次性引入所有插件，或者逐个引入到页面中。


## Bootstrap说：why me？

这节标题借用了Bootstrap的口吻说：why me？其实不然，这种前端大拿们做出来的框架才不理你，它的态度其实是：你用，或者不用，我就在这里……。所以，我们得凑上去，看看为什么要选择这个优秀的前端框架来增加SharePoint网站页面的用户体验？

1. 优秀的网页布局解决方案，这正好是不太熟悉前端开发的同学所欠缺的。通过Bootstrap的栅格系统，导航组件，页头页脚组件，能快速拼装一个页面布局。
2. 完善的全局CSS定义。各种Html元素都有对应的CSS定义，并且自成体系，轻松配置出合理的网页配色方案。
3. 丰富的网页组件。涵盖了常见的网页组件：下拉菜单，导航，弹出框等等，同时也是自成体系。
4. 强大的Javascript插件。框架本身提供了丰富的基于jQuery插件格式的组件，比如我们可以使用下面很轻松的定义一个下拉菜单```$('.dropdown-toggle').dropdown();```，并能获取客户端对象模型，以便使用其中的事件，方法等。同时，还有很多优秀的开发者基于此提供了更加丰富的插件，所谓只有想不到，没有做不到。
5. 跨平台支持，主流IE，Chrome，Firefox，Safari支持（SharePoint从2013开始，也已经做到多平台浏览器支持），妈妈再也不用担心我们陷入浏览器黑洞了。
6. 同时，Bootstrap框架从3.0版本开始，是一个移动优先的前端框架，也就是说，只要正确合理利用了框架，我们实现的网页是大小屏默认支持。使用浏览器打开[上海水杉网络有限公司网站](http://www.shuishan-tech.com)， 在手机浏览器打开同样的网址可以观察到，内容从PC端浏览器和手机端浏览器看上去差不多，但是内容排版上大相径庭，而页面真的就是只有一个，这就是响应式Web设计带来的好处。

它的好怎么说也说不完，我们还是在接下来使用的过程中慢慢体会。俗话说，是骡子是马，拉出来溜溜，光说不练是个假把式，下面我们就在实例案例中看看如何使用Visual Studio结合Bootstrap框架来进行SharePoint网站页面开发。


## 拉出来溜溜
> 这部分内容主要三个方面的重点：
> 
> 1. 使用Visual Studio定义并推送母版页。
> 2. 使用Visual Studio定义并推送网站页面。
> 2. Bootstrap风格页面呈现。
>
>开发环境使用Visual Studio 2013 + SharePoint 2013。

既然要溜溜，我们就来真格的：程序猿，一切以实际代码为准则。

***代码下载地址： [https://github.com/shuishan-tech/sharepoint.withbootstrap]
(https://github.com/shuishan-tech/sharepoint.withbootstrap)***

### 定义及推送母版页
> 关键点：使用SharePoint的Feature schema定义来推送母版页等。

1. 新建空模块（Module），起名字为MasterPages。
	
	成功后目录结构下包含以下文件： Elements.xml, simple.txt, 修改simple.txt为simple.master。
	
	打开Elements.xml, 按照以下配置修改其中内容：
	
	```
	<?xml version="1.0" encoding="utf-8"?>
	<Elements xmlns="http://schemas.microsoft.com/sharepoint/">  		<Module Name="MasterPages" Url="_catalogs/masterpage/bootstrap">    		<File Path="MasterPages\simple.master" Url="simple.master" Type="GhostableInLibrary"/>  		</Module>	</Elements>
	```
	> 说明：
	
	> Module节点上的Url属性值是指网站对应的存放母版页的路径，例子中的值`_catalogs/masterpage/bootstrap` 表示在网站的母版页存放路径下创建一级目录，名字叫做`bootstrap`。
	
	>File节点属性`Path`表示被推送文件在当前项目中得路径，例子中的`MasterPages\simple.master`, 前面`MasterPages`表示当前模块目录，由此可以引申，一个模块可以推送其他模块包含的文件。
	
	>File节点属性`Url`表示用户访问的文件名字，例子中和当前推送文件名一直，也可以不一致，根据需要设置。
	
	>File节点属性`Type`表示缓存文件的类型，由于存放母版页的是文档库，因此设置为`GhostableInLibrary`，把推送的文件作为文档库的一个文件缓存，也就是说会写入数据库，否则文件只是存在于Feature在服务器上的文件目录，SharePoint启动后缓存在内存里。浅显点说，如果`Type=Ghostable`，打开母版页文档库你看不到对应的文件项目，只有设置为`GhostableInLibrary`才能看到。
	
	>关于模块的具体说明请参考 [MSDN](https://msdn.microsoft.com/zh-cn/library/office/ms453137(v=office.14).aspx)。
   
2. 完善母版页内容。
	
	代码示例中创建了一个极度简单的母版页，可以说没有输出任何视觉内容，主要定义了三个PlaceHolder，用作html head区域重构，html title重构，以及html body内容填充。
	
### 定义及推送网站页面

1. 新建空模块（Module），起名为SitePages。参考`定义及推送母版页`第一步。
2. 完善网站页面内容。
	例子中我们创建了一个叫做`Demo.aspx`的网站页面，推送到网站的`SitePages`目录下。此页面中重要的四部分内容：
	* 引用母版页
		
		在`Demo.aspx`页面的头部，我们注意到此文件引用了上一步定义的母版页。

		```
		MasterPageFile="~/_catalogs/masterpage/bootstrap/simple.master"
		```
	* 注入html title
		
		```
		<asp:Content ID="ContentTitle" ContentPlaceHolderID="PlaceHolderPageTitle" runat="server">		    ShuiShan Bootstrap Demo		</asp:Content>
		```
	* 在html head区域注入资源引用
		
		```
		<asp:Content ID="ContentHead" ContentPlaceHolderID="PlaceHolderPageHead" runat="server">	 		<!-- Bootstrap Core CSS -->    		<link href="~/_layouts/15/ShuiShan.SharePoint.WithBootstrap/css/bootstrap.min.css" rel="stylesheet">    		<!-- Custom CSS -->    		<link href="~/_layouts/15/ShuiShan.SharePoint.WithBootstrap/css/modern-business.css" rel="stylesheet">    		<!-- Custom Fonts -->    		<link href="~/_layouts/15/ShuiShan.SharePoint.WithBootstrap/font-awesome-4.1.0/css/font-awesome.min.css" rel="stylesheet" type="text/css">    		<!-- HTML5 Shim and Respond.js IE8 support of HTML5 elements and media queries -->    		<!-- WARNING: Respond.js doesn't work if you view the page via file:// -->    		<!--[if lt IE 9]>        		<script src="https://oss.maxcdn.com/libs/html5shiv/3.7.0/html5shiv.js"></script>        		<script src="https://oss.maxcdn.com/libs/respond.js/1.4.2/respond.min.js"></script>    		<![endif]-->		</asp:Content>
		```
	* 在html body区域注入网页内容
		
		在body区域注入了真正视觉意义上的网页内容，使用浏览器访问此页面，body区域的内容会呈现在用户面前。

### 引入Bootstrap

在这里才开始介绍Bootstrap的引入，和传统的SharePoint开发一致，只需要把Bootstrap相关的资源文件存放在`Layouts`目录下即可，为了方便管理，不对同一服务器场的其他项目照成影响，在`Layouts`目录下创建了一个叫做`ShuiShan.SharePoint.WithBootstrap`的目录用来存放项目对应的资源文件。

我们在回过头看看代码中对于Bootstrap相关资源的引用

* html head区域，引用样式文件
	
	```
	<!-- Bootstrap Core CSS -->    <link href="~/_layouts/15/ShuiShan.SharePoint.WithBootstrap/css/bootstrap.min.css" rel="stylesheet">    <!-- Custom CSS -->    <link href="~/_layouts/15/ShuiShan.SharePoint.WithBootstrap/css/modern-business.css" rel="stylesheet">    <!-- Custom Fonts -->    <link href="~/_layouts/15/ShuiShan.SharePoint.WithBootstrap/font-awesome-4.1.0/css/font-awesome.min.css" rel="stylesheet" type="text/css">
	```
* html body区域，引用脚本文件，执行脚本

	```
	<!-- jQuery Version 1.11.0 -->    <script src="~/_layouts/15/ShuiShan.SharePoint.WithBootstrap/js/jquery-1.11.0.js"></script>    <!-- Bootstrap Core JavaScript -->    <script src="~/_layouts/15/ShuiShan.SharePoint.WithBootstrap/js/bootstrap.min.js"></script>    <!-- Script to Activate the Carousel -->    <script>    $('.carousel').carousel({        interval: 5000 //changes the speed    })    </script>
	
	```

## 后记
* 示例代码使用的是场解决方案，请谨慎使用。
* 部署解决方案包后，示例页面的访问地址： http://xxx.xxx/SitePages/Demo.aspx。
* 本文可以随意转载，但请留下文章引用地址。
* 从事SharePoint，但不仅限于SharePoint，相信将来企业应用和互联网应用会融合在一起，并一直致力于此。
* 交流QQ群：413575985
