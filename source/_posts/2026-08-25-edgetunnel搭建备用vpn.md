---
title: edgetunnel搭建备用VPN
date: 2026-08-25T16:01:00.000Z
published: true
tags:
  - 技术分享
---
博客地址

https://kjgx668.blogspot.com/2026/08/edgetunnel-vpn-vpn-cloudflare-8k-ipai.html#google_vignette

⚙️ Workers 部署

「 Workers 部署文字教程 」

部署 CF Worker：

在 CF Worker 控制台中创建一个新的 Worker。

将 worker.js 的内容粘贴到 Worker 编辑器中。

在左侧的 设置选项卡中，选择 变量 > 添加变量。 变量名称填写ADMIN，值则为你的管理员密码，后点击 保存即可。

绑定 KV 命名空间：

在 绑定选项卡中选择 添加绑定 + > KV 命名空间 > 添加绑定，然后选择一个已有的命名空间或创建一个新的命名空间进行绑定。

变量名称填写KV，然后点击 添加绑定即可。

给 Workers绑定 自定义域：

在 workers控制台的 触发器选项卡，下方点击 添加自定义域。

填入你已转入 CF 域名解析服务的次级域名，例如:vless.google.com后 点击添加自定义域，等待证书生效即可。

访问后台：

访问 https://vless.google.com/admin 输入管理员密码即可登录后台。

🛠 Pages 上传 部署方法 最佳推荐!!! 图文教程

「 Pages 上传文件部署文字教程 」

部署 CF Pages：

下载 main.zip 文件，并点上 Star !!!

在 CF Pages 控制台中选择 上传资产后，为你的项目取名后点击 创建项目，然后上传你下载好的 main.zip 文件后点击 部署站点。

部署完成后点击 继续处理站点 后，选择 设置 > 环境变量 > 制作为生产环境定义变量 > 添加变量。 变量名称填写ADMIN，值则为你的管理员密码，后点击 保存即可。

返回 部署 选项卡，在右下角点击 创建新部署 后，重新上传 main.zip 文件后点击 保存并部署 即可。

绑定 KV 命名空间：

在 设置选项卡中选择 绑定 > + 添加 > KV 命名空间，然后选择一个已有的命名空间或创建一个新的命名空间进行绑定。

变量名称填写KV，然后点击 保存后重试部署即可。

给 Pages绑定 CNAME自定义域：视频教程

在 Pages控制台的 自定义域选项卡，下方点击 设置自定义域。

填入你的自定义次级域名，注意不要使用你的根域名，例如： 您分配到的域名是 fuck.cloudns.biz，则添加自定义域填入 lizi.fuck.cloudns.biz即可；

按照 CF 的要求将返回你的域名DNS服务商，添加 该自定义域 lizi的 CNAME记录 edgetunnel.pages.dev 后，点击 激活域即可。

访问后台：

访问 https://lizi.fuck.cloudns.biz/admin 输入管理员密码即可登录后台。

🛠 Pages + GitHub 部署方法

「 Pages + GitHub 部署文字教程 」

部署 CF Pages：

在 Github 上先 Fork 本项目，并点上 Star !!!

在 CF Pages 控制台中选择 连接到 Git后，选中 edgetunnel项目后点击 开始设置。

在 设置构建和部署页面下方，选择 环境变量（高级）后并 添加变量 变量名称填写ADMIN，值则为你的管理员密码，后点击 保存并部署即可。

绑定 KV 命名空间：

在 设置选项卡中选择 绑定 > + 添加 > KV 命名空间，然后选择一个已有的命名空间或创建一个新的命名空间进行绑定。

变量名称填写KV，然后点击 保存后重试部署即可。

给 Pages绑定 CNAME自定义域：视频教程

在 Pages控制台的 自定义域选项卡，下方点击 设置自定义域。

填入你的自定义次级域名，注意不要使用你的根域名，例如： 您分配到的域名是 fuck.cloudns.biz，则添加自定义域填入 lizi.fuck.cloudns.biz即可；

按照 CF 的要求将返回你的域名DNS服务商，添加 该自定义域 lizi的 CNAME记录 edgetunnel.pages.dev 后，点击 激活域即可。

访问后台：

访问 https://lizi.fuck.cloudns.biz/admin 输入管理员密码即可登录后台。

点击我是高手要折腾

Encrypted Client Hello 设置为启动 保存

优选订阅生成   模式改为自定义

删除原优选地址，https://github.com/LancelotRar/best-cf-ips中获取IP API和DOMAIN API新地址 保存

获取节点自适应链接订阅
