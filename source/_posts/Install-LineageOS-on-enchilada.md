---
title: 在一加六上安装 Lineage OS
tags:
  - 刷机
categories:
  - 技术
comments: true
sitemap: true
abbrlink: 732f9bb
date: 2022-07-20 19:19:13
updated: 2022-07-20 19:19:13
---

译者：Cccc_

译自[Install LineageOS on enchilada](https://wiki.lineageos.org/devices/enchilada/install)

与原文不同之处，请以原文为准。

<!-- more -->

---

> 警告：这些操作指南只有在你准确地遵循每一个章节和步骤时才有效。
> 在某个过程中发生错误的话请不要继续下一步!

## 基本要求

1. 在实际操作之前，至少要通读一遍说明，以避免因遗漏任何步骤而出现任何问题！
2. 请确保你的电脑有```adb```和```fastboot```。安装指导可以在[这里](https://wiki.lineageos.org/adb_fastboot_guide.html)找到。
3. 打开设备的[USB 调试](https://wiki.lineageos.org/adb_fastboot_guide.html#setting-up-adb)。

> 警告：在遵循这些操作指南时，请确保设备正在使用 **Android 11** 固件（即系统的安卓版本应为11）。
>
> 如果供应商为该版本提供了多个更新，例如 安全更新，请确保你的设备处于最新状态！
>
> 如果你目前的设备比 **安卓 11** 更新或更旧，请在开始之前降级/升级至指定的版本（教程可以在网上找到）。

## 解锁 bootloader（引导加载程序）

> 注意：以下步骤只需要在每个设备上运行一次。

> 警告：解锁 bootloader 将清除设备上的所有数据！在继续之前，请确保你想要保留的数据已经备份在你的电脑和/或你的谷歌账号或类似平台上。请注意，一旦安装了 LineageOS ，系统供应商的备份解决方案（像三星备份、摩托罗拉备份）可能无法在 LineageOS 上使用。

1. 打开设备设置中 开发者选项 --> OEM 解锁（如果存在OEM 解锁）。
2. 用 USB 连接设备至你的电脑。
3. 在电脑上，打开一个命令提示符（Windows）或终端（Linux 或 Mac OS）窗口，输入：

```bash
adb reboot bootloader
```

你也可以以组合键启动进入 fastboot 模式：

- 在设备电源关闭的情况下，按住<kbd>音量上键</kbd> + <kbd>电源键</kbd>

4. 当你的设备处于 fastboot 模式时，检验你的电脑是否检测到了你的设备，输入：

```bash
fastboot devices
```

如果你没有得到任何输出或得到了一个错误：

- Windows：确保设备出现在设备管理器中，没有三角形警告。否则尝试其他驱动程序，直到上面的命令有效！
- Linux 或 Mac OS：如果你看到```no permissions fastboot```，尝试以root权限运行```fastboot```。当输出为空时，检查您的 USB 线和端口！

5. 现在输入一下命令以解锁bootloader

```bash
fastboot oem unlock
```

> 注意：此时，设备可能会显示屏幕提示，需要交互才能继续解锁bootloader。请采取设备要求你继续执行的任何操作。

6. 如果设备没有自动重启，手动将其重启。现在它应该已经被解锁了。

7. 由于设备完全重置，你将需要重新启用 USB 调试 功能才能继续。

## 用```fastboot```临时启动至一个自定义recovery（恢复）模式

1. 下载[Lineage Recovery](https://download.lineageos.org/enchilada)。仅下载最新的 recovery 文件，一般情况下，文件名类似于```lineage-19.1-20220714-recovery-enchilada.img```。
2. 用 USB 连接设备至你的电脑。
3. 在电脑上，打开一个命令提示符（Windows）或终端（Linux 或 Mac OS）窗口，输入：

```bash
adb reboot bootloader
```

你也可以以组合键启动进入 fastboot 模式：

- 在设备电源关闭的情况下，按住<kbd>音量上键</kbd> + <kbd>电源键</kbd>

4. 当你的设备处于 fastboot 模式时，检验你的电脑是否检测到了你的设备，输入：

```bash
fastboot devices
```

如果你没有得到任何输出或得到了一个错误：

- Windows：确保设备出现在设备管理器中，没有三角形警告。否则尝试其他驱动程序，直到上面的命令有效！
- Linux 或 Mac OS：如果你看到```no permissions fastboot```，尝试以root权限运行```fastboot```。当输出为空时，检查您的 USB 线和端口！

> 提示：有些设备在 bootloader 模式下对 USB 的支持有问题，如果你在使用 ```fastboot getvar ...``` 、 ```fastboot boot ...```、 ```fastboot flash ...``` 等命令时看到 ```fastboot``` 挂起，没有输出，你可能想尝试不同的USB端口（最好是 USB Type-A 2.0 端口）或 USB 集线器。

5. 在设备上临时刷入一个 recovery ，输入（以实际的文件名替代 ```<recovery_filename>```！）：

```bash
fastboot flash boot <recovery_filename>.img
```

> 提示：过时的 fastboot 版本放弃了对 传统 A/B 分区 的支持，所以如果你尝试刷入 ```boot``` ，它可能会尝试刷入到 ```boot__a``` / ```boot__b``` 分区而不是 ```boot_a``` / ```boot_b```分区。在这种情况下，你必须将 ```fastboot``` 更新到比 ```31.0.2``` 更新或相同的版本。另外，你可以根据fastboot失败刷入的分区，手动指定要刷入到哪个分区。例如，如果 fastboot 不能刷入到 ```boot__a```，你必须刷入到 ```boot_a```。

6. 现在重启至 recovery 模式以验证安装。

- 使用菜单导航到并选择 ```Recovery``` 选项。

<details>

<summary>译者注：如果上面两个步骤无效，点开这里使用这个方法</summary>

7. 在 fastboot 模式下，将设备启动到自定义的 recovery，输入（以实际的文件名替代 ```<recovery_filename>```！）：

```bash
fastboot boot <recovery_filename>.img
```

本文以下提到 sideload（旁加载）或 recovery 模式的地方都需要在执行完上面的命令的状态下（即在 Lineage Recovery 模式下）。

</details>

## 确保所有的固件分区是一致的

> 注意：以下步骤只需要在每个设备上运行一次。

在某些情况下，非活动 slot（区） 可能未被填充或包含比活动 slot 老得多的固件，这会导致各种问题，包括可能的硬砖（即手机无法使用）。我们可以通过将活动 slot 的内容复制到非活动 slot 中来确保这些情况不会发生。

要做到这一点，请通过以下步骤 sideload （旁加载） ```copy-partitions-20210323_1922.zip``` ：

1. 从[这里](https://www.androidfilehost.com/?fid=2188818919693768129)下载 ```copy-partitions-20210323_1922.zip``` 。这个文件的 MD5 值应为 ```92c010bf0371bfa6e55895c4c4750177``` ， SHA-256 值应为 ```200877dfd0869a0e628955b807705765a91e34dff3bfeca9f828e916346aa85f```。

2. Sideload （旁加载） ```copy-partitions-20210323_1922.zip``` ：
- 在设备的 recovery 模式中，选择 "Apply Update" ，然后点选 "Apply from ADB" 来开始
- 在电脑上，用命令 ```adb sideload copy-partitions-20210323_1922.zip``` sideload（旁加载） 这个文件。

> 注意：复制分区脚本是由 LineageOS 开发者 erfanoabdi 和 filipepferraz 创建的，但没有用LineageOS的官方密钥签名，因此当它被旁加载时， Lineage Recovery 会出现一个屏幕，显示 ```Signature verification failed```（签名验证失败），这是正常现象，请点击```Continue```（继续）。

3. 现在通过点按 "Advanced" 重启至 recovery 模式，然后点按 "Reboot to recovery"。

## 从 recovery 安装 LineageOS

1. 下载你要安装的 [LineageOS 安装包](https://download.lineageos.org/enchilada) 。~~或者自己[构建](https://wiki.lineageos.org/devices/enchilada/build)安装包（一般不用考虑）~~。

- （可选）：如果你想安装一个应用包附加组件，类似 [Google Apps](https://wiki.lineageos.org/gapps.html) （使用 ```arm64``` 结构），请阅读并遵循[Google Apps page](https://wiki.lineageos.org/gapps.html)的指南。

2. 如果你的设备不在 recovery 模式中，重启进入 recovery 模式：

- 在设备电源关闭的情况下，按住<kbd>音量上键</kbd> + <kbd>电源键</kbd> *（译者：如果不能临时刷入 recovery 以我提供的方法进入 recovery 模式）*

3. 现在点按 **Factory Reset** ，然后 **Format data / factory reset** ，并继续格式化过程。这将移除加密并删除内置存储中的所有文件，同时也会格式化你的 cache 分区（如果有的话）。

4. 回到主菜单。
5. Sideload（旁加载) LineageOS ```.zip``` 包：

- 在设备上，点选 "Apply Update"，然后点选 "Apply from ADB" 以开始 sideload 。
- 在电脑上，输入 ```adb sideload filename.zip```（以下载到的 LineageOS 安装包的文件名代替 filename ，注意要在该文件的同一目录下执行）。

> 提示：正常情况下， adb 会报告 ```Total xfer: 1.00x``` ，但在某些情况下，即使过程成功，输出也会在47%处停止，并报告 ```adb: failed to read command: Success``` 。在某些情况下，它会报告 ```adb: failed to read command: No error``` 或 ```adb: failed to read command: Undefined error: 0``` ，这也没问题。

6. （可选）：完成以上步骤后，如果你想安装任何附加组件，点击 ```Advanced``` ，然后点击 ```Reboot to Recovery``` ，当你的设备重启时，依次点击 ```Apply Update``` > ```Apply from ADB``` ，再于电脑上输入命令 ```adb sideload filename.zip ``` ，其中 ```filename```应为你要刷入的包的文件名。

> 注意：附加组件没有用LineageOS的官方密钥签名，因此当它们被旁加载时，Lineage Recovery会出现一个屏幕，显示 ```Signature verification failed```（签名验证失败），这是正常的，请点击 ```Continue```（继续）。

> 注意：如果你想在你的设备上使用 Google Apps ，你必须 **在第一次启动到LineageOS之前** 按照这个步骤进行操作，刷入 GAPPS ！

7. 当你成功安装了一切，点击屏幕左上方的后退箭头，然后点击 "Reboot system now"（立即重启系统）。

> 注意：第一次启动通常不超过15分钟，这取决于设备的情况。如果需要更长的时间，你可能错过了一个步骤，否则请随时[寻求帮助](https://blog.iscccc.eu.org/posts/732f9bb/#%E5%AF%BB%E6%B1%82%E5%B8%AE%E5%8A%A9)。

## 寻求帮助

在你仔细检查了你是否准确地遵循了这些步骤，没有跳过任何步骤，仍然有问题或卡住了，请随时在[我们的subreddit](https://reddit.com/r/LineageOS)或[Libera.Chat的#LineageOS](https://kiwiirc.com/nextclient/irc.libera.chat#lineageos)中提问。
