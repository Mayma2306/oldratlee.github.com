---
layout: post
title: 【译】GUI & CLI Principles
location: Hangzhou
permalink: /post/2012-11-04/gui-cli-principles
write-time: 2012-11-04 17:03
tags:
- XX
- YY
---

文章[Subversion UI Shootout](http://onlamp.com/pub/a/onlamp/2005/03/10/svn_uis.html "Subversion UI Shootout")比较了多个GUI SVN工具以及命令行的优劣。

虽然说的是SVN工具，但文中列出的GUI和CLI的原则，值得单独拿出来看看。这里翻译一下。

PS： 交互思考有相通的之处，下面的几篇说了不错的话题，也可以看看：   

* [大众点评移动客户端的“轻”点评模式](http://ifredric.me/post/2012-10-31/dianping_test_2 "大众点评移动客户端的“轻”点评模式")
* [Chrome 浏览器的哪些设计符合「Don't make me think」原则 — 知乎](http://www.zhihu.com/question/20564451 "Chrome 浏览器的哪些设计符合「Don't make me think」原则")  
你可能不知道常用的Chrome有哪些贴心的地方哦~
* [PC 用户的哪些行为让你当时就震惊了？ — 知乎](http://www.zhihu.com/question/20100408 "PC 用户的哪些行为让你当时就震惊了？")  
这篇里会有很多让你震惊却又会心一笑的回答。


# GUI Principles

## GUI Principle #1

>GUIs are superior when graphical representations add clarification. A good example of this is a standard GUI diff utility. While it is possible to figure out what has changed with a unified diff output, it is very helpful to have a split-framed diff utility (such as vimdiff or Tortoise's built-in diff) and see the old file and new file side by side with changes color coded.

在展示和说明一件事时，GUI更优。

一个好例子是，标准的GUI Diff工具。尽管可以算出差异后用统一格式输出**[1]**，但分屏对比显示（比如像VimDiff、Tortoise自带的Diff）会方便很多，新老文件左右两边对比显示，使用不同的颜色来标识出修改部分。

**[1]** 译注：diff命令的输出格式参见：[读懂diff](http://www.ruanyifeng.com/blog/2012/08/how_to_read_diff.html "读懂diff")

## GUI Principle #2

>GUIs are superior when they make performing a specific task more obvious. An example of this among the SVNs is diffing between revisions of a file. In Tortoise, it is just a matter of looking at the log, selecting two log entries, and selecting "Compare Revisions." In the CLI, I had to do a `svn help diff` first before figuring out that the syntax I needed was `svn diff -r <old version>:<new version>`.

要让操作显示更直白性时，GUI更优。

在使用SVN时的一个例子是，查看一个文件不同版本的差异。在Tortoise中，只要在Log窗口，选择两个Log条目，选“比较版本”即可。用CLI，我要先执行`svn help diff`查出diff命令的语法是`svn diff -r <old version>:<new version>`。

## GUI Principle #3

>GUIs are superior for executing an action against a subset of a list of items that requires a human brain for its creation. If you have a command, such as `svn status`, that will generate a list of items and need to commit some, but not all, of the files in the resultant list with a criteria that you cannot easily programmatically derived (such as "Oh, I was only fooling around with this file; it doesn't need to be committed," or "The changes in this file are for next build, not this build, so I'd better not commit them yet"), it is easier to have a list of items to select or deselect with a mouse click rather than, in this case, performing a commit one file at a time.

要人脑子先想好的一系列操作步骤，再从中挑出一部分来执行时，GUI更优。

如果你用一个命令（比如 `svn status`）生成需要提交文件的列表，但是只要提交其中一部分，而不是所有的文件。是否提交的条件不方便用编程地算出（比如，“哦，我搞错了这个文件，它不用提交的”，或是“这个文件的修改下一次build才用，所以先不提交”）。在一个列表里用鼠标选选比起用命令一次提交一个文件的情况，操作会更方便。

## GUI Principle #4

>GUIs are superior when you want to perform a limited number of functions on a list of items. An example is: "What do you want to do with a list of files in a potential commit operation?" The only things that I can think of are to diff the files with the latest repository version to see what changes have been made locally, and revert specific files back to the repository revision. Tortoise includes these options, as well as the ability to open the files. Doing a diff on a specific file is available (as mentioned in this article several times, because that is an awesome feature!) with a double-click on the file.

在一个条目列表上执行多项操作时，GUI更优。

一个例子是，“对于可能要提交的文件，你会要做什么操作？”，我只能想到要看看这些文件和仓库里最新版本的Diff，确认一下本地我修改了哪些内容，回滚一些文件到仓库里的版本。Tortoise有这样的选项，还可以打开文件。在提交窗口要查看Diff，双击文件即可查看文件的Diff。（这个在前面已提到了好几次，真是一个很赞的功能！）

## GUI Principle #5

>GUIs are superior when fields and forms provide visual "clues" regarding input. The GUIs both provide fields to enter the repository location, the directory to put it in once it is checked out, and which revision to check out. This is a simple example and anyone who has checked out a project more than a couple of times with the CLI will have no problem remembering which parameters to put where. The principle, though, still stands. Sometimes having a form to fill out makes it easier to enter input.

窗口里的表单和文本框能提供用户输入的可视化“提示”，GUI更优。

在checkout操作时，GUI窗口会同时提供了输入仓库地址和checkout目录的文本框。这是个简单的例子，尽管命令行上做过几次checkout操作后，都不会搞错参数位置。但作为原则仍然成立。有时候有表单引导会让输入更容易。

# CLI Principles

## CLI Principle #1

>CLIs are superior when processing the result of something with another utility is helpful. For example, to add all .txt files recursively, do something like this:

```bash
for f in `find . -name "*.txt" -print`
do
    svn add "$f"
done
```

处理其它工具输出结果时，CLI更优。

比如，要递归添加目录下的所有TXT文件，可以用下面的命令完成。

```bash
for f in `find . -name "*.txt" -print`
do
    svn add "$f"
done
```

# CLI Principle #2

>CLIs are superior when they support time-saving features of the shell. Tab completion is an amazing time-saving feature of many modern shells. Some SVN commands (such as move) in Rapid can benefit from such features.

当操作被Shell方便省时的功能支持时，CLI更优。

Tab补全是现代Shell都支持的超赞的方便省时功能。有些SVN命令（比如move）利用这些Shell功能可以迅速完成。

![GUI vs. CLI](http://m3.img.libdd.com/farm5/2012/1104/21/F46810A0A7B9BE874F193204F3FE1C2E1BB14E29A271B_400_123.JPEG "GUI vs. CLI")