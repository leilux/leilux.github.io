leilux.github.io
================

<link rel="stylesheet" href="/assets/css/style.css" type="text/css"/>

##<span class="icon-quill"></span> post

* 用&lt;code class='todo'&gt;&lt;/&gt;表示待做的事情
* 使用&lt;!--more--&gt;作为except\_separator

##<span class="icon-lab"></span> lab

lab包含一些试验性的项目，发布一个项目的基本流程是:

1. 编写项目主页`xxx.md`，为了方便管理放到`/_posts/LAB`目录中
2. `xxx.md`的YAML信息如下：参考`/_posts/LAB/template.md`
> layout: post
> title: 
> category: lab
> tags: 
> name: 项目名称
> web: 项目网址
> thumbnail: 项目缩略图, /assets/img/lab/项目缩略图
> progress: 当前进度(80%)
> introduction: 项目简介，30字以内
3. 生成静态文件，lab页会列出所有`category`为`lab`的post

##TODO

* 能整合stackedit吗？这真是我用过的最好的md编辑器了。
* TOC
* [网易云音乐插件](http://music.163.com/#/outchain/0/37650114/m/use)
```html
<embed src="http://music.163.com/style/swf/widget.swf?sid=37650114&type=0&auto=0&width=310&height=430" width="330" height="450"  allowNetworking="all"></embed>
```
