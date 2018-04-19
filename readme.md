## github个人博客网站

[在线预览](在线预览 "https://lost-xming.github.io")  **旨在整理知识点和记录工作遇到的问题处理方法**

### 开通自己的github.io 博客步骤

github.io是完全基于github创建的，其本质上是在你的github账户下创建一个特殊的repo

![](http://image.wwlin.cn/github1.jpg)

下一步：

![](http://image.wwlin.cn/github2.jpg)

**注意：仓库的前缀名称 要与owner 名称相同 图中因为我已创建 才爆红**

### 把你创建的repo clone到本地


	$ git clone https://github.com/lost-xming/lost-xming.github.io.git lost-xming

>  编写简单的博客页面 

		$ cd lost-xming
		 
		$ echo "hello world" > index.html
		
		$ git add index.html
		
		$ git commit -m "Init commit"
		 
		$ git push origin master

此时 打开博客网站 https://lost-xming.github.io
	
	不出意外，你就可以看到你的hello world博客页面了。

## 选择一款jekyll的主题

	github.io默认采用Jekyll作为建站工具。
	Jekyll是一款当前火热的开源的静态网站建站工具，拥有非常庞大的使用群里和社区，
	其Github截止本文，已经有超过3W+的star，拥有丰富的插件，丰富的主题，
	并且有无数的人已经帮你早出了无数的轮子可供参考。Jekyll自身的强大功能已经足够你打造自己心仪的静态网站
	（这里注意的是静态网站，Jekyll没有任何的后台数据库），
	然而前提是你自己还是得有一定的前端功底，而为了不至于长的太难看，你还得有一定的设计能力。
	这一下子把大部分人给难住了，咱们只是为了单纯的写写博客啊，至于有这么多要求吗？
	看到这里，很多人可能觉得此法不怎么方便啊，然则，正如刚刚反复强调的，
	Jekyll已经有一个非常庞大的社区，这就意味着，你完全可以借鉴别人已经造好的轮子，
	放在Jekyll这里，咱们应该成为主体（Theme）比较合适。本文推荐国内用户可以考虑一款国人开发的主题。
	博主的个人博客即是采用了这个主题。

	因为全部都是英文看着比较费力，出于偷懒，就从平时看到的 github.io博客比较喜欢的clone 下来，自己去除冗余代码，轻松上阵

	你可以选择 https://github.com/Huxpro/huxpro.github.io （国人开发的主题） or https://keysaim.github.io/(同样也是国人开发的主题) 
	

## 遇到的问题

### 1、页面过多，有很多重复代码
	
> 如果用传统的jq开发模式 ，左侧菜单 以及个人信息板块 会存在于每个静态页面中， 当需要修改一处时，需要修改所有静态页的 所有页面
> 
> 提供几种可选 解决方法
> 
> 1) jq + ajax请求静态页（这里的静态页是 独立的左侧菜单和个人信息板块的 dom结构）+ 公共js填充
> 
> 弊端：每次打开新页面时 左侧都是后出来
> 
> 2）VUE 等单页应用开发
> 
> 弊端 初次加载很慢而且 内容涉及一些字体包和庞大的公共CSS npm run dev 和 npm run build 到线上的 样式不一样


楼主选择的方案二，采用VUE开发

### 2、公共CSS 3500多行，而且没有注释， 实在难以分离

**注：**

	在clone 后发现，页面所以CSS 被写在一个CSS文件中， 而且没有注释， 实在难以分离， 

	在main.js 中 import index.js时 ，在开发环境中 还好， 样式都很完美。 

	一旦打包到线上的时候，发现样式缺陷了好多 

	推测： CSS 被 并没有全局引用到

**解决方法：** 修改打包后的html 采用外链的方式 引用index.js 在index.js里又会去引用字体包文件

