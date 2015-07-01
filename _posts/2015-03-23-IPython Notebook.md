---
layout: post
title: IPython Notebook
category: tech
tags: IPython-Notebook Jupyter python
---


##1. IPython介绍

<br>
![Ipython logo](http://img3.url2io.com/blog-assets/img/ipython_logo.png)

IPython是Python的交互式shell，支持代码自动补全、高亮，支持shell命令。还有众多magic命令扩展各种功能。比如在函数后加`?`执行会列出此函数的使用文档，在函数后加`??`执行会列出此函数的源码。个人认为这是当前最好用的Python shell。

<!--more-->

##2. IPython Notebook介绍

Notebook是web based IPython封装，使得可以在浏览器上使用IPython。得益于web端数据与表现分离的模式和富文本特性，使得Notebook可以将IPython被命令行限制的数据表现能力，通过浏览器得到完全展现。如果分析下我们以前的工作流程就能发现这一改变能带来什么。

1. 首先要完成整个工作的一个部分，在命令行中输入代码或执行代码文件得到计算结果
2. 再将计算结果输出到屏幕或存入文件中。如果要修改结果则重复以上步骤
3. 将计算结果从文件中取出作为整个工作的一部分写入报告中（共享、交流）
4. 各个部分的工作重复以上步骤

可以看到我们必须在代码编辑器，运行终端，文件夹，文档编辑器中不断进行切换，而在Notebook中整个过程始终在浏览器中进行。包括视频、图片、LaTex公式都可以嵌入。

![Notebook.png](http://img3.url2io.com/blog-assets/img/notebook.png)

基于这些特性Notebook更多得被作为一种新兴的交互式的数据分析与记录工具，而不是IPython的web版。所以在IPython3.0中Notebook Evolved from the IPython Project，The language-agnostic parts of IPython are getting a new home in Project [`Jupyter`](https://github.com/jupyter)。以下是它的一些特性。
> 可以替代IPython的语言和工具[IPython kernels for other languages](https://github.com/ipython/ipython/wiki/IPython-kernels-for-other-languages)  
> Notebook (format, environment, conversion)  
> [JupyterHub](https://github.com/jupyter/jupyterhub) (multi-user Notebook server)  
> Rich REPL Protocol

##3. 安装

本文安装的是IPython3.0下的Notebook，IPython3.0之前或之后的版本应该会有所不同。
> IPython will continue to exist as a Python shell and a kernel for Jupyter, but the notebook and other language-agnostic parts of IPython will move to new projects under the Jupyter name. IPython 3.0 will be the last monolithic release of IPython.

```bash
## 创建python虚拟环境(非必要)
$ mkvirtualenv ml --system-site-package
## 1. 安装numpy包
$ pip install numpy
## 2. 安装pyside包
$ sudo add-apt-repository ppa:pyside
$ sudo apt-get update
$ sudo apt-get install python-pyside
## 3. Fortran编译器
sudo apt-get install gfortran
## 4. 按章matplotlib包
pip install matplotlib
## 5. 安装scipy包
sudo apt-get install python-scipy
## 6. ipython notebook, 其他依赖pip自动解决
pip install "ipython[notebook]" --upgrade
```

##4. 使用

因为IPython Notebook基于B/S架构，所以除了可以作为本地软件运行，它还可以作为服务器供其他人通过网络访问（SaaS啊！）。

本地运行十分简单，只用一句命令

```bash
$ ipython notebook
# 参数见
$ ipython notebook -h
```

以下详细介绍远程方式

###4.1 configuring the IPython Notebook

建立server的config
> The notebook web server can also be configured using IPython profiles and configuration files. The Notebook web server configuration options are set in a file named `ipython_notebook_config.py` in your IPython profile directory. The profile directory is a subfolder of your IPython directory, which itself is usually `.ipython` in your home directory.

```bash
# 查看配置文件位置
$ ipython profile locate [default]
# 创建配置文件
$ ipython profile create ml
# 查看你的配置文件在哪，方便之后配置
$ ipython profile locate my_profile
```

在运行时需要用以下方式指定配置文件

```bash
$ ipython notebook --profile=my_profile
```

更多IPython配置的相关细节见[here](http://ipython.org/ipython-doc/dev/config/intro.html)

###4.2 Securing the notebook server

> The IPython Notebook allows arbitrary code execution on the computer running it. Thus, the notebook web server should never be run on the open internet without first securing it. By default, the notebook server only listens on local network interface (127.0.0.1) There are two steps required to secure the notebook server:  
> 1.Setting a password  
> 2.Encrypt network traffic using SSL  

**Setting a password**

将以下代码加入配置文件，你的`ipython_notebook_config.py`中

```python
from IPython.lib import passwd
# Password to use for web authentication
password = passwd("my_password")
c = get_config()
# 安全起见也可以在外部将密码sha1后，再复制到此
c.NotebookApp.password = password
```

**Using SSL/HTTPS**

TODO

###4.3 Running a public notebook server

默认情况下Notebook server只监听`locahost/127.0.0.1`，需要通过修改配置文件使它能够监听所有ip。另外默认情况会自动打开浏览器，而作为服务器时是不需要的。

还是在你的`ipython_notebook_config.py`中

```python
c.NotebookApp.ip = '*'
c.NotebookApp.open_browser = False
```

###4.4 Running with a different URL prefix

默认的Notebook通过`http://localhost:8888/tree`访问，如果你想定制它的运行网址可以在你的`ipython_notebook_config.py`中设置

```python
c.NotebookApp.base_url = '/ipython/' #你的前缀
c.NotebookApp.webapp_settings = {'static_url_prefix':'/ipython/static/'}
```

###4.5 Using a different notebook store

TODO

###4.6 使用supervisor来监控

通过以上配置我们得到了一个可用的服务，以下通过supervisor来监控它的运行，使它成为一个真正的web服务。

在`etc/supervisor/conf.d`中添加`ipy.conf`作为服务的配置文件，内容如下：

```
[program:pein]
command=/home/你的用户名/.virtualenvs/ml/bin/ipython notebook --notebook-dir=/home/你的用户名/learn_space/ml/ipy --profile=ML
process_name=ipython_notebook
numprocs=1
numprocs_start=0
direcotory=/home/你的用户名/learn_space/ml/ipy
autostart=true
autorestart=true
user=你的用户名
```

到此为止IPython Notebook的所有工作都完成了。我用它做了kaggle的[Titanic: Machine Learning from Disaster](https://www.kaggle.com/c/titanic)不得不说用它来做机器学习、数据挖掘之类的工作真是太爽了!


Ref:

* [ipython/examples/Notebook](http://nbviewer.ipython.org/github/minrk/ipython/tree/master/examples/Notebook/) -> [Configuring the Notebook and Server](http://nbviewer.ipython.org/github/minrk/ipython/blob/master/examples/Notebook/Configuring%20the%20Notebook%20and%20Server.ipynb#)  
* [IPython notebook搭建](http://www.jinglingshu.org/?p=4190)
* [IPython3时代到来](http://www.dongwm.com/archives/ipython3shi-dai-dao-lai/)
* [分享ipython Notebook](http://www.dongwm.com/archives/ji-jiang-zai-bpugfen-xiang/) 干货超多!
> 1.豆瓣东西双11临时后台 - 想看效果么? 看下面  
> 2.把ipython notebook转换成html或者其他格式以及它的原理  
> 3.我写的一个缩小版的nbviewer: Ipynb-viewer, 直接在ipython目录启动web服务  
> 4.nbconvert原理  
> 5.用ipynb写blog(pelican/nikola) 效果可见divingintoipynb_pelican和divingintoipynb_nikola 还会讲到pelican转换ipynb到html插件，使用fabric: new_post, edit，import_ipynb. 我也给nikola贡献了import ipynb功能.  
> 6.ipython notebook用到得第三方库和组件  
> 7.Rich display system  
> 8.现有的扩展, 演示. 我自己写的一个扩展. 演示, 代码分析  
> 9.定制ipython notebook的键位. 使用emacs键位. 设计一个新的功能 - 弹出一个dialog列出所有emacs快捷键说明(想起来了么? C-h b)  
> 10.定制一个基于selectize.js的widget. 前后端代码分析.  
> 11.ipython notebook 其他方面的一些用法， 整个过程中有ipython2也有ipython3  
