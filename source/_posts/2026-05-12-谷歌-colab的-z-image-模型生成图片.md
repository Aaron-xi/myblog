---
title: 谷歌 Colab的 Z-Image 模型生成图片
date: 2026-05-12T21:34:00.000Z
published: true
tags:
  - 技术分享
---
<iframe width="560" height="315" src="https://www.youtube.com/embed/6p0SUVxioTs?si=FiNls74VWRAQ4IEp" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
操作流程：使用 Google Colab 免费运行 Z-Image 图像生成器
安装 Colaboratory 应用（仅首次）

打开 Google Drive。

点击左上角「新建」→「更多」→「连接更多应用」。

搜索「Collaboratory」，安装第一个结果。

创建并配置 Colab 笔记本

打开准备好的 Colab 链接。

点击菜单栏「文件」→「在 Drive 中保存副本」，系统将自动在新页面打开副本文件。

在新页面中，点击「运行时」→「更改运行时类型」。

将「硬件加速器」选为 T4 GPU，保存。

点击右上角「连接」，等待显示 T4 标识（表示 GPU 已就绪，可查看剩余时长；每天约免费 5 小时）。

运行代码

点击「运行全部」（Run all），等待约 10–25 分钟（取决于网速）。

第一段代码运行结束显示「Installation successful」后，第二段代码会自动运行。

等待屏幕出现 Gradio 链接，点击进入项目界面。

使用图像生成界面

提示词：支持中英文，填写在顶部区域。

图片比例：可选 16:9 等。

种子（Seed）：相同种子生成相似图片，0 表示随机。

推理步骤：保持默认 9。

CFG：提示词相关度，越高越严格。

去噪（Denoising）：越高图片越精细，越低生成越快。

负面提示词：填写不应出现的元素（可保持原默认值）。

推荐调整：仅修改图片比例和种子。

生成后点击图片上方「下载」链接保存。

注意事项

模型本身无语言翻译能力，如需英文提示词请自行完整提供。

Z-Image 模型无内容限制，完全依据提示词生成。

若生成图片未及时保存，可在 Colab 文件中依次点击「文件」→ ComfyUI → 展开底部「Result」文件夹，其中存放所有历史生成图片。

**下次运行可直接点击Z_Image_Turbo.ipynb”的副本，然后点右上角的连接，然后全部运行，等网页地址生成后，点击进入即可。**
