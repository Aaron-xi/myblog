---
title: rclone+alist自动备份memos数据到网盘
date: 2026-03-07T23:00:00.000Z
tags:
  - 技术分享
---
<p>1.reclone config设置<br>新建一个aliyunbackup名字的reclone<br>Editing existing "aliyunbackup" remote with options:</p>

<!-- /wp:paragraph -->



<!-- wp:list -->

<ul class="wp-block-list"><!-- wp:list-item -->

<li>type: webdav</li>

<!-- /wp:list-item -->



<!-- wp:list-item -->

<li>url: http://192.168.124.24:5244/dav/aliyun/backup</li>

<!-- /wp:list-item -->



<!-- wp:list-item -->

<li>vendor: other</li>

<!-- /wp:list-item -->



<!-- wp:list-item -->

<li>user: jfklx</li>

<!-- /wp:list-item -->



<!-- wp:list-item -->

<li>pass: \*\*\* ENCRYPTED \*\*\*</li>

<!-- /wp:list-item --></ul>

<!-- /wp:list -->



<!-- wp:paragraph -->

<p>2.查看是否挂载成功<br>rclone lsd aliyunbackup:</p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p>3.添加脚本/path/to/memos_backup.sh 内容为：<br>rclone sync -v /mnt/docker/memos/ aliyunbackup:/memos/ \<br>--log-file=/var/log/rclone.log \<br>--exclude "*.tmp"</p>

<!-- /wp:paragraph -->



<!-- wp:paragraph {"style":{"elements":{"link":{"color":{"text":"var:preset|color|accent-3"}}}},"textColor":"accent-3"} -->

<p class="has-accent-3-color has-text-color has-link-color"><strong>注意：</strong>a、为了避免错误，脚本内容用单行命令更好一些rclone sync -v /mnt/docker/memos/ aliyunbackup:/memos/ --log-file=/var/log/rclone.log --exclude "*.tmp"</p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p>          b、脚本的权限问题：添加执行权限（所有用户） </p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p>chmod +x /path/to/memos_backup.sh</p>

<!-- /wp:paragraph -->



<!-- wp:heading {"level":1,"fontSize":"medium"} -->

<h1 class="wp-block-heading has-medium-font-size">验证权限变更     ls -l /path/to/memos_backup.sh</h1>

<!-- /wp:heading -->



<!-- wp:paragraph -->

<p>4.添加定时任务，命令crontab -e</p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p>5.选1。/bin/nano 进行编辑</p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p>6.添加一行0 2 \* \* * /path/to/memos_backup.sh #每天2点执行脚本，分 时 日 月 周 \[执行命令]</p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p>7.查看任务列表crontab -l</p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p>8.确保脚本具有执行权限chmod +x /root/backup.sh</p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p>9.手动执行脚本命令/path/to/memos_backup.sh</p>

<!-- /wp:paragraph -->



<!-- wp:paragraph -->

<p></p>

<!-- /wp:paragraph -->
