---
title: 你的下一台电脑，何必是电脑——安卓平板免root生产力优化方案
date: 2025-01-24 22:36:51
tags:
  - productivity
  - android
  - rootless
cover: /images/rootless_productivity_optmization_for_android_tablets/cover.jpeg
---

## 前情提要：

在平板上安装ZeroTermux，利用@萌系生物研究员 大佬的TMOE把平板变成生产力工具

需要条件：
1. 一台安卓平板，鸿蒙5.0以及鸿蒙NEXT不行，iPad不行（那样的话你的下一台电脑可能还得是电脑💻），最低配置6+128
2. 一双手
3. 能看懂胎教级教程的眼睛👀和脑子

**禁忌症**：*看不懂中文的*😜

## 注意事项：

1. 尽量不要升级到a15，ColorOS15已知无法良好使用Termux，HyperOS2会出现奇怪bug
2. 本教程的程序开发部分不适用于以下人群：Android开发者，Flutter Android开发者，React Native开发者（这三个都是因为谷歌不提供Linux aarch64的SDK），macOS / iOS开发者，electron开发者（electron在proot下会出现权限&所有权问题），WPF C#开发者，.NET Windows开发者（Linux平台对C#不友好）
3. 本教程适用编程语言：Rust（Attribute自动补全支持不好），Golang（import时没有自动提示），Python（完美），React.js（完美），Vue.js（还好），Svelte（一般），Flutter（只要不是Android就完美），Java（理论可行）
4. 由于不是所有机型都支持GPU加速，故我在这里不放教程了。有骁龙设备的自己去找对应版本的Turnip Zink驱动。。。反正我平板不支持 :loudly_crying_face:

## 开始安装：

### 下载并安装ZeroTermux

打开这个链接🔗：[查看链接](https://www.123865.com/s/PBdSVv-WOi8H)
里面是我存的ZeroTermux beta和ZeroTermux engine 文件（不要在意里面beta打成bate的问题，不是我打的，是官方打的），两个软件都要安装
进去之后会有一个协议，拉到最底下然后关掉（直接关不行哒QwQ）

### 下载基础容器包

在[这个链接](https://www.123865.com/s/PBdSVv-BTK8H)里边找到TMOE_BASE_CONTAINER.tar.gz，下载，保存到内部存储/xinhao/data文件夹里面，如果没有就新建一个
***注意***：ZeroTermux的权限一定要给足！尤其要给内部存储权限！否则后续可能会检测不到恢复包！如果你用的是和我一样的澎湃OS，无论如何也检测不到，那恭喜你，你可以直接按照酷安`@大龙爪子021` 的[这篇帖子](https://www.coolapk.com/feed/52976234?shareKey=YWZiYTUxZDNhYzI5Njc5NDg5N2I~&shareUid=34000961&shareFrom=com.coolapk.market_15.0.2) 安装TMOE并跳过步骤4了，唯一要补充说明的是启用一言的那块我建议选no，这样能少装一个依赖，容器加载速度也能快一点 😜

### 恢复基础容器

从屏幕上三分之一以内的屏幕左边缘往右滑，可以避免触发全面屏手势（大部分系统是这样的），点击备份与恢复![来自 @大龙爪子021 的图片](/images/rootless_productivity_optmization_for_android_tablets/zerotermux_homepage_sidebar.jpeg) 然后点恢复，就能看见那个TMOE_BASE_CONTAINER.tar.gz了，点击，输入新名称，确认，一气呵成 😁 
完事之后从左往右滑，点切换容器，点你刚才设置的那个名字，确认，重新启动ZeroTermux

### 下载并使用容器恢复包

输入tmoe，弹出以下菜单：![TMOE主菜单](/images/rootless_productivity_optmization_for_android_tablets/tmoe_mainpage.jpeg)如果你是从步骤3直接跳过来的，那你应该是这个界面：![刚安装完TMOE](/images/rootless_productivity_optmization_for_android_tablets/after_install_tmoe.jpeg)直接两次返回上级菜单就和别人一样了
选中第七个更新，回车，出现对应提示后再次回车（我打包的时候mo2把tar的-J选项删了，出现了恢复bug，新版已修复，具体参考我这个issue：[查看链接](https://gitee.com/mo2/linux/issues/IAUH7C)）
选中第一个，回车
再选中Restore恢复容器，回车
这个时候先把ZeroTermux挂后台
随便下载[这个链接](https://www.123865.com/s/PBdSVv-BTK8H)中任意一个文件夹 📁 （除了Touchscreen system之外）中的任意一个文件下载，放到Download/backup/containers/proot文件夹里，没有的自己创建
编程党建议选server里的ubuntu web dev，自带neovim
这时候再回到ZT，此时应该长这样：![容器恢复菜单](/images/rootless_productivity_optmization_for_android_tablets/restore_menu.png)直接回车，选自动选择最新，回车，出现提示后再次回车
然后会回到和上图一模一样的界面中，返回主菜单
选第一个，回车，再选已安装容器列表，回车，然后就能看见你刚才恢复的那个容器了，再回车
会出现以下界面：![容器详情菜单](/images/rootless_productivity_optmization_for_android_tablets/container_details.jpeg)默认选第一个，回车（好多回车啊 😯 QwQ）
然后就启动了![容器已进入](/images/rootless_productivity_optmization_for_android_tablets/in_the_container.jpeg)web党这个时候已经可以撤了，里面事先安装好了Lunarvim，输`lvim`启动 😎![LunarVim](/images/rootless_productivity_optmization_for_android_tablets/lunarvim.jpeg)![LunarVim React.js 开发](/images/rootless_productivity_optmization_for_android_tablets/lvim_reactjs.jpeg)

### LazyVim 安装

用其他语言的兄弟们跟着我接着往下走
先从[这个链接](https://www.123865.com/s/PBdSVv-nRi8H)下载我编译的Neovim最新版（旧版会报错），并在容器内输入以下命令：
```bash
cp ~/sd/neovim-0.11.0_arm64.deb .
apt install ./neovim-0.11.0_arm64.deb
# 我在制作恢复包的时候脑子抽了一下，直接用的make install，导致可执行文件一直在/usr/local/bin/里面呆着，覆盖了默认的软件包可执行文件
rm /usr/local/bin/nvim
```
（⚠️ 注意：第二条命令尽量使用`apt install`而非`dpkg -i`，因为`apt`会自动检测并安装依赖，而`dpkg`不会，CSDN害人不浅）
输入以下命令，克隆 LazyVim 官方配置到本地：
```bash
git clone https://github.com/LazyVim/starter ~/.config/nvim
rm -rf ~/.config/nvim/.git
```
然后输入`nvim`启动，初次加载需要从GitHub上下载文件📃，如果网络不好或者不会魔法的话需要多失败几次
总之，此时你拥有了宇宙最强IDE（VS Code：你在说啥？😅）——LazyVim，enjoy！
