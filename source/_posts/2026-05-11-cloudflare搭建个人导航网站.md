---
title: cloudflare搭建个人导航网站
date: 2026-05-11T13:40:00.000Z
published: true
tags:
  - 技术分享
---
``

感谢爱分享的marco大佬分享<https://www.youtube.com/watch?v=BYIOKbpaalw>

[](https://www.youtube.com/watch?v=BYIOKbpaalw)

通过cloudflare免费搭建一个自己的导航页面

首先我们通过浏览器打开github上的这个开源项目https://github.com/shiteThings/Cloudflare-Navihive

fork本仓库，修改wrangler.template.jsonc为wrangler.jsonc

点击上方的"Deploy to Cloudflare Workers"按钮

登录您的 Cloudflare 账号

在部署界面上，您需要配置以下内容：

项目名称：为您的导航站项目取个名字

D1 数据库：点击"创建新数据库"，命名为navigation-db

环境变量：

AUTH_ENABLED：设置为true启用登录认证

AUTH_USERNAME：管理员用户名

AUTH_PASSWORD：管理员密码

AUTH_SECRET：JWT 密钥（使用随机字符串）

点击"部署"按钮

部署完成后，您将获得一个类似https://your-project-name.username.workers.dev的网址，这就是您的导航站地址。

初始化项目数据库

登录您的 Cloudflare 控制台

进入"Workers & Pages"部分

选择您刚刚部署的项目

在左侧菜单中点击"设置" > "数据库"，您将看到已绑定的数据库（名为"navigation-db"）

点击数据库名称以进入数据库管理界面：

数据库管理界面

在数据库管理界面，点击"控制台"选项卡进入SQL编辑器

在SQL编辑器中，逐个复制并粘贴以下SQL命令：

\-- 创建分组表

CREATE TABLE IF NOT EXISTS groups (

\    id INTEGER PRIMARY KEY AUTOINCREMENT, 

\    name TEXT NOT NULL, 

\    order_num INTEGER NOT NULL, 

\    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP, 

\    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP

);

\-- 创建站点表

CREATE TABLE IF NOT EXISTS sites (

\    id INTEGER PRIMARY KEY AUTOINCREMENT, 

\    group_id INTEGER NOT NULL, 

\    name TEXT NOT NULL, 

\    url TEXT NOT NULL, 

\    icon TEXT, 

\    description TEXT, 

\    notes TEXT, 

\    order_num INTEGER NOT NULL, 

\    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP, 

\    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP, 

\    FOREIGN KEY (group_id) REFERENCES groups(id) ON DELETE CASCADE

);

\-- 创建配置表

CREATE TABLE IF NOT EXISTS configs (

\    key TEXT PRIMARY KEY,

\    value TEXT NOT NULL,

\    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,

\    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP

);

\-- 设置初始化标志

INSERT INTO configs (key, value) VALUES ('DB_INITIALIZED', 'true');

点击"运行"按钮执行SQL命令：

SQL编辑器界面

如果SQL命令执行成功，您将看到"查询成功"的提示信息

至此，数据库初始化完成，您可以访问您的导航站首页并使用配置的管理员账号登录
