---
title: "使用 Netlify + Github + Hugo 快速搭建静态网站"
date: 2019-09-22T20:37:21+08:00
draft: false
tags: ["blog"]
categories: ["blog"]
---

本文主要描述了如何基于 [Netlify](https://www.netlify.com/) 的服务快速部署一个静态网站，其网站源码托管在 [GitHub](https://github.com/)，并使用 [hugo](https://gohugo.io/) 工具构建静态网站。

感谢技术的发展，如今搭建一个网站的成本是如此之低，基本上只需要出钱购买域名，其他服务均有免费的提供商。

[Netlify](https://www.netlify.com/) 就是一家提供了网站托管服务的提供商，基础功能可以免费使用。

想要使用 [Netlify](https://www.netlify.com/) 的服务，首先当然是注册一个 [Netlify](https://www.netlify.com/) 的用户，访问 [Netlify](https://www.netlify.com/) 的主页，点击页面右上角的 **Log in** 或者 **Sign up** 跳转至[认证页面](https://app.netlify.com) 。  

![app.netlify.com](/img/host-static-website-using-netlify/app.netlify.com.png)  

Netlify支持使用GitHub、Gitlab等账户进行登录，由于我们的静态网站打算存储在GitHub上，这里自然就选择用GitHub的用户进行登录。  

点击 **GitHub** 按钮跳转至GitHub完成认证和授权，进入Netlify的控制台。

![netlify.admin](/img/host-static-website-using-netlify/netlify.admin.png)

在控制台中可以直接上传已经构建好的静态网站文件，也可以基于已有的 repository 创建网站，当然这两种方式的前提是你已经准备好了静态网站的相关文件。

为了体验快速搭建一个静态网站，这里我选择使用 [Netlify](https://www.netlify.com/) 提供的一键部署功能。使用该功能可以基于 [Netlify](https://www.netlify.com/) 提供的模板一键部署网站，甚至不需要提前在 GitHub 创建 repository。

首先点击控制台最下方的 [Docs](https://www.netlify.com/docs/) 连接，进入 [Netlify](https://www.netlify.com/) 的文档主页，并下拉至页面最下方，可以看到如下连接：

![netlify.docs](/img/host-static-website-using-netlify/netlify.docs.png)

点击 [View our Templates](https://templates.netlify.com/) 即可进入模板页面。

![netlify.templates](/img/host-static-website-using-netlify/netlify.templates.png)

可以在页面中浏览一下提供的模板，模板名称下面的 **Tag** 显示了该模板所使用的技术等信息。由于后面我们打算使用 **Hugo** 构建网站，因此直接使用 [Hugo](https://templates.netlify.com/tags/hugo) 标签过滤出所有基于Hugo的模板:

![netlify.template.casper](/img/host-static-website-using-netlify/netlify.template.casper.png)

第一模板的主题看起来还不错，就选择它进行部署，点击 `Deploy to netlify` 按钮，去 **GitHub** 进行授权。

![github.auth](/img/host-static-website-using-netlify/github.auth.png)

使用GitHub的账号进行登录，如果之间已经完成过授权，会直接跳到下一步：

![netlify.save.deploy](/img/host-static-website-using-netlify/netlify.save.deploy.png)

在这里可以输入将要在 **GitHub** 上创建的 **repository** 的名字，这里我使用默认名称，不进行修改。

点击 `Save & Deploy` 按钮完成部署。

页面将跳转回控制台，等待一段时间，平台将完成静态网站的构建和部署：

> 如果页面一直显示正在部署，可以刷新网页试一试

![step.one](/img/host-static-website-using-netlify/step.one.png)

上图中左上角的域名就是部署完成的网站的URL了，该域名是 [Netlify](https://www.netlify.com/) 为每个项目分配的唯一地址。可以点击该地址看一下我们的网站，体验一下阶段性成果。

别着急，我们的工作还没有完，[Netlify](https://www.netlify.com/) 分配的地址可不是便于人类记忆的地址，自己的网站还是要有自己的域名。提供域名服务的服务商有很多，价格也很亲民，我是在阿里云的[万网](https://wanwang.aliyun.com/)买的域名，有些新的域名第一年只需个位数的人民币就能拿下（当然第二年起就贵了，还是要注意看清楚），域名的购买就不在这里展开了。

> 购买域名后要记得实名认证和进行备案

点击 **Getting started** 中的第二项 **Set up custom domain** 去设置域名：

![netlify.add.custom.domain](/img/host-static-website-using-netlify/netlify.add.custom.domain.png)

输入自己买到的域名，并点击 `Verify` 进行验证。

![netlify.confirm.domain](/img/host-static-website-using-netlify/netlify.confirm.domain.png)

[Netlify](https://www.netlify.com/) 会去验证域名是否已经被注册了，并提示你进行确认，点击 `Yes, add domain` 按钮完成 [Netlify](https://www.netlify.com/) 上域名的设置。

试着访问一下我们买的域名，你会发现网站并没有如期出现，这是因为此时的域名还没有生效，我们还要去设置 **DNS解析** 。一般域名提供商都会提供 **DNS解析** 服务，因此我直接去阿里云进行配置。

在控制台的左上方点击 `Domain settings` 按钮，进入 **Domain management** 页面，等待系统完成DNS解析的检测：

![netlify.domain.management](/img/host-static-website-using-netlify/netlify.domain.management.png)

点击带有黄色感叹号标志的 `Check DNS configuration` 连接，会弹出DNS的设置指南：

![netlify.dns.configuration](/img/host-static-website-using-netlify/netlify.dns.configuration.png)

可以看到，首先推荐的方式是添加 **ANAME** 或者 **ALIAS** 记录。若DNS服务商不支持推荐的方式，则可以添加 **A** 记录，只是享受不到一些高级特性了。除了去第三方DNS服务提供商添加记录，[Netlify](https://www.netlify.com/) 本身也提供了DNS服务，点击上图最后的 `Set up Netlify DNS for ***`链接可以完成相关配置，并在最后一步提示你去购买域名的服务商进行配置：

![netlify.setup.dns.nameservers](/img/host-static-website-using-netlify/netlify.setup.dns.nameservers.png)

到这里你会发现，无论哪种方式，最终都要去你真正的域名提供商进行配置才可以。我最终选择使用 **Netlify DNS** ，并在阿里云域名控制台的 **DNS修改** 里填写 Netlify 的 DNS 服务器：

![aliyun.dns.modify](/img/host-static-website-using-netlify/aliyun.dns.modify.png)

完成 **DNS** 的配置后，就可以通过我们自己的域名 [dawniot.top](https://dawniot.top/) 访问我们的网站了。

最后，我在 [Netlify](https://www.netlify.com/) 的 [About](https://www.netlify.com/about/) 页面中发现，其团队成员分布在多个国家，并且超过一半的人都是在家远程办公，小小羡慕一下~
