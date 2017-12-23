# 借助 Homebrew Cask，教你快速下载安装 Mac App 新姿势

### 在 Mac 上安装软件程序，你会怎么做？通常的做法应该是以下两种：

- 在 Mac App Store 搜索，然后安装；
- 对于不在 Mac App Store 上架的软件，先在搜索引擎中搜索，找到官网，然后打开下载页面下载，最后再将下载的安装包拖到「软件程序」文件夹或执行安装。

听起来是不是有些麻烦？今天我分享一种高效快速安装 Mac 软件的方法：使用 Homebrew Cask 扩展。这种方法只需在终端输入一行命令，就可以解决包括查找、下载和安装软件的一系列步骤。

也许在你看到「终端」「命令」等字眼的时候会有些犹豫，更是对 Homebrew Cask 一无所知，没关系，因为它其实并没有很复杂，只需一点学习成本，就能让你解锁一种高效而炫酷的安装 Mac App 新姿势。

## 什么是 Homebrew 与 Homebrew Cask

Homebrew 是基于 OS X 的套件管理工具，是一个开源的 Ruby 脚本，专门用于快速下载软件。更通俗地讲，Homebrew 类似于一个软件中心，你可以理解成 App Store 或者 Google Play 那样的软件商店，只不过，Homebrew 比前者以及 Mac App Store 来说有着更丰富的资源与更高效的管理，具体会在下文提及。

至于 Homebrew Cask，它是一套建立在 Homebrew 基础之上的 OS X 软件安装命令行工具，是 Homebrew 的扩展。不拿那么多拗口的术语来烦你了，简言之，你完全可以把 Homebrew Cask 当作是 Homebrew 的一部分，你只需要记住，在安装常用软件的过程中，大部分情况下我们只需要使用 Homebrew Cask 就足够了。

## 有什么优势

- 通过 Homebrew 下载安装的软件全部来自对应的软件官网，无需担心下载源的安全问题。
- 依存于系统既有的库，减少了空间占用和冗余
- 使用 Git 进行管理和更新
- 易于定制
- 安装软件 / 软件包 / 软件都在一个目录下，方便管理，这也是 Homebrew 能如此受欢迎的最大原因之一。

Homebrew Cask 的常用命令非常简单，也很好理解，虽然是通过命令行，但你完全不需要对「终端」「命令行」有过多了解，也能很快上手。

不管是 Homebrew 还是 Homebrew Cask，它们除了安装软件外还能帮你做一些其他操作，因此，你花费一定的学习成本带来的效率提升，是值得的。

## 为什么要用「命令行」装软件

看到这里，想必很多人都有这样的疑问：为什么要用 Homebrew 或者 Homebrew Cask 这种方式安装软件？正常安装也没有多麻烦呀？我相信，你不用它的理由可以有很多，但不妨先看看我推荐用它的几点理由：

### 1. 操作真的很方便

就像文章开头所提，使用 Homebrew 安装 App 的一大好处就是快速且方便，全部过程只需要一行命令搞定，如果你想安装多个软件，这种方法的优势更加明显——它还是只需要一行命令：

brew cask install <软件名1> <软件名2> <软件名3>

### 2. 相比从 Mac App Store 下载的优势

对于在 Mac App Store 中上架的软件而言，更新速度就是一个很大的问题。由于需要经过苹果审核，一款 App 的官网版（非商店版本）往往比商店版更新更频繁或功能更全。现在，已有越来越多的 Mac App 开发商选择官网版，甚至愿意从 Mac App Store 下架，此前的 Sketch 下架事件就闹得沸沸扬扬。关于一款 App 上架 MAS 的优劣对比，你可以阅读少数派 这篇文章 了解。

而使用 Homebrew 安装的 App 也是从它的软件官网下载，Homebrew 只是做了整合，这使得它对于常用 App 的支持更全面，更新也更迅速。

### 3. 相比从官网下载的优势

通过 Homebrew 或者 Homebrew Cask 安装的软件都会集中在一个目录下面，再由 Homebrew 将相关软件软链接到相关路径。举个例子，如果当我们访问系统中的 A 文件时，系统都会将访问路径导向 B 文件对应的路径，那么 A 文件就是 B 文件的软链接，这也是 Homebrew 的原理。

相比我们自行去官网下载的 App 安装包，有时在「桌面」有时在「下载」文件夹的情况，使用 Homebrew 我们无需担心文件的位置，所有安装包都会放在一处，这对之后的管理提供了很大便利。

说完理由，下面让我们一起看看如何使用 Homebrew Cask。

## 准备工作

在开始前，你可能需要先做好以下准备工作：

### 1. 配备 Intel CPU 的 Mac 电脑

确保你的 Mac 系统版本在 OS X 10.9 或以上。

### 2. 安装 Xcode

如果你的电脑上没有安装 Xcode，你可能需要先在 Mac App Store 下载 Xcode，如果嫌 Xcode 体积庞大的话，可以前往 Apple 开发者网站 尝试下载 Command Line Tools for Xcode 进行安装。

### 3. 安装 Homebrew

相信有些朋友已经在 Aria2 的文章中安装过 Homebrew 套件管理器了，上一步的 Xcode 安装也是为这一步做准备。如果你还没有安装过 Homebrew，方法也很简单，打开终端运行下列代码就可以了：

`/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`

## 下载软件

完成上述操作步骤，就下来就可以开始为你的 Mac 安装软件了。

使用 Homebrew 安装 App 非常简单，这里需要用到的是基于 Homebrew 的扩展 Homebrew Cask，具体方法是在「终端」中输入类似下列形式的代码并运行：

`brew cask install 软件名`

这里的「软件名」就是我们所要安装软件的名称，下面列举几个常用软件的安装命令大家就会明白了：

- brew cask install google-chrome 安装 Chrome 浏览器
- brew cask install alfred 安装 Alfred
- brew cask install fliqlo 安装屏保程序 Fliqlo
- brew cask install dropbox 安装 Dropbox
- brew cask install java 安装 Java 等开发环境也是可以的

以上几个命令只是简单举例，截止目前，Homebrew Cask 已经收录了近 2100 个软件，足够满足大多数人的需求，你也可以到 [Homebrew Cask]() 官网搜索看看有没有你想要的软件程序。

## Homebrew 还能做什么

Homebrew 当然不只是能做「安装软件」这一件事，我整理了一些 Homebrew 的常用命令，可以满足各种需求：

- brew cask uninstall 软件名 卸载通过 Homebrew Cask 安装的软件
- brew cask search 列出所有可以被安装的软件，当然你也可以直接前往上文提供的 Homebrew Cask 搜索。
- brew cask search google 这里是查找所有与 google 有关的软件，google 关键词可以自行替换
- brew cask info 软件名 查找相关软件的信息
- brew cask cleanup 删除 Homebrew Cask 下载的包
- brew cask list 列出通过 Homebrew Cask 安装的包
- brew cask update 更新 Homebrew Cask

要注意的是，Homebrew Cask 并没有提供相关的软件更新命令，这里我们可以直接使用软件内的更新功能就可以了。

之前少数派写过增强 Mac「预览」功能（QuickLook）的教程，里面有提到很多小插件，其实你也可以直接用 Homebrew 快速下载这些插件，比如：

- brew cask install qlmarkdown 安装 Markdown 预览（QuickLook）插件
- brew cask install qlcolorcode 代码块高亮
- brew cask install qlvideo 视频预览插件

当然关于 Homebrew 以及 Homebrew Cask 的用法还有很多，这里就不一一介绍。

## 小结

写到这里，还是不免唠叨地要说，「终端」和「命令行」并不是只有极客或开发人员才能玩的东西，我们大可不必先入为主的产生抗拒心理。

Homebrew 这种方式不仅能让你更快更好的解决软件安装的问题，节省更多时间，也会为你开启一个新世界的大门，慢慢地你会发现用「命令行」你还能做很多事情。



