---
title: clawcloud(爪云)Docker一键部署MoonTV教程
date: 2026-03-07T23:08:00.000Z
tags:
  - 技术分享
---
<p>感谢数字套利大佬分享视频地址<a href="https://www.youtube.com/watch?v=T-EnePTdqv4">claw cloud(爪云)最新MoonTV部署Docker教程 | 白嫖全网最强视频库 | 支持手机/电视/网页 #电影 #电视剧 #视频 #docker #emby</a></p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p><strong>《部署教程说明》</strong></p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p>🎬 MoonTV 是一个开箱即用的、跨平台的影视聚合播放器。它基于 Next.js 14 + Tailwind CSS + TypeScript 构建，支持多资源搜索、在线播放、收藏同步、播放记录、本地/云端存储，让你可以随时随地畅享海量免费影视内容。<a target="_blank" rel="noreferrer noopener" href="https://youtube.com/@am_clubs?sub_confirmation=1">【YouTube频道】 |&nbsp;</a><a target="_blank" rel="noreferrer noopener" href="https://t.me/am_clubs">【Telegram群】 |&nbsp;</a><a target="_blank" rel="noreferrer noopener" href="https://github.com/amclubs">【GitHub仓库】</a></p>

<!-- /wp:paragraph -->



<!-- wp:heading -->

<h2 class="wp-block-heading" id="%E2%9C%A8-%E5%8A%9F%E8%83%BD%E7%89%B9%E6%80%A7">✨ 功能特性</h2>

<!-- /wp:heading -->



<!-- wp:list -->

<ul class="wp-block-list"><!-- wp:list-item -->

<li>🔍 <strong>多源聚合搜索</strong>：内置数十个免费资源站点，一次搜索立刻返回全源结果。</li>

<!-- /wp:list-item -->



<!-- wp:list-item -->

<li>📄 <strong>丰富详情页</strong>：支持剧集列表、演员、年份、简介等完整信息展示。</li>

<!-- /wp:list-item -->



<!-- wp:list-item -->

<li>▶️ <strong>流畅在线播放</strong>：集成 HLS.js &amp; ArtPlayer。</li>

<!-- /wp:list-item -->



<!-- wp:list-item -->

<li>❤️ <strong>收藏 + 继续观看</strong>：支持 Redis/D1/Upstash 存储，多端同步进度。</li>

<!-- /wp:list-item -->



<!-- wp:list-item -->

<li>📱 <strong>PWA</strong>：离线缓存、安装到桌面/主屏，移动端原生体验。</li>

<!-- /wp:list-item -->



<!-- wp:list-item -->

<li>🌗 <strong>响应式布局</strong>：桌面侧边栏 + 移动底部导航，自适应各种屏幕尺寸。</li>

<!-- /wp:list-item -->



<!-- wp:list-item -->

<li>👿 <strong>智能去广告</strong>：自动跳过视频中的切片广告（实验性）</li>

<!-- /wp:list-item --></ul>

<!-- /wp:list -->



<!-- wp:heading -->

<h2 class="wp-block-heading" id="%E4%B8%80%E3%80%81%E9%A1%B9%E7%9B%AE%E6%95%88%E6%9E%9C%E5%9B%BE">一、项目效果图</h2>

<!-- /wp:heading -->



<!-- wp:list -->

<ul class="wp-block-list"><!-- wp:list-item -->

<li><strong>配置视频源</strong> 👉 <a href="https://t.me/AM_CLUBS" target="_blank" rel="noreferrer noopener">点击加入TG群</a>发送关键字 <strong>视频源</strong> 获取下载</li>

<!-- /wp:list-item -->



<!-- wp:list-item -->

<li>点击查看项目截图<a href="https://img.809098.xyz/img/iptv/moontv-01.png"></a></li>

<!-- /wp:list-item --></ul>

<!-- /wp:list -->



<!-- wp:heading -->

<h2 class="wp-block-heading" id="%E4%BA%8C%E3%80%81%E5%87%86%E5%A4%87%E5%B7%A5%E4%BD%9C">二、准备工作</h2>

<!-- /wp:heading -->



<!-- wp:paragraph -->

<p><code>①</code>&nbsp;注册并登录clawcloud 👉 官网：<a target="_blank" rel="noreferrer noopener" href="https://console.run.claw.cloud/signin?link=FGS7Y8E2GQ7X">点击进入clawcloud</a>&nbsp;👉&nbsp;<a target="_blank" rel="noreferrer noopener" href="https://youtu.be/yZpqM3foAd4">点击观看注册视频教程</a></p>

<!-- /wp:paragraph -->



<!-- wp:quote -->

<blockquote class="wp-block-quote"><!-- wp:paragraph -->

<p><strong>💡：</strong>&nbsp;使用 GitHub 登录（建议 GitHub 账号满 180 天）</p>

<!-- /wp:paragraph --></blockquote>

<!-- /wp:quote -->



<!-- wp:paragraph -->

<p><code>②</code>&nbsp;<strong>Upstash Redis注册</strong></p>

<!-- /wp:paragraph -->



<!-- wp:list {"ordered":true} -->

<ol class="wp-block-list"><!-- wp:list-item -->

<li>在 <a href="https://upstash.com/" target="_blank" rel="noreferrer noopener">upstash</a> 注册账号并新建一个 Redis 实例，名称任意。</li>

<!-- /wp:list-item -->



<!-- wp:list-item -->

<li>复制新数据库的 <strong>HTTPS ENDPOINT 和 TOKEN</strong></li>

<!-- /wp:list-item -->



<!-- wp:list-item -->

<li>返回你的 MoonTV 部署项目，新增环境变量 <strong>UPSTASH_URL 和 UPSTASH_TOKEN</strong>，值为第二步复制的 endpoint 和 token</li>

<!-- /wp:list-item -->



<!-- wp:list-item -->

<li>设置环境变量 NEXT_PUBLIC_STORAGE_TYPE，值为 <strong>upstash</strong>；设置 USERNAME 和 PASSWORD 作为站长账号</li>

<!-- /wp:list-item --></ol>

<!-- /wp:list -->



<!-- wp:quote -->

<blockquote class="wp-block-quote"><!-- wp:paragraph -->

<p><strong>💡：</strong>&nbsp;使用 支持播放记录/收藏功能 才要注册Upstash Redis</p>

<!-- /wp:paragraph --></blockquote>

<!-- /wp:quote -->



<!-- wp:paragraph -->

<p><code>③</code>&nbsp;<strong>AUTH_TOKEN授权码获取 已取消不用授权码了</strong></p>

<!-- /wp:paragraph -->



<!-- wp:heading -->

<h2 class="wp-block-heading" id="%E4%BA%8C%E3%80%81clawcloud%E9%83%A8%E7%BD%B2">二、clawcloud部署</h2>

<!-- /wp:heading -->



<!-- wp:list {"ordered":true} -->

<ol class="wp-block-list"><!-- wp:list-item -->

<li>设置镜像</li>

<!-- /wp:list-item --></ol>

<!-- /wp:list -->



<!-- wp:paragraph -->

<p>bash</p>

<!-- /wp:paragraph -->



<!-- wp:table -->

<figure class="wp-block-table"><table class="has-fixed-layout"><tbody><tr><td>1</td><td>ghcr.io/moontechlab/lunatv:latest</td></tr></tbody></table></figure>

<!-- /wp:table -->



<!-- wp:list {"ordered":true,"start":2} -->

<ol start="2" class="wp-block-list"><!-- wp:list-item -->

<li>设置变量</li>

<!-- /wp:list-item --></ol>

<!-- /wp:list -->



<!-- wp:paragraph -->

<p>bash</p>

<!-- /wp:paragraph -->



<!-- wp:table -->

<figure class="wp-block-table"><table class="has-fixed-layout"><tbody><tr><td>1<br>2<br>3<br>4<br>5</td><td>USERNAME=admin<br>PASSWORD=admin_password<br>NEXT_PUBLIC_STORAGE_TYPE=upstash<br>UPSTASH_URL={上面 https 开头的 HTTPS ENDPOINT}<br>UPSTASH_TOKEN={上面的 TOKEN}</td></tr></tbody></table></figure>

<!-- /wp:table -->



<!-- wp:list {"ordered":true,"start":3} -->

<ol start="3" class="wp-block-list"><!-- wp:list-item -->

<li>访问 <code>默认分配的域名</code> 即可</li>

<!-- /wp:list-item --></ol>

<!-- /wp:list -->



<!-- wp:paragraph -->

<p>三、配置视频源 👉 点击加入TG群发送关键字 视频源 获取下载<br>视频源样例<br>{<br>"cache_time": 7200,<br>"api_site": {<br>"dyttzy": {<br>"api": "http://caiji.dyttzyapi.com/api.php/provide/vod",<br>"name": "电影天堂资源",<br>"detail": "http://caiji.dyttzyapi.com"<br>},<br>"heimuer": {<br>"api": "https://json.heimuer.xyz/api.php/provide/vod",<br>"name": "黑木耳",<br>"detail": "https://heimuer.tv"<br>}<br>}<br>}<br>AI获取免费视频源 \[点击观看视频教程]<br>点击注册grok免费AI https://grok.com<br>四、手机端观看 \[点击观看视频教程]<br>📱 PWA：离线缓存、安装到桌面/主屏，移动端原生体验。</p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p>五、电视端AndroidTV观看 \[点击观看视频教程]<br>目前该项目可以配合 OrionTV 在 Android TV 上使用，可以直接作为 OrionTV 后端</p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p>暂时收藏夹与播放记录和网页端隔离，后续会支持同步用户数据</p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p></p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p>文章转自<a href="https://blog.809098.xyz/moontv-clawcloud/">clawcloud(爪云)最新MoonTV部署教程 Docker一键部署 全网最强影视免费看 支持手机/电视/网页 | 数字套利</a></p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p></p>

<!-- /wp:paragraph -->
