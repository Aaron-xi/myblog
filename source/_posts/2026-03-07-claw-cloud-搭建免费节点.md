---
title: Claw Cloud 搭建免费节点
date: 2026-03-07T22:52:00.000Z
tags:
  - 技术分享
---
<p>大佬博客链接：<a href="https://tweek.top/archives/1745141133212">白嫖不寒酸！Claw Cloud 免费 VPS 教程 + 节点部署保姆级教学（无需信用卡） | Tweek</a></p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p>1.服务器选新加坡</p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p>2.进入App Launchpad → Create App，选择镜像名：metaligh/3x-ui</p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p>配置推荐：</p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p>CPU：<strong>1 核</strong></p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p>内存：<strong>512M</strong></p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p>地区：选择 <strong>Singapore</strong></p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p>网络端口设置：</p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p>开启 <strong>80 端口</strong></p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p>添加并开启 <strong>2053 端口</strong></p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p>所有端口都选 <strong>Public（公网）</strong></p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p>存储添加：</p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p>本地挂载两个目录：复制编辑<code>/etc/x-ui/</code></p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p><code>/etc/letsencrypt/</code></p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p>点击 <strong>Deploy Application（部署应用）</strong></p>

<!-- /wp:paragraph -->



<!-- wp:separator -->

<hr class="wp-block-separator has-alpha-channel-opacity"/>

<!-- /wp:separator -->



<!-- wp:heading {"level":3} -->

<h3 class="wp-block-heading" id="%F0%9F%A7%A9-%E7%AC%AC%E4%B8%89%E6%AD%A5%EF%BC%9A%E7%99%BB%E5%BD%95-3x-ui-%E7%AE%A1%E7%90%86%E9%9D%A2%E6%9D%BF">🧩 第三步：登录 3x-ui 管理面板</h3>

<!-- /wp:heading -->



<!-- wp:list -->

<ul class="wp-block-list"><!-- wp:list-item -->

<li>部署状态变为 <code>Running</code> 后</li>

<!-- /wp:list-item -->



<!-- wp:list-item -->

<li>打开 <strong>2053 端口对应的网络地址</strong>，进入管理后台</li>

<!-- /wp:list-item -->



<!-- wp:list-item -->

<li>默认登录信息：<code>pgsql</code><strong>Undefined</strong>复制编辑<code>用户名：admin 密码：admin</code></li>

<!-- /wp:list-item --></ul>

<!-- /wp:list -->



<!-- wp:quote -->

<blockquote class="wp-block-quote"><!-- wp:paragraph -->

<p>登录后请务必第一时间修改用户名和密码，确保安全！</p>

<!-- /wp:paragraph --></blockquote>

<!-- /wp:quote -->



<!-- wp:separator -->

<hr class="wp-block-separator has-alpha-channel-opacity"/>

<!-- /wp:separator -->



<!-- wp:heading {"level":3} -->

<h3 class="wp-block-heading" id="%F0%9F%A7%A9-%E7%AC%AC%E5%9B%9B%E6%AD%A5%EF%BC%9A%E5%88%9B%E5%BB%BA-vless-%E8%8A%82%E7%82%B9">🧩 第四步：创建 VLESS 节点</h3>

<!-- /wp:heading -->



<!-- wp:paragraph -->

<p>创建成功后，可直接导入到 v2ray / Clash 工具中使用</p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p>创建节点时选择：</p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p>类型：<strong>VLESS</strong></p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p>传输协议：<strong>WS</strong></p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p>端口配置：</p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p>将默认端口修改为 <strong>443</strong></p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p>地址填写为 VPS 的 <strong>80 端口链接</strong></p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p>启用 TLS</p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p></p>

<!-- /wp:paragraph -->
