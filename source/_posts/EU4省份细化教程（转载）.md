---
title: EU4省份细化教程（转载）
description: 看我看我
tags:
  - 游戏
  - EU4
  - 转载
categories:
  - 存档
comments: true
abbrlink: 48376
date: 2021-11-27 23:41:59
subtitle:
---

## EU4省份细化教程

整合自[百度贴吧@Haruka_斑驳](https://tieba.baidu.com/p/6152957843?see_lz=1)

在开始之前，我们需要做好细化准备工作：

notepad++

PS6

上面两个软件，或者能代替的软件。此处随个人喜好选择。

![1](https://cdn.jsdelivr.net/gh/Cccc-owo/blogPic@master/EU4%E7%9C%81%E4%BB%BD%E7%BB%86%E5%8C%96%E6%95%99%E7%A8%8B/1.jpg)

首先向大家简单介绍一下细化所必须的相关文件

如图所示

图上标蓝的 是基础细化必要文件 今天我只讲最基础的细化

只涉及area、climate、continent、default、definition、positions以及terrain

这些个文件有空的时候你们可以自己看看文件构成，或者去维基百科看看

首先向大家简单介绍一下细化所必须的相关文件

首先需要明确的一点是，细化修改文件只能在原版的基础上进行修改

这意味着，细化MOD互相间都不可能兼容

首先我们创建一个新的MOD文件

![3](https://cdn.jsdelivr.net/gh/Cccc-owo/blogPic@master/EU4%E7%9C%81%E4%BB%BD%E7%BB%86%E5%8C%96%E6%95%99%E7%A8%8B/3.png)

直接叫map_test好了

然后新建一个.mod文件

![4](https://cdn.jsdelivr.net/gh/Cccc-owo/blogPic@master/EU4%E7%9C%81%E4%BB%BD%E7%BB%86%E5%8C%96%E6%95%99%E7%A8%8B/4.png)

name 是你在游戏启动器界面 你这个MOD会显示的名字

path 是mod路径

tags是在启动器界面鼠标移动到MOD名字的时候，会显示的标签

supported_version是该MOD支持的版本 如图所示 1.28

![5](https://cdn.jsdelivr.net/gh/Cccc-owo/blogPic@master/EU4%E7%9C%81%E4%BB%BD%E7%BB%86%E5%8C%96%E6%95%99%E7%A8%8B/5.png)

最简单的细化MOD 只包含这3个文件夹

common里头，只包含这俩文件夹

分别是贸易公司归属

贸易区归属

history文件夹 只包含省份历史文件夹

common和history 是后面收尾的处理工作 此处先不讲

![6](https://cdn.jsdelivr.net/gh/Cccc-owo/blogPic@master/EU4%E7%9C%81%E4%BB%BD%E7%BB%86%E5%8C%96%E6%95%99%E7%A8%8B/6.png)

在map文件夹里，根据你细化程度的多少 必要文件也会相对应有所变化

这四个文件是最低限度的细化文件 缺一不可

少了一个 MOD就会报错闪退

首先我们打开definition文件

![7](https://cdn.jsdelivr.net/gh/Cccc-owo/blogPic@master/EU4%E7%9C%81%E4%BB%BD%E7%BB%86%E5%8C%96%E6%95%99%E7%A8%8B/7.png)

打开后是这样的 我们可以看到，P社给了注释

格式是：

省份ID;R;G;B;备忘栏;x

注意这里的分号是英文输入法下的分号

x是小写

往下拉到最低层

![8](https://cdn.jsdelivr.net/gh/Cccc-owo/blogPic@master/EU4%E7%9C%81%E4%BB%BD%E7%BB%86%E5%8C%96%E6%95%99%E7%A8%8B/8.png)

可以看到EU41.28版本，共有4650个省份

一般来说 我们细化就是直接在4650后面接上4651

不过这里我教大家一个小技巧

你可以直接像我一样

![9](https://cdn.jsdelivr.net/gh/Cccc-owo/blogPic@master/EU4%E7%9C%81%E4%BB%BD%E7%BB%86%E5%8C%96%E6%95%99%E7%A8%8B/9.png)

从5000开始

我的日不落MOD是从6000开始的

这么做的意义何在呢？答案是为了方便P社后面亲自弄细化

你移植自己的MOD时，不用跟着P社的屁股后头 一个个改你已经细化好的省份ID

这么做的代价 仅仅是会让游戏报错文件多出几行错误日志而已 并不影响大体

我们输入5000;192;153;156;prov5000;x

注意RGB的数值必须是独一无二的

每个省份只能对应一个RGB数据

RGB撞车的记录 大概是1/1700W

你能撞上 基本可以去试试买彩票了

我们可以利用excal表格的随机函数 从0-255内自动生成数值

![10](https://cdn.jsdelivr.net/gh/Cccc-owo/blogPic@master/EU4%E7%9C%81%E4%BB%BD%E7%BB%86%E5%8C%96%E6%95%99%E7%A8%8B/10.png)

添加好后 我们保存退出

![11](https://cdn.jsdelivr.net/gh/Cccc-owo/blogPic@master/EU4%E7%9C%81%E4%BB%BD%E7%BB%86%E5%8C%96%E6%95%99%E7%A8%8B/11.png)

打开default

![12](https://cdn.jsdelivr.net/gh/Cccc-owo/blogPic@master/EU4%E7%9C%81%E4%BB%BD%E7%BB%86%E5%8C%96%E6%95%99%E7%A8%8B/12.png)

把最高省份ID 改为5001

就是你definition中 最大ID再加一个

不要问我为什么要多加一个 P社就是这么设定的

这里简单介绍一下default文件

|英文|翻译|
|----|----|
|sea_starts|海域省份|
|only_used_for_random|只用于随机新大陆的省份|
|lakes|湖泊省份|

其他的内容 基本用不上 此处就不讲了

设定好5001后 保存文件

其他的内容 基本用不上 此处就不讲了

设定好5001后 保存文件

![13](https://cdn.jsdelivr.net/gh/Cccc-owo/blogPic@master/EU4%E7%9C%81%E4%BB%BD%E7%BB%86%E5%8C%96%E6%95%99%E7%A8%8B/13.jpg)

此处输入ID为5000的省份RGB数值

![14](https://cdn.jsdelivr.net/gh/Cccc-owo/blogPic@master/EU4%E7%9C%81%E4%BB%BD%E7%BB%86%E5%8C%96%E6%95%99%E7%A8%8B/14.png)

我们就画个松江（上海）出来吧

![15](https://cdn.jsdelivr.net/gh/Cccc-owo/blogPic@master/EU4%E7%9C%81%E4%BB%BD%E7%BB%86%E5%8C%96%E6%95%99%E7%A8%8B/15.png)

PS选择好画笔工具 选择铅笔工具

![16](https://cdn.jsdelivr.net/gh/Cccc-owo/blogPic@master/EU4%E7%9C%81%E4%BB%BD%E7%BB%86%E5%8C%96%E6%95%99%E7%A8%8B/16.png)

然后拉一条线

想画的跟历史边界一样 就得自己下功夫比照历史边界 一点点修改

这里就随意画了

![17](https://cdn.jsdelivr.net/gh/Cccc-owo/blogPic@master/EU4%E7%9C%81%E4%BB%BD%E7%BB%86%E5%8C%96%E6%95%99%E7%A8%8B/17.png)

选择魔棒工具

![18](https://cdn.jsdelivr.net/gh/Cccc-owo/blogPic@master/EU4%E7%9C%81%E4%BB%BD%E7%BB%86%E5%8C%96%E6%95%99%E7%A8%8B/18.png)

这里这样设置

容差为1 是为了防止选色的时候串色

不勾选消除锯齿 是为了防止魔棒选取的时候会多选择像素点

![19](https://cdn.jsdelivr.net/gh/Cccc-owo/blogPic@master/EU4%E7%9C%81%E4%BB%BD%E7%BB%86%E5%8C%96%E6%95%99%E7%A8%8B/19.png)

快捷键是alt+del

对魔棒选中区域进行快速涂色

当然你要是自己直接拿铅笔工具涂也行

画好后 我们点保存 退出

![20](https://cdn.jsdelivr.net/gh/Cccc-owo/blogPic@master/EU4%E7%9C%81%E4%BB%BD%E7%BB%86%E5%8C%96%E6%95%99%E7%A8%8B/20.png)

打开area文件

每一省份都有两个属性

一个是地球归属

意思是这个省份属于哪个area，哪个region，哪个superregion 哪个continent climate terrain

不然这省份就是无主之地了 进游戏点选该省份会闪退

这里最低限度得填上area才不会闪退

一个是国家属性

改省份属于哪个国家，或者还是哪个国家都不属于

这个通过history控制，此处不谈

area文件 就是游戏中的地区 的概念

苏州的ID是1822 松江在苏州旁边

![21](https://cdn.jsdelivr.net/gh/Cccc-owo/blogPic@master/EU4%E7%9C%81%E4%BB%BD%E7%BB%86%E5%8C%96%E6%95%99%E7%A8%8B/21.png)

我们直接搜索1822

找到了南江苏area

把ID5000填上去

这就意味这 这5个省份是在同一个area州里头

弄好后 我们保存area

打开continent

![22](https://cdn.jsdelivr.net/gh/Cccc-owo/blogPic@master/EU4%E7%9C%81%E4%BB%BD%E7%BB%86%E5%8C%96%E6%95%99%E7%A8%8B/22.png)

找到亚洲 把5000填进去

然后保存

打开terrain文件

该文件控制每个省份的地形

terrain可不填，不填则由系统随机分配省份的地形

依旧是找到1822

![23](https://cdn.jsdelivr.net/gh/Cccc-owo/blogPic@master/EU4%E7%9C%81%E4%BB%BD%E7%BB%86%E5%8C%96%E6%95%99%E7%A8%8B/23.png)

我们发现1822是被归属到农田地形的 那我们就把5000填进去吧

保存后 我们打开climate

依旧是找到1822

![24](https://cdn.jsdelivr.net/gh/Cccc-owo/blogPic@master/EU4%E7%9C%81%E4%BB%BD%E7%BB%86%E5%8C%96%E6%95%99%E7%A8%8B/24.png)

1822 苏州 省份 被归属到中度季风区

补上5000

这里跟大家简单介绍一下climate文件

该文件控制着省份的以下属性

气候带（温带，热带等）气候带不填则系统自动生成

冬天类型（温暖的冬天，严酷的冬天等）冬天类型不填则该省份永远不会有冬天

季风类型（中度季风，严酷季风等）同冬天类型不填则永远没有

以及不可通行省份 就是游戏中的荒地

这样 细化的最基础工作就完成了

如果你细化想要增加新的area、region、superregion、continent

这些都是可行的 无非是在这些文件中 添加上你所添加的area region等

至此细化工作结束

现在我们讲讲细化的收尾工作

![25](https://cdn.jsdelivr.net/gh/Cccc-owo/blogPic@master/EU4%E7%9C%81%E4%BB%BD%E7%BB%86%E5%8C%96%E6%95%99%E7%A8%8B/25.png)

在省份历史文件夹里头，我们新建一个txt文件

命名开头必须是省份ID，后面空一空格后，随你写什么，只要你自己以后改省份的时候 记得是这个ID

填写省份历史是细化中我认为最为枯燥的一个工作

这里我们直接沿用1822 苏州的省份文件

![26](https://cdn.jsdelivr.net/gh/Cccc-owo/blogPic@master/EU4%E7%9C%81%E4%BB%BD%E7%BB%86%E5%8C%96%E6%95%99%E7%A8%8B/26.png)

具体代码是什么意思 此处我不作介绍 自行翻阅维基百科

不过稍微看一下也应该明白了 简单的英语

我们将内容复制到5000上

其中 capital 就是 ![27](https://cdn.jsdelivr.net/gh/Cccc-owo/blogPic@master/EU4%E7%9C%81%E4%BB%BD%E7%BB%86%E5%8C%96%E6%95%99%E7%A8%8B/27.jpg)

最底下那个

此处我加载了汉化补充包

所以是汉字

我们在5000的文件中，改成松江或者上海 随你

![28](https://cdn.jsdelivr.net/gh/Cccc-owo/blogPic@master/EU4%E7%9C%81%E4%BB%BD%E7%BB%86%E5%8C%96%E6%95%99%E7%A8%8B/28.png)

这俩文件 分别是贸易公司和贸易区归属

像之前那样添加area一样 把5000填进去

现在除了positions文件 以及本地化文件外 都已经弄好了

接下来讲怎么处理positions文件

steam用户可以直接在EU4的启动项中输入【-nudge】，在进入游戏主界面的时候 在多人游戏选项的右侧 进入nudge模式

学习用户则右键EU4.exe 在文件末尾里添加【 -nudge】（注意前面有个空格，steam则没有）实在不会就去查怎么加启动项

nudge调整好的positions文件放在C盘文档的EU4/map 里 覆盖你的MOD的同名文件就可以了

![29](https://cdn.jsdelivr.net/gh/Cccc-owo/blogPic@master/EU4%E7%9C%81%E4%BB%BD%E7%BB%86%E5%8C%96%E6%95%99%E7%A8%8B/29.png)

新建一个localisation文件夹

然后建议大家在localisation里新建一个replace文件夹

现在我们需要一个yml文件

可以直接从EU4的localisation文件夹汇总复制一个过来

![30](https://cdn.jsdelivr.net/gh/Cccc-owo/blogPic@master/EU4%E7%9C%81%E4%BB%BD%E7%BB%86%E5%8C%96%E6%95%99%E7%A8%8B/30.png)

EU4的是这俩文件

![31](https://cdn.jsdelivr.net/gh/Cccc-owo/blogPic@master/EU4%E7%9C%81%E4%BB%BD%E7%BB%86%E5%8C%96%E6%95%99%E7%A8%8B/31.png)

随便你取什么名字

只要你自己能知道该文件是用来干嘛的

![32](https://cdn.jsdelivr.net/gh/Cccc-owo/blogPic@master/EU4%E7%9C%81%E4%BB%BD%E7%BB%86%E5%8C%96%E6%95%99%E7%A8%8B/32.png)

省份的名词 本地化格式是这样的

![33](https://cdn.jsdelivr.net/gh/Cccc-owo/blogPic@master/EU4%E7%9C%81%E4%BB%BD%E7%BB%86%E5%8C%96%E6%95%99%E7%A8%8B/33.png)

我们完全不需要这么多，一个就够了

省份的ID命名也是如此

![34](https://cdn.jsdelivr.net/gh/Cccc-owo/blogPic@master/EU4%E7%9C%81%E4%BB%BD%E7%BB%86%E5%8C%96%E6%95%99%E7%A8%8B/34.png)

保存后注意查看编码是不是UTF-8-BOM

yml文件都是以该编码保存

现在我们进游戏后 地图上就是显示的 “Songjiang”了

现在讲讲怎么汉化

我们需要去[云汉化平台](https://paratranz.cn/utilities/converter)进行文件转码

![35](https://cdn.jsdelivr.net/gh/Cccc-owo/blogPic@master/EU4%E7%9C%81%E4%BB%BD%E7%BB%86%E5%8C%96%E6%95%99%E7%A8%8B/35.jpg)

直接输入中文汉字 注意格式

英文冒号数字0空格英文引号汉字英文引号

就是XXXX:0 "汉字"这种格式

![36](https://cdn.jsdelivr.net/gh/Cccc-owo/blogPic@master/EU4%E7%9C%81%E4%BB%BD%E7%BB%86%E5%8C%96%E6%95%99%E7%A8%8B/36.png)

这里直接转码

![37](https://cdn.jsdelivr.net/gh/Cccc-owo/blogPic@master/EU4%E7%9C%81%E4%BB%BD%E7%BB%86%E5%8C%96%E6%95%99%E7%A8%8B/37.png)

将乱码复制回去

另一个文件也同样

如果我们需要大量转码

可以使用云汉化平台的工具

![38](https://cdn.jsdelivr.net/gh/Cccc-owo/blogPic@master/EU4%E7%9C%81%E4%BB%BD%E7%BB%86%E5%8C%96%E6%95%99%E7%A8%8B/38.png)

这东西我相信大家都是看一眼就能学会的

至此所有工作全部结束

现在我们进游戏看看效果

![39](https://cdn.jsdelivr.net/gh/Cccc-owo/blogPic@master/EU4%E7%9C%81%E4%BB%BD%E7%BB%86%E5%8C%96%E6%95%99%E7%A8%8B/39.jpg)

我们可看到 松江已经汉化了

另外nudge模式可以修改贸易路线

![40](https://cdn.jsdelivr.net/gh/Cccc-owo/blogPic@master/EU4%E7%9C%81%E4%BB%BD%E7%BB%86%E5%8C%96%E6%95%99%E7%A8%8B/40.jpg)

点击保存后

C盘EU4文件夹会生成common文件夹和map文件夹

![41](https://cdn.jsdelivr.net/gh/Cccc-owo/blogPic@master/EU4%E7%9C%81%E4%BB%BD%E7%BB%86%E5%8C%96%E6%95%99%E7%A8%8B/41.png)

将这俩文件剪切到MOD的相对应文件中

重开游戏

![42](https://cdn.jsdelivr.net/gh/Cccc-owo/blogPic@master/EU4%E7%9C%81%E4%BB%BD%E7%BB%86%E5%8C%96%E6%95%99%E7%A8%8B/42.jpg)

可以看到 已经完全没有问题了

如此简单 大家学会了吗？
