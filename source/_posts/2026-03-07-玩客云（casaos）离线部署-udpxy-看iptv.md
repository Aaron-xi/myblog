---
title: 玩客云（CasaOS）离线部署 udpxy 看IPTV
date: 2026-03-07T23:22:00.000Z
tags:
  - 技术分享
---
<!-- wp:heading {"level":4} -->

<h4 class="wp-block-heading">一、 背景环境</h4>

<!-- /wp:heading -->



<!-- wp:list -->

<ul class="wp-block-list"><!-- wp:list-item -->

<li><strong>硬件：</strong> 玩客云（CPU 架构为 ARMv7 32位）。</li>

<!-- /wp:list-item -->



<!-- wp:list-item -->

<li><strong>系统：</strong> CasaOS (基于 Armbian)。</li>

<!-- /wp:list-item -->



<!-- wp:list-item -->

<li><strong>网络：</strong> * 内置网口 <code>eth0</code> 接局域网（IP: 192.168.124.24）。<!-- wp:list -->

<ul class="wp-block-list"><!-- wp:list-item -->

<li>USB 网卡 <code>enx3cab72beff30</code> 接光猫 ITV 口（用于接收组播信号）。</li>

<!-- /wp:list-item --></ul>

<!-- /wp:list --></li>

<!-- /wp:list-item --></ul>

<!-- /wp:list -->



<!-- wp:separator -->

<hr class="wp-block-separator has-alpha-channel-opacity"/>

<!-- /wp:separator -->



<!-- wp:heading {"level":4} -->

<h4 class="wp-block-heading">二、 操作步骤</h4>

<!-- /wp:heading -->



<!-- wp:heading {"level":5} -->

<h5 class="wp-block-heading">1. 离线获取匹配架构的 Docker 镜像</h5>

<!-- /wp:heading -->



<!-- wp:paragraph -->

<p>由于玩客云无法直接拉取外网镜像，且架构特殊，必须在可联网的电脑上强制下载 ARMv7 版本。</p>

<!-- /wp:paragraph -->



<!-- wp:list -->

<ul class="wp-block-list"><!-- wp:list-item -->

<li><strong>拉取命令：</strong>Bash<code>docker pull --platform linux/arm/v7 vistalba/udpxy</code></li>

<!-- /wp:list-item -->



<!-- wp:list-item -->

<li><strong>导出镜像：</strong>Bash<code>docker save -o udpxy_armv7.tar vistalba/udpxy</code></li>

<!-- /wp:list-item --></ul>

<!-- /wp:list -->



<!-- wp:heading {"level":5} -->

<h5 class="wp-block-heading">2. 镜像传输与加载</h5>

<!-- /wp:heading -->



<!-- wp:list {"ordered":true,"start":1} -->

<ol start="1" class="wp-block-list"><!-- wp:list-item -->

<li>通过 CasaOS 的 <strong>Files</strong> 浏览器，将 <code>udpxy_armv7.tar</code> 上传到 <code>/DATA/Downloads</code> 目录。</li>

<!-- /wp:list-item -->



<!-- wp:list-item -->

<li>通过 SSH 登录玩客云，进入该目录加载镜像：Bash<code>docker load -i /DATA/Downloads/udpxy_armv7.tar</code></li>

<!-- /wp:list-item --></ol>

<!-- /wp:list -->



<!-- wp:heading {"level":5} -->

<h5 class="wp-block-heading">3. 准备 USB 网卡环境（关键）</h5>

<!-- /wp:heading -->



<!-- wp:paragraph -->

<p>Linux 系统中，如果网卡没有 IPv4 地址或处于 Down 状态，udpxy 无法抓包。</p>

<!-- /wp:paragraph -->



<!-- wp:list -->

<ul class="wp-block-list"><!-- wp:list-item -->

<li><strong>激活网卡：</strong>Bash<code>ip link set enx3cab72beff30 up</code></li>

<!-- /wp:list-item -->



<!-- wp:list-item -->

<li><strong>分配“假地址”（静态 IP）：</strong>Bash<code># 只要是不冲突的私有 IP 即可，目的是激活网口的 IPv4 协议栈 ip addr add 192.168.200.1/24 dev enx3cab72beff30</code></li>

<!-- /wp:list-item --></ul>

<!-- /wp:list -->



<!-- wp:heading {"level":5} -->

<h5 class="wp-block-heading">4. 部署 Docker 容器</h5>

<!-- /wp:heading -->



<!-- wp:paragraph -->

<p>使用环境变量 <code>UDPXY_OPTS</code> 传递参数，并开启 <code>host</code> 网络模式。</p>

<!-- /wp:paragraph -->



<!-- wp:list -->

<ul class="wp-block-list"><!-- wp:list-item -->

<li><strong>部署命令：</strong>Bash<code>docker run -d \ --name udpxy \ --restart always \ --net=host \ -e UDPXY_OPTS="-p 4022 -c 30 -T -a eth0 -m enx3cab72beff30" \ vistalba/udpxy</code><!-- wp:list -->

<ul class="wp-block-list"><!-- wp:list-item -->

<li><code>-p 4022</code>: 监听端口。</li>

<!-- /wp:list-item -->



<!-- wp:list-item -->

<li><code>-T</code>: 必须包含，防止容器作为后台进程直接退出。</li>

<!-- /wp:list-item -->



<!-- wp:list-item -->

<li><code>-a eth0</code>: 绑定分发信号的网卡。</li>

<!-- /wp:list-item -->



<!-- wp:list-item -->

<li><code>-m enx3cab72beff30</code>: 绑定接收信号的 USB 网卡。</li>

<!-- /wp:list-item --></ul>

<!-- /wp:list --></li>

<!-- /wp:list-item --></ul>

<!-- /wp:list -->



<!-- wp:separator -->

<hr class="wp-block-separator has-alpha-channel-opacity"/>

<!-- /wp:separator -->



<!-- wp:heading {"level":4} -->

<h4 class="wp-block-heading">三、 验证与播放</h4>

<!-- /wp:heading -->



<!-- wp:list {"ordered":true,"start":1} -->

<ol start="1" class="wp-block-list"><!-- wp:list-item -->

<li><strong>状态页验证：</strong> 浏览器访问 <code>http://192.168.124.24:4022/status</code>。</li>

<!-- /wp:list-item -->



<!-- wp:list-item -->

<li><strong>播放地址格式：</strong><!-- wp:list -->

<ul class="wp-block-list"><!-- wp:list-item -->

<li>原始组播地址：<code>udp://239.254.200.9:8264</code></li>

<!-- /wp:list-item -->



<!-- wp:list-item -->

<li>udpxy 转发地址：<code>http://192.168.124.24:4022/udp/239.254.200.9:8264</code></li>

<!-- /wp:list-item --></ul>

<!-- /wp:list --></li>

<!-- /wp:list-item --></ol>

<!-- /wp:list -->



<!-- wp:separator -->

<hr class="wp-block-separator has-alpha-channel-opacity"/>

<!-- /wp:separator -->



<!-- wp:heading {"level":4} -->

<h4 class="wp-block-heading">四、 进阶：如何让“假地址”在开机后自动生效？</h4>

<!-- /wp:heading -->



<!-- wp:paragraph -->

<p>玩客云重启后，手动执行的 <code>ip addr</code> 命令会失效。你可以把激活命令写进 CasaOS 的启动脚本或系统的 <code>rc.local</code> 中。</p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p><strong>简单方法：</strong> 在 CasaOS 的终端执行：</p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p>Bash</p>

<!-- /wp:paragraph -->



<!-- wp:code -->

<pre class="wp-block-code"><code>crontab -e

</code></pre>

<!-- /wp:code -->



<!-- wp:paragraph -->

<p>在末尾添加一行（重启后自动激活网卡并补全 IP）：</p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p>Bash</p>

<!-- /wp:paragraph -->



<!-- wp:code -->

<pre class="wp-block-code"><code>@reboot sleep 30 &amp;&amp; ip link set enx3cab72beff30 up &amp;&amp; ip addr add 192.168.200.1/24 dev enx3cab72beff30

</code></pre>

<!-- /wp:code -->



<!-- wp:separator -->

<hr class="wp-block-separator has-alpha-channel-opacity"/>

<!-- /wp:separator -->



<!-- wp:paragraph -->

<p><strong>心得总结：</strong> 这次成功的核心在于：</p>

<!-- /wp:paragraph -->



<!-- wp:list {"ordered":true,"start":1} -->

<ol start="1" class="wp-block-list"><!-- wp:list-item -->

<li><strong>镜像架构锁定</strong>：确保了 ARMv7 版本的正确性。</li>

<!-- /wp:list-item -->



<!-- wp:list-item -->

<li><strong>环境变量传参</strong>：顺应了镜像作者定义的 <code>UDPXY_OPTS</code> 规则。</li>

<!-- /wp:list-item -->



<!-- wp:list-item -->

<li><strong>激活物理链路</strong>：通过“假地址”解决了 Linux 接口无载波（No Carrier）导致程序崩溃的问题。</li>

<!-- /wp:list-item --></ol>

<!-- /wp:list -->



<!-- wp:paragraph -->

<p></p>

<!-- /wp:paragraph -->
