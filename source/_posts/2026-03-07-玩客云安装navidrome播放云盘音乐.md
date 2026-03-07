---
title: 玩客云安装navidrome播放云盘音乐
date: 2026-03-07T22:54:00.000Z
tags:
  - 技术分享
---
<p>aliyundrive-fuse映射云盘到本地</p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p>nohup aliyundrive-fuse -r （refreshtoken） -w /var/run/aliyundrive-fuse /mnt/aliyundrive &gt; /var/log/aliyundrive-fuse.log 2&gt;&amp;1 &amp;</p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p><strong><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-accent-3-color">安装navidrome</mark></strong></p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p>1.安装命令<br>docker run -d \<br>--name navidrome \<br>-v /mnt/aliyundrive/ziyuan/music:/music:ro \<br>-v /DATA/AppData/Navidrome:/data \<br>-p 4533:4533 \<br>deluan/navidrome:latest</p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p>2.验证音乐库路径是否存在：<br>ls /mnt/aliyundrive/ziyuan/music # 确认路径存在且可访问</p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p>如果路径不存在，需检查阿里云盘挂载状态：<br>mount | grep aliyundrive # 查看挂载点是否生效</p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p>创建数据存储目录（如果尚未创建）：<br>mkdir -p /DATA/AppData/Navidrome # 确保宿主机目录存在<br>chmod 755 /DATA/AppData/Navidrome # 赋予必要权限</p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p>3.完整执行命令<br>docker run -d --name navidrome -v /mnt/aliyundrive/ziyuan/music:/music:ro -v /DATA/AppData/Navidrome:/data -p 4533:4533 deluan/navidrome:latest</p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p>验证操作<br>1.检查容器状态：<br>docker ps -a | grep navidrome # 确认容器已运行且无报错</p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p>2.查看挂载路径：<br>docker inspect navidrome | grep -A 10 "Mounts" # 验证宿主机路径是否正确映射</p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p>3.观察日志：<br>docker logs navidrome # 确认日志中显示 <code>absoluteLibPath=/music</code></p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p>可能遇到的权限问题<br>如果阿里云盘挂载路径 (/mnt/aliyundrive/ziyuan/music) 存在访问限制，需调整挂载权限：</p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p>1.检查挂载参数：确保挂载时添加 allow_other 选项（适用于 rclone 或 aliyundrive-fuse）：<br>rclone mount aliyundrive: /mnt/aliyundrive --allow-other --vfs-cache-mode writes</p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p>2.修改目录权限：<br>chmod 755 /mnt/aliyundrive/ziyuan/music # 开放读权限</p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p></p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p></p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p>4.将刚上传到阿里云盘的歌曲更新到本地挂载目录 /mnt/aliyunmusic，解决方法：重启 systemd 挂载服务（推荐，简单有效）<br>sudo systemctl restart rclone-aliyun<br>这会重新挂载 WebDAV，强制刷新目录结构和缓存，新上传的歌曲即可在/mnt/aliyunmusic 中显示。</p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p>5.重启navidrome服务可刷新歌曲列表到客户端。</p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p></p>

<!-- /wp:paragraph -->
