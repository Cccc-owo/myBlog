---
title: 关于Bitmap font字体贴图
tags:
  - EU4
  - Bitmap-font
categories:
  - 技术
comments: true
sitemap: true
abbrlink: 8b51873a
date: 2022-08-23 15:09:18
updated: 2022-08-23 15:09:18
---

>Bitmap font 是 P 社的 Clausewitz 引擎所使用的一种字体格式（当然现在也能用 TTF），这种字体的特点是所有文字都是栅格化的，不同于 ttf 等矢量格式的字体。所有字符绘制在一张或多张像素图片（通常为 dds 或 tga）上，再通过一个定义文件（fnt）来描述每个字符在图片中的位置，引擎就可以以此配置来读取并将字符显示到界面中。

<!-- more -->

---

## 前言

关于如何制作P社游戏字体，在[这里](https://paratranz.cn/blog?category=document)有一个大概的教程，我不赘述了。

本文就分享一下我制作P社游戏（EU4）的地图字体的经验吧。

## 字体选择？

> ParaTranz站长的小贴士：
>
> 建议选择 GBK 字符集的字体，可以从[方正字体](http://www.foundertype.com/)的官网上选择一款你喜欢的字体

一开始，我选择了 ```方正北魏楷书/方正新楷体``` 作为地图字体，详情可见[这个帖子](https://tieba.baidu.com/p/7968865688)。

然而，我发现自制字体的效果好像还不如 ```盛世楷书```（即原汉化mod自带的字体），问题主要有两点：

1. 两种字体不带描边的话，在某些深色的地方显示效果不好；带上白色描边，则又显得比较丑。
2. 方正新楷体在默认不加粗的情况下，看起来太细了，而在软件中机器加粗可能会导致字体笔画粘连。

对于第一个问题，我经过了一些钻研，找到了解决方案：给字体加灰色阴影。

对于第二个问题，我选择更换字体。经过观察，```方正公文楷体``` 会是一个比较好的选择。*顺带一提， 「东亚·天朝日不落」 的地图字体也是这个。*

## 给字体贴图加阴影

由于[此文](https://paratranz.cn/blog?category=document)没有给出为字体添加阴影的教程，于是我自己研究出了一个方法。

我的方法未必是最好的，如果你有什么建议，可以在评论区留言交流。

### 准备

- 软件：[GIMP](https://www.gimp.org/downloads/)
- 一张字体贴图（.dds文件）

### 步骤

1 ) 首先通过[bmfont generator](http://www.angelcode.com/products/bmfont/)生成字体贴图，教程在上面有贴出链接。

!*注意在 bmfont 的 Export Options 中 Compression 请设置为 None，压缩我们放在后面导出字体贴图时再进行。*

2 ) 以 ```GIMP``` 打开dds贴图文件。会弹出一个框，不用管那么多，直接 "OK" 确认即可。

![1](https://drive.iscccc.eu.org/api/raw/?path=/Img%C2%B7%E5%9B%BE%E5%BA%8A/bitmap-font/1.png)

3 ) 在窗口标题下的那一栏找到 ```滤镜``` -> ```光照和阴影``` -> ```投影```

![2](https://drive.iscccc.eu.org/api/raw/?path=/Img%C2%B7%E5%9B%BE%E5%BA%8A/bitmap-font/2.png)

4 ) 依照下图的参数调整，其中 ```Grow radius``` 个人建议设置为 1~2 ，不易太高，否则阴影范围会很大，也不能小于等于0，这样就没有效果

![3](https://drive.iscccc.eu.org/api/raw/?path=/Img%C2%B7%E5%9B%BE%E5%BA%8A/bitmap-font/3.png)

这是 ```Grow radius``` 调为 3 的效果，阴影会比较明显，但是显示出来的效果不一定就好（为方便观察，我加了一个白色背景，请忽略）：

![4](https://drive.iscccc.eu.org/api/raw/?path=/Img%C2%B7%E5%9B%BE%E5%BA%8A/bitmap-font/4.png)

5 ) 就这样，阴影就加完了。接下来就要保存。具体见下图操作。

选择 ```文件``` -> ```导出为```

![5](https://drive.iscccc.eu.org/api/raw/?path=/Img%C2%B7%E5%9B%BE%E5%BA%8A/bitmap-font/5.png)

在打开的界面中，将文件命名为 ```zh-hans-map.dds``` ，并点击 ```导出```。

![6](https://drive.iscccc.eu.org/api/raw/?path=/Img%C2%B7%E5%9B%BE%E5%BA%8A/bitmap-font/6.png)

在又打开的一个新窗口中，按如下配置：

![7](https://drive.iscccc.eu.org/api/raw/?path=/Img%C2%B7%E5%9B%BE%E5%BA%8A/bitmap-font/7.png)

确保无误后即可点击 ```Export``` 导出了。

6 ) 到此为止，加阴影的教程就结束了，接下来的操作就是将生成的文件进行处理后照一般操作将其放入 ```gfx/fonts/``` 文件夹内。

## 字体贴图制作的小经验

由于我们制作的是地图字体，所以在 ```bmfont``` 中 ```Font Settings``` 的 ```Size``` 不易过小，建议为 60~90 左右，否则会比较不清晰。

另外，要注意控制dds文件的大小，过大可能会导致无法显示文字。

感谢你看到这里，欢迎在评论区中交流！

<!-- Q.E.D. -->