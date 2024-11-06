---
title: SwitchyOmega
description: 
published: true
date: 2024-11-06T10:45:32.341Z
tags: 
editor: markdown
dateCreated: 2024-11-06T09:56:19.077Z
---

# SwitchyOmega 浏览器代理插件安装使用
# 一、下载安装
Chrome 或基于 Chromium 的浏览器
(1)在线安装
从 Chrome 应用商店 安装，如果您无法从该链接安装，请使用下面的离线安装。
(2)离线安装
去 [Github](https://github.com/FelisCatus/SwitchyOmega/releases) 下载 最新版安装包 ，或者下载文章末尾附件 文件进行安装。
> 在 Chrome 地址栏输入 chrome://extensions 打开扩展程序，拖动 .crx 后缀的 SwitchyOmega 安装文件到扩展程序中进行安装。

Firefox 或基于 Mozilla 的浏览器
(1)在线安装
从 Mozilla Add-Ons 应用商店安装。如果您无法链接应用商店安装，请使用下面的离线安装。
(2)离线安装
去 Github 下载 最新版安装包，或者下载本文章末尾附件 文件进行安装。
> 在 Firefox 地址栏输入 about:addons 打开插件管理 (Add-Ons Manager)， 选择扩展程序 (Extensions) ，拖动 .xpi 后缀的 SwitchyOmega 安装文件到扩展程序 (Extensions) 中进行安装。

> SwitchyOmega 需要在 Firefox Nightly 版本 >= 57 才能安装使用。
{.is-warning}

# 二、配置

目前 SwitchyOmega 支持 Chrome 和 Firefox 浏览器。SwitchyOmega 不提供代理服务，不会自动解封网站，也不会自动保护您的隐私，你需要有代理服务器才可以使用。

## 1、情景模式
**①代理服务器**
代理服务器可以支持 HTTP、HTTPS、SOCKS4、SOCKS5 代理协议。SOCKS 代理协议不支持验证。下图以配置 Shadowsocks 的 SOCKS5 代理协议为例。
![switchyomega1.png](/images/switchyomega1.png)

> 情景模式只需要设置好代理协议和端口就可以，如果是使用需要验证的 HTTP 代理协议请设置验证信息。不要填错了代理协议（常见的有 HTTP 或 SOCKS），如果填错了有一大堆问题，程序还不会提示填错了。
{.is-info}

**② 自动切换模式**
自动切换模式比较类似下面的“PAC情景模式”，但自动切换模式配置更多，可以自己设置切换规则规则，也可以根据 GFWList 生成规则。

在新建情景模式时，类型选择第二个 “自动切换模式”，然后做如下配置：
![switchyomega2.png](/images/switchyomega2.png)

切换规则是在访问条件设置的域名时候使用后面设置的情景模式。比如图中我设置 *.google.com 使用 SS 情景模式。我们可以点击“添加条件”来添加自己的规则。
将图中 规则列表规则 前面的框打√，再将后面的情景模式设置为 SS，意思是规则列表中的内容，我们使用 SS 情景模式。然后规则列表设置中：
> 规则列表格式： AutoProxy
规则列表网址： https://raw.githubusercontent.com/gfwlist/gfwlist/master/gfwlist.txt
{.is-info}

输入上面的网址后请点击“立即更新情景模式”，更新成功后可以看到下面的更新时间和内容，这样设置完成 “规则列表规则” 后就不需要在切换规则中一个一个添加条件了。
切换规则 最后一行的“默认情景模式”代表不在规则列表中网址我们使用“直接连接”情景模式，也就是说不走代理。

**③ PAC情景模式**

主要根据 PAC 文件里面的规则来访问网络。下图以配置 Shadowsocks 的 PAC 代理为例。
![switchyomega3.png](/images/switchyomega3.png)

输入可用的 PAC 网址，点击“立即更新情景模式”，更新成功后下面会提示更新时间，PAC 脚本会出现更新的内容。

## 2、导入导出

在导入导出页面点击“从备份文件恢复”。SwitchyOmega 项目有提供备份文件，可以自己下载使用。如果打开来是个网页请直接右键另存为。此外如果曾经在 SwitchySharp 里配置过，在这里可以直接使用 SwitchySharp 导出的备份文件。

![switchyomega4.png](/images/switchyomega4.png)

另外也可以使用在线 URL 来恢复备份。
启用同步可以将设置和情景模式同步到所有使用 Chrome 浏览器的桌面设备。

> 同步服务由 Chrome Sync 提供，而此服务会上传数据到谷歌。 Chrome Sync 需要您登录 Chrome，但此过程中 SwitchyOmega 无法获取您的账户信息。关于数据同步服务，请查看谷歌隐私政策。
{.is-warning}

## 3、DNS 和 SOCKS 代理
在 Chromium 浏览器（以及基于 Chromium 的所有浏览器）中使用 SOCKS 代理时，部分 DNS 请求不会经过服务器发送（英文参考资料）。这是由 DNS 预加载造成的。以下引用 Chromium 浏览器代理信息页面的文字：
> Note that some traffic such as DNS prefetching will NOT go through the proxy server. To prevent the browser from doing local DNS resolves try adding this command line flag:
{.is-info}

> –host-resolver-rules=“MAP * ~NOTFOUND , EXCLUDE 127.0.0.1”

要防止DNS请求泄露，请使用以上命令行参数（请将 127.0.0.1 替换成您使用的代理主机地址）。或者您也可以在Chromium选项中完全禁止DNS预加载。请在选项的”Show advanced settings…“下方取消选择此选项：
> [ ] 预测网络操作，以提高网页加载速度

附件：
-[switchyomega_chromium.zip](/switchyomega/switchyomega_chromium.zip)
-[omegaoptions.bak](/switchyomega/omegaoptions.bak)
-[proxy_switchyomega-2.5.20-an+fx.xpi](/switchyomega/proxy_switchyomega-2.5.20-an+fx.xpi)
-[switchyomega_chromium.crx](/switchyomega/switchyomega_chromium.crx)

