---
title: Vaultwarden的数据备份
date: 2026-06-09T15:43:00.000Z
published: true
---
Vaultwarden 本身安全性通常没问题（前提是正确部署），但\*\*真正的风险往往不是被黑，而是设备坏、硬盘坏、误删、Docker 数据丢失\*\*。



对于玩客云这种老设备，我建议做\*\*至少 3 层备份\*\*。



\## 方法一：直接备份 Vaultwarden 数据目录（最推荐）



Vaultwarden 的核心数据一般保存在 Docker 的 volume 或宿主机目录里。



先找数据目录：



如果是 Docker：



\`\``bash

docker inspect vaultwarden

\`\``



重点看：



\`\``text

Mounts

\`\``



例如可能看到：



\`\``text

Source: /DATA/AppData/vaultwarden

Destination: /data

\`\``



说明数据在：



\`\``bash

/DATA/AppData/vaultwarden

\`\``



里面通常有：



\`\``text

db.sqlite3

attachments/

send/

config.json

\`\``



其中最重要的是：



\`\``text

db.sqlite3

\`\``



这是密码数据库。



直接压缩备份：



\`\``bash

tar -czvf vaultwarden_backup.tar.gz /DATA/AppData/vaultwarden

\`\``



或者：



\`\``bash

cp -r /DATA/AppData/vaultwarden /mnt/backup/

\`\``



\---



\## 方法二：定时自动备份（推荐）



写个脚本：



\`\``bash

nano backup_vaultwarden.sh

\`\``



内容：



\`\``bash

\#!/bin/bash



DATE=$(date +%F)



tar -czf /mnt/backup/vaultwarden_$DATE.tar.gz \

/DATA/AppData/vaultwarden



find /mnt/backup -mtime +30 -delete

\`\``



赋执行权限：



\`\``bash

chmod +x backup_vaultwarden.sh

\`\``



每天自动：



\`\``bash

crontab -e

\`\``



加入：



\`\``text

0 3 \* \* * /root/backup_vaultwarden.sh

\`\``



这样每天凌晨自动备份。



\---



\## 方法三：异地备份（强烈建议）



不要只放玩客云里。



方案：



\### A. 同步到 NAS



\`\``bash

rsync -av /DATA/AppData/vaultwarden/ user@nas:/backup/vaultwarden/

\`\``



\---



\### B. 同步到电脑



Windows 可以装：



\* Syncthing



把备份目录同步到电脑。



\---



\### C. 云盘加密备份



先压缩：



\`\``bash

tar -czf vaultwarden.tar.gz vaultwarden

\`\``



再加密：



\`\``bash

gpg -c vaultwarden.tar.gz

\`\``



得到：



\`\``text

vaultwarden.tar.gz.gpg

\`\``



上传到：



\* Google Drive

\* Dropbox

\* Microsoft



即使云盘泄露，没有密码也打不开。



\---



\## 方法四：备份 Bitwarden 导出文件（额外保险）



登录 Vaultwarden Web 页面：



\`\``text

设置 → 导出保险库

\`\``



导出：



\`\``text

JSON

\`\``



或者：



\`\``text

加密 JSON

\`\``



这个相当于保险柜钥匙的另一份副本。



⚠️ JSON 千万不要明文长期放电脑桌面。



\---



\## 方法五：Docker 整体迁移备份



如果以后换设备（比如换 NAS、树莓派、J4125 小主机）：



直接复制：



\`\``text

docker-compose.yml

/data目录

\`\``



再：



\`\``bash

docker compose up -d

\`\``



整个 Vaultwarden 会恢复。



\---



\## 我给你的建议（适合玩客云）



最低配置：



\* 玩客云保留 Vaultwarden

\* 每天自动备份 \`/data\`

\* 每周同步一次到电脑

\* 每月再上传一份加密云备份



这样即使：



\* 玩客云坏了

\* Docker 崩了

\* SD 卡挂了

\* 硬盘挂了



密码都还能恢复。



另外提醒一句：\*\*密码管理器最危险的不是数据库丢失，而是主密码丢失。\*\*主密码一定单独记牢，并考虑打印一份离线保存。
