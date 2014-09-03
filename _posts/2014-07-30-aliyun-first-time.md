---
layout: post
title: aliyun first time
category: 
---

大致介绍了第一次接触阿里云需要了解的一些东西。包括有哪些产品、这些产品的功能、产品的收费标准、续费和升级的规则、这里介绍的产品有云服务器ECS和开放存储服务OSS。ECS相关的有云服务器的使用导航包括登录、磁盘等和一些linux操作指南。介绍了OSS的域名绑定。

<!--more-->

#资源

* [云服务器帮助大全](http://help.aliyun.com/all/11108189.html?spm=5176.7224673.1997283365.4.CQuPf0)
* [云服务器产品文档](http://help.aliyun.com/doc/all/11112743.html?spm=5176.7224673.0.0.CQuPf0)
* [阿里云官方论坛](http://bbs.aliyun.com)

------

<code>弹性计算</code>

#[云服务器ECS](http://www.aliyun.com/product/ecs/?spm=5176.383338.201.2.M2AUj9)

云服务器（Elastic Compute Service 简称ECS）是一种简单高效，处理能力可弹性伸缩的计算服务助您快速构建更稳定、安全的应用。提升运维效率，降低IT成本，使您更专注于核心业务创新

创建了一个ECS实例：es(Eastwatch-by-the-Sea, 东海望)
> CPU：1      期限：2014-7-30 ～ 2015-1-31
> 内存：1GB
> 系统盘：20G 数据盘：0G
> 带宽：1Mbps 期限：2014-7-30 ～ 2014-8-31
> IP：121.40.xxx.xxx(公) 10.168.xxx.xxx(内)

[ECS实例规格选择-价格因素](http://help.aliyun.com/doc/view/13514657.html?spm=0.0.0.0.kHy17K)

1. (算力)ECS实例的规格：包含CPU的配置和内存的大小，如4核CPU 16GB内存。参考[ECS实例规格表](http://help.aliyun.com/view/13433721.html?spm=0.0.0.0.UCOz0C)。
2. (带宽)网络的规格包含两种方式: 按固定带宽的方式、按使用流量的方式
3. (容量)磁盘规格：包括磁盘的种类，个数，及每块磁盘的容量
> 临时磁盘：具有更好的吞吐能力，适合数据可靠性要求不高，但吞吐要求较高的应用。如视频压缩的临时文件，Hadoop等已经具备多份拷贝能力的软件
> 云磁盘（包括独立云磁盘）：具有更好的数据安全性，适合作为文件系统，重要的数据存储，如MongoDB/PostgreSQL等
> 云磁盘和临时磁盘都容许最多选择5块磁盘（含系统盘，单个磁盘容量最大2000GB，单个临时磁盘容量最大1024GB），单台ECS实例临时磁盘总容量最大2048GB
> 磁盘购买相关：一台实例可以使用一种或两种磁盘种类（包括系统盘和数据盘），一旦在购买时选定了磁盘种类，不能再做更改。
> 
> 不同磁盘种类的实例的特性如下：
> **拥有云磁盘（包括独立云磁盘）的ECS实例最为灵活和弹性**
>  可以增加减少CPU，内存；
>  可以增加磁盘个数；
>  当物理机出现故障宕机时，将自动为您进行宕机迁移，并保证数据的一致性和完整性，最大限度的减少您的服务中断时间。
> **拥有临时磁盘的ECS实例，会有如下的限制**
>  不能增加磁盘个数；
>  不能升级CPU和内存（但可以升级带宽）；
>  当物理机出现故障宕机时，会为您的ECS实例进行自动的宕机迁移，但是您在数据盘上的数据将会丢失。
> *注意：当系统盘为云磁盘时，数据盘只能是云磁盘；而当系统盘为临时磁盘时，数据盘可以选择临时磁盘和云磁盘。*
> ref: [ECS的存储](http://help.aliyun.com/doc/list/11112752.html?spm=0.0.0.0.mHwMRw)


[包年包月ECS实例的：续费、升级、购买相同配置](http://help.aliyun.com/doc/view/13514712.html?spm=0.0.0.0.DJpNdR)
> **续费**
> 您可以在包年包月的ECS实例到期前进行续费操作，在续费的同时您也可以为ECS实例变更配置，包括增加、减少CPU和内存，增加或者降低带宽，这些变更是指在当前服务期限结束后进行变更，当前服务期限内配置不发生变化。
> 注意：
> CPU和内存的变更需要在控制台中进行ECS实例的重启操作，才能生效，原配置到期后，请务必到控制台操作重启（其他方式重启无效），您有5（自然）天的时间安排重启计划，5天后仍未重启，阿里云将自动为您重启ECS实例。
> 续费时进行了配置变更操作后，您不能在原服务期限结束前再次进行升级（除了带宽）和续费变更操作。
> **升级**
> 当您的ECS实例的计算能力已经不能满足您的业务需求时，你可以根据负载情况选择升级ECS实例，包括增加CPU和内存，增加磁盘，增加带宽。
> 注意：
> CPU和内存的升级需要在控制台中进行ECS实例的重启操作，才能生效；
> 增加磁盘，无需停止您的ECS实例，需要对增加的磁盘进行“分区格式化和挂载新分区”的操作。操作指南《分区格式化/挂载数据盘》；
> 升级带宽，选择升级时间，无需停止您的ECS实例，直接生效。
> **购买相同配置**
> 您可以方便的购买相同的多台ECS实例，阿里云会为您复制相同的配置（包括操作系统）到新的订单，实现方便的一键购买。

[云服务器实例规格详单](http://help.aliyun.com/doc/view/13514749.html?spm=0.0.0.0.DJpNdR)
> 规格分类：Tiny, Standard, High Memory, High CPU
> 各规格的：类型代码，CPU(Core)，内存，包月全网开放，按量付费全网开放



##[Linux系统云服务器使用导航](http://help.aliyun.com/view/11108189_13433798.html?spm=5176.7224689.1997283805.7.Fh2LHl)

###1. 远程登录服务器
```bash
# 公钥登录：http://www.ruanyifeng.com/blog/2011/12/ssh_remote_login.html
$ ssh-copy-id root@$IP_ES
$ ssh root$IP_ES
#host authorized_keys 文件
$ vi ～/.ssh/authorized_keys
$ service ssh restart

#local 登录更方便
$ vi ~/.ssh/config
+    Host sshname
+    user username
+    hostname hostname(ip address)
+    IdentityFile ~/.ssh/id_rsa
+    port 22
```


###2. 检查磁盘和分区格式化

原始的hostname不好辨认，修改hostname为es

```bash
$ uname -a
$ vi /etc/hostname 
$ vi /etc/hosts
```

<code>ref</code>:
 * [Linux 系统挂载数据盘](http://help.aliyun.com/view/13435365.html)


###3. 上传文件到系统里

1. sftp

```bash
$ sftp june@$IP\_ES:/home/june
# lcd, lls, lmkdir, lpwd, 或在命令前加! 进行本地操作
$ cd, ls, mkdir, pwd进行远程操作
# 本地上传到远程主机
$ put [-Ppr] local [remote]  // put /home/pic/solgan.png 
# 从远程主机下载到本地
$ get [-Ppr] remote [local]  // get solgan.png
```

2. rsync <code class='todo'></code>

```bash
$ rsync (--exclude=exclude) -avz (-e "ssh -p 22") ./ sshname:~/path
```

###4. 新建用户及调整目录文件的拥有者和拥有组

新建用户：

```bash
$ adduser june
$ cp .profile /home/june
$ cp .bashrc /home/june
# 将/home/june目录和目录下所有文件的拥有者和拥有组改为june june
$ chown -hR june:june /home/june
$ vi /etc/group # 添加june到sudo组
```

查看进程是以什么身份运行的：

```bash
ps aux | grep nginx // 对应网站的根目录及下面的文件目录的拥有者和组应该也是这个用户，这样才不会有权限错误
```


###5. 更新源, 同步时间

[update\_source.zip](http://oss.aliyuncs.com/aliyunecs/update_source.zip?spm=5176.7150518.1996836753.5.xmeZtd&file=update_source.zip)
> 功能：自动检测系统并更新源
> 适用系统版本：兼容线上所有linux版本
> 执行方法：以root身份执行命令：bash update\_source.sh
> 解决了什么问题：一键式检测系统并更新源
> 给客户带来了好处：用户只需执行该脚本一次即可自动检测系统并更新源。
> 备注：由于系统版本都有支持的周期所以部分源可能会出现不可用的情况，包括官方的源，这是正常情况

[update\_time.zip](http://oss.aliyuncs.com/aliyunecs/update_time.zip?spm=5176.7150518.1996836753.5.VltFsC&file=update_time.zip)
> 功能：修正时区，修改ntp配置，同步时间，修改ntp服务启动模式
> 适用系统版本：兼容线上所有linux版本
> 执行方法：以root身份执行命令，bash update_yum_source.sh
> 解决了什么问题：一键式修正系统时间不同步的问题，省去了复杂的命令和步骤


##[linux操作指南](http://help.aliyun.com/all/sub/11108193.html?spm=5176.7224825.1997283229.8.FAH1ht)


###[开机启动项 chkconfig]() <code class='todo'></code>

```bash
$ sudo apt-get install chkconfig
$ chkconfig --list
$ chkconfig --level ??
```


###[新手入门-云服务器linux使用手册](http://bbs.aliyun.com/read.php?spm=5176.7150518.1996836753.6.iQKWR6&tid=130069)

> 远程访问
> 挂载数据盘
> 安装Apache
> 安装MySQL
> 安装PHP
> 安装PHPWind

###[一键安装web环境](http://help.aliyun.com/view/11108189_13435438.html?spm=5176.7224445.1997283057.5.dqPOxE) <code class='todo'></code>

[安装包](http://oss.aliyuncs.com/aliyunecs/sh-1.3.0.zip?spm=5176.7150518.1996836753.5.UzIFhF&file=sh-1.3.0.zip)包含的软件及版本：

* nginx：1.0.15、1.2.5、1.4.4
* apache：2.2.22、2.4.2
* mysql：5.1.73、5.5.35、5.6.15
* php：5.3.18、5.4.23、5.5.7
* php扩展：memcache、Zend Engine/ OPcache
* ftp：（yum/apt-get安装）
* phpwind：8.7 GBK
* phpmyadmin：4.1.8


###[Memcache和Redis高速缓存部署方式！](http://help.aliyun.com/view/11110205_13666616.html?spm=5176.7224905.1997284357.8.K52Cdy) <code class="todo"></code>

###[部署工具](capistrano)

在《ECS生产环境搭建》中介绍了git部署代码push-to-deploy

##[运维技术分享](http://help.aliyun.com/all/sub/11108195.html?spm=5176.7224825.1997283229.10.d08tw2)  <code class="todo"></code>


<code>存储与CDN</code>

#[开放存储服务OSS](http://www.aliyun.com/product/oss/?spm=5176.383518.3.7.ZINfEV)

开放存储服务（OpenStorageService，OSS），是阿里云对外提供的海量、安全和高可靠的云存储服务。RESTFul API的平台无关性，容量和处理能力的弹性扩展，按实际容量付费真正使您专注于核心业务。

##[价格总览](http://help.aliyun.com/view/11108271_13438754.html?spm=5176.7225921.1997285357.4.q6IR0g)

1. 价格总览
2. 扣费说明
3. 欠费说明
> 当OSS服务处于欠费状态，且欠费时间超过24小时，OSS服务将自动停止。而您所占用的存储空间的这部分资源仍会继续按日扣费， 因此欠费余额会累计。在欠费后24小时内时行充值，您的服务将不会受到停服影响。如您欠费时间超过24小时，则您的OSS服务将自动停止，您可以在15天内充值补足欠费后，服务会自动开启，可以继续使用。**欠费超过15天，将视为您主动放弃OSS存储服务，存储空间将被回收，存储空间内的数据会被清理，数据不可恢复。**
4. [OSS价格计算器](http://www.aliyun.com/product/oss/recommend.html?spm=5176.383663.5.18.USJOPC)
> 价格因素：存储、流量、请求次数
> 存储和流量按实际使用量，最小计费单位是GB。请求次数按PUT型每千次，GET型每万次整数计量计费收费


##[OSS域名绑定](http://help.aliyun.com/view/13438897.html)

设置绑定域名，验证备案号
1. 选择欲绑定BUCKET的“属性”进行设置
2. 在BUCKET “属性”设置中选择“绑定域名”模块
3. 详细阅读“操作指南”，点击“下一步”进入当前Bucket的“域名绑定”操作页面。
4. 填写要绑定的域名
5. 域名线上验证
> 第一步，到域名提供商网站上将域名image.a.com  添加A记录指向主机：10.1.1.1；
> 第二步，下载验证文件，放置到云主机10.1.1.1根目录下，如image.a.com/21131.txt；
>   $ python -m CGIHTTPServer 80 //开启服务器 
> 第三步，在控制台点击[验证并绑定域名]()
> 第四步，验证通过以后，请到域名提供商处删除之前做的A记录，然后将域名image.a.com CNAME到BUCKET的网址 [OSS内外网网址](http://help.aliyun.com/view/11108271_13438690.html?spm=5176.7224861.1997285601.8.eylrVF)
