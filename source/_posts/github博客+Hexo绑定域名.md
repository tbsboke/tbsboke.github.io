---
title: github+hexo绑定服务器域名
date: 2020-03-02 21:53:24
tags: Hexo 建站
categories: Hexo
---
# 前言：

使用hexo部署的博客是将博客托管到github page上，并且域名固定为xxx.github.io。因github不在大陆内的原因，访问速度有时会不那么理想，想让自己的博客能以稳定的速度访问，需要部署到云服务器。

若想自定义域名，则需要购买一个域名并进行绑定，国外有各种域名服务商，国内阿里云、腾讯云等。

若想部署到云服务器，首先需要购买一个云服务器，国外的可以直接使用，大陆的需要备案(头铁不嫌麻烦可用)但是稳定(而且学生有优惠非常便宜，但是非常非常麻烦)。

[原文地址](https://www.cnblogs.com/luqwer/p/11328600.html)

# 绑定域名但不部署到自己的服务器
## 1、购买域名

国内域名购买后需要实名认证才可以进行解析。国外不需要。

以阿里云为例，也可以选择其他域名服务商(指国外)，注意选择靠谱的商家。
阿里云域名注册网址：https://wanwang.aliyun.com/

<img src="/img/hexo/bangyuming1.png"  alt="加载失败" />

首先想好自己的域名名。域名指[name].com，开头的www.等是不算在这之内的，

如本人博客域名为wa2000.cn，www是在解析域名时添加的。如下

<img src="/img/hexo/bangyuming2.png"  alt="加载失败" />

查询自己想要的域名是否已经被注册，未被注册则看价格是否满意即可购买，短域名价格昂贵，**.com**略贵，**.cn**较便宜大概30/年左右，学生购买服务器+域名有优惠，详情百度阿里云/腾讯云 学生套餐 等。套餐内容貌似不同，但是购买有限制，如只能用大陆服务器、尾缀有要求等等。

<img src="/img/hexo/bangyuming3.png"  alt="加载失败" />

购买域名并实名认证后即可进行解析。

**解析域名**

以我的域名为例，不同商家解析时都差不多。点击解析

<img src="/img/hexo/bangyuming4.png"  alt="加载失败" />

点击添加记录。会出现如前图的添加设置。

<img src="/img/hexo/bangyuming5.png"  alt="加载失败" />

主机记录可理解为域名前缀，即用户输入什么样的网址访问到该解析目标。如果主机记录为www ，则用户需要输入www.[你的域名]才能访问到该解析目标。如果为@，则直接输入域名即可。如果不添加www ，则通过www+域名方式访问的用户将访问失败，@同理，其余的也同理。

<img src="/img/hexo/bangyuming6.png"  alt="加载失败" />

记录类型为解析目标的类型，如果想把该域名绑定到一个ip地址，则选A，如果目标为一个网址，则选CNAME。

这里有两种绑定方法，一种是选CNAME然后在记录值填写 [yourname].github.io ，另一种是选A，然后通过cmd命令行输入 ping [yourname].github.io 获取ip地址，记录值里填入ip地址。

<img src="/img/hexo/bangyuming7.png"  alt="加载失败" />

获取 [yourname].github.io 的ip地址，如图，ping通后会显示ip地址。

<img src="/img/hexo/bangyuming8.png"  alt="加载失败" />

线路选默认。

记录值根据选择的记录类型进行填写。TTL为缓存生效时间，默认600秒即可，即10分钟后生效。填写完毕后点击保存。可以为域名填写多个记录， 如图

<img src="/img/hexo/bangyuming9.png"  alt="加载失败" />

前两个是为github pages绑定时添加的记录，一个www、一个@，这样可以让用域名直接访问的和加了www访问的用户都能访问到自己的博客 (部署到服务器后就不再用了所以暂停了)。接下来两条A类型是将网站部署到自己的服务器时，把域名解析到了自己的服务器IP地址，这样可以通过www、或者直接输入域名的方式来访问自己的服务器。最后一条是绑定的七牛云，用来当做博客的图床。每条记录后面都有操作可以进行修改以及暂停和开启。

**绑定到github pages**

登陆到自己的github，进入网站绑定的仓库，进入设置
<img src="/img/hexo/bangyuming10.png"  alt="加载失败" />

往下找到GitHub Pages，在Custom domain填入刚刚购买的域名，点击save保存。勾选Enforce HTTPS则开启HTTPS安全协议。

<img src="/img/hexo/bangyuming11.png"  alt="加载失败" />

如

<img src="/img/hexo/bangyuming12.png"  alt="加载失败" />

然后到本地博客**source文件夹**下**新建文件CNAME**，输入内容为自己的域名，**并将文件尾缀如.txt等删掉然后保存即可**。(没有的话貌似每次将代码从本地推到github都会使域名访问404，因为每次推送都会覆盖原本的仓库代码。所以把CNAME文件放在source中，使每次推送都会建立一个CNAME)

至此，github pages的域名绑定完成了，稍等片刻即可尝试使用域名访问。
