<!-- Markdown提示/错误等：https://github.com/orgs/community/discussions/16925-->


<div align="center">
<h1>Online Proxy</h1>


<br>

<!-- [![GitHub license](https://img.shields.io/github/license/1234567Yang/cf-proxy-ex)](https://github.com/ViewFaceCore/ViewFaceCore/blob/main/LICENSE) &nbsp;&nbsp;

![GitHub stars](https://img.shields.io/github/stars/1234567Yang/cf-proxy-ex?style=flat)
[![Github Release](https://img.shields.io/github/v/release/1234567Yang/cf-proxy-ex)](https://github.com/1234567Yang/cf-proxy-ex/releases/latest)
![GitHub forks](https://img.shields.io/github/forks/1234567Yang/cf-proxy-ex) -->

[💻 在线体验](#在线体验) &nbsp;| [⚒ 用法](#用法) &nbsp;| [🚀 快速开始](#快速开始) &nbsp;| [📈 基于原项目的改进](#基于原项目的改进) &nbsp;| [🔒 安全密码](#安全密码) &nbsp;| [📸 截图](#截图) &nbsp;| [📦 LICENSE](#license) &nbsp;| [📄 备注](#备注) &nbsp;| [👍 感谢](#感谢) &nbsp;| [⭐ Star History](#star-history)


无服务器(Serverless)在线代理，支持Github，DuckDuckGo等网站。

<br>
<!--本项目可以让你通过一个**不同**的链接打开**相同**的网站，目前支持100%加载Github，Duckduckgo，Stackoverflow等网站，并且和打开原网站毫无差别。和其它开源代理以及hide.me在线代理相比，本项目可以加载更多静态资源、实现Cookie作用域管理、提交表单、相对URL转绝对URL，转跳自动补全网址等强大的功能。-->
<!--本项目是一款基于Cloudflare worker的在线代理。目前支持100%加载Github，Duckduckgo，Stackoverflow等网站，并且和打开原网站毫无差别。和其它开源代理以及hide.me在线代理相比，本项目可以加载更多静态资源、实现Cookie作用域管理、提交表单、相对URL转绝对URL，转跳自动补全网址等强大的功能。-->

</div>


# 在线体验

### 首页
https://proxy.ilovescratch.dpdns.org/
### DuckDuckGo聊天
https://proxy.ilovescratch.dpdns.org/https://duckduckgo.com/?t=h_&q=hi&ia=chat
### Google地图
https://proxy.ilovescratch.dpdns.org/https://www.google.com/maps


# 用法
* 请先根据 [快速开始](#快速开始) 进行部署
* 在任意网址前面加上 `https://你的域名/` <br>例如 `https://你的域名/https://github.com`
* [使用技巧](usage_tips.md)


# 快速开始

* [在Deno上部署](deploy_on_deno_tutorial.md)
* [在Cloudflare上部署](deploy_on_cf_tutorial.md)

> [!TIP]
> 强烈建议开启[安全密码](#安全密码)，不仅可以防止被扫描，还可以防止网站爬虫爬取内容。

自定义域名获取（可选）：

> [!NOTE]  
> 请注意，免费域名未经实际测试，只是转发消息，并且实际上应该很难获取

* 免费域名申请：https://secure.nom.za/  https://nic.eu.org/  https://nic.ua https://domain.digitalplat.org/
* 不需要申请，link域名0元免费1年：https://dynadot.com/
* 域名购买：https://porkbun.com/  https://domain.com/<br >购买时可以按 `Ctrl + F`，搜索 `$0.` 


# 基于原项目的改进
* 去掉`/proxy/`，方便使用。我看到有issue说了，但是作者说想添加引导界面，这个问题我也解决了。
* 手动处理转跳事件（3XX），防止一些相对资源加载不出来。
* 判断欲代理的网址是否以`http`开头，如果不是就自动加上。
* 把Header里所有有关代理网址的信息全部换成要代理的网站的信息，防止某些网站阻止代理。
* 相对路径全部转换绝对路径，方便加载资源（如JS，CSS等）。
* Cookie作用域修改成仅当代理那个网站时，防止Cookie太大服务器发来400 bad request，同时也防止恶意网站获取所有Cookie。
* 把`XMLHttpRequest`和`fetch`注入返回的HTML，这样也可以提交表单数据。
* 把一个文档监视器注入到返回的HTML，这样有新的链接也可以相对转绝对。
* 修改`Content-Security-Policy`和`X-Frame-Options`的Header，实现可代理Duckduckgo，同时也解决了一些网站打不开的问题。
* 在返回的时候，如果是HTML，那么添加`"Content-Type": "text/html; charset=utf-8"`，防止一些较为古老的中文网站打开出现`锟斤拷`，`烫烫烫`的问题。
* 添加最后访问网址的Cookie，可以解决搜素引擎搜素之后出现异常的情况，如：`https://the proxy/https://www.duckduckgo.com/`会转到`https://the proxy/?q=key`。
* 优化了一些代码。

# 安全密码
安全密码利用Cookie，在设置了密码的情况下，会先检测是否有密码Cookie以及是否正确，如果不正确那么可以设置输入密码界面，或者直接403。密码Cookie默认名称为`passwordCookieName`，设置密码可以代码里搜索`const password = "";`并替换成你的密码。
更详细的教程可以[点这里](security_password_tutorial.md)。

# 截图
![DuckDuckgo](img/duckduckgo.jpg)
![Baidu](img/baidu.jpg)
![GitHub](img/github.jpg)
![StackOverFlow](img/stackoverflow.jpg)

# LICENSE

本项目基于 [cf-proxy-ex]（ 附加要求的MIT 协议）开发，衍生作品整体采用 修改版 MIT 协议。  
- 原代码部分：保留协议（见 [LICENSE-MIT](LICENSE.cf-proxy-ex) 文件）。  
- 新增代码及修改部分：（见 [LICENSE](LICENSE) 文件）。  

# 备注
* **此项目仅供学习在线代理的原理和实现方式使用，严禁用于从事违法违规活动！**
* 请不要通过在线代理登录任何网站。虽然本项目中已经限制了Cookie的作用域，也就是说理论上是可行的，但是非常不建议。像是这个项目原版的代理，它Cookie是全局的。也就是说如果你（通过代理）登录了GitHub然后访问恶意网站，你的所有Cookie就给你偷走了。
