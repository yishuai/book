---
layout: post
title: Linux
---

我们首先熟悉 Marscode 网络编程环境采用的 Linux 操作系统。

## Terminal

我们打开 VS Code 等编程工具之后，在中间的下面，有一个叫 Terminal 的部分。在这里，我们就可以输入命令。

我们打开 Marscode 项目后，也能看到这个 Terminal。这个 Terminal 就是我们以后登录到远程主机上工作时的工作界面。

大家平时学习生活中用命令行工具比较少。用得比较多的是 Windows 或者 MacOS 的图形化用户界面。在这种界面中，用鼠标用得很顺手。

但当我们远程登录服务器后，是没有图形化界面的，只能通过这种 Terminal 远程登录到服务器上工作，所以就只有这种命令行的方式可以工作。所以必须要学会。

## 多用户

我们点右上角的这个加号，就可以再新启动一个 Terminal。然后在右边可以切换这些 Terminal。它们可以同时工作。

一台 Linux 服务器，会有很多用户开很多 Terminal，同时在上面工作。这是 Linux 操作系统跟 Windows 不一样的地方。Windows 一般是给个人用户用的，而 Linux 一般是服务器，可以给很多人用户同时用。那么怎么用呢？不是接很多显示器和键盘，而是大家都可以远程登录，各自用不同 Terminal 来工作。比如说这台电脑，我登录上去了，你也登录上去了。我们各自用不同的 Terminal，都可以工作，互不干扰。

不同的用户登录后，有不同的用户名。我们在 Terminal 里可以用 echo $USER 来看一下我们的用户名。开头的 $ 符号代表后面这个 USER 是一个环境变量，而 echo 能够把这个环境变量打印出来看一眼。我们把它打印出来后，就会发现我们的用户名是 cloudide。

## 环境变量

一个 Terminal 有很多环境变量。比如 USER 就是一个环境变量。另一个重要的环境变量是 PATH。我们可以用 echo $PATH 来看一下我们的程序搜索路径。比如我们敲了一个命令 java，Linux 就会到 PATH 下面的这些目录里面依次去找 java 的可执行程序。如果找到了，它就执行这个程序，如果没有找到的话，它就会报告说没有找到。

如果我们想知道 java 这个程序到底在哪个目录下，我们可以输入 which java。它会告诉我们 java 在哪个目录下。

环境变量很重要，需要根据我们系统的情况进行配置。很多程序执行的时候需要看看这个变量，然后去访问系统里的一些东西。比如 PATH，就是供系统去寻找可执行文件的。类似的，一些程序可能需要 JAVA_HOME 这个环境变量去找 Java 的游戏东西。所以，我们需要根据我们系统的实际情况，对它们进行配置。

一个最常见的配置 Terminal 环境变量的地方，是我们 Home 目录下的 Terminal 启动文件。我们一般就在这个文件里配置这些环境变量。

首先，让我们进自己的 Home 目录。每个用户都有自己的 Home 目录。因为我的用户名是 cloudide 对吧，所以我的 Home 目录就在 /user/cloudide。我们 cd ~ 就能进入这个目录。

我们 ls -l 看一下这个目录下的文件，就会发现这个目录下的东西的 Owner 和 Group 就是 cloudide。所以这些目录文件都是我的。我想删就删。但是其它用户不能来删我的。

那么，我新建一个 Termianl 终端，这个 Terminal 都会自动执行我的 Home目录下的一些隐藏文件，帮我初始化这我这个环境。我们 ls -a 就能看到这些隐藏文件。

因为我的 Terminal 是一个 z-shell，所以，它就会执行这个 .zshrc 文件里面的语句。这些语句是一些命令。我们可以在这里面加一些命令，让它自动执行。

所以我们就可以在 .zshrc 里把这些 JAVA_HOME 什么的环境变量都给设上。这样的话，我们每次启动一个 Terminal，它都会自动帮我们执行这个 .zshrc，帮我们设置这些环境变量。

所以我们必须得改这个文件。因为我们在 Terminal 里，所以只能用 vi 来改它。

## root 权限

斜杠 / 代表根目录。用 ls -l / 就能列出根目录下的所有目录和文件。这时我们会发现它们的 Owner 和 Group 都是 root。

这个 root 就是整个系统的管理员，或者叫 super user（超级用户）。它特别厉害。它想把这个电脑格式化，都是可以的。所以它的权限很高，因此也特别可怕。

我们 ls -l 可以看到这些文件的“读-写-执行”权限。这个 rwx 就是 read - write - execute 的缩写。然后它有三组。分别代表：自己，同组的人，还有其他人。

因为有这个权限设置，所以咱们上去就不能随便看到别人的东西了，更不能够改只有这个管理员才能改的一些东西。比如说 IP 地址这些关键的配置。比如，在这里，因为我们的用户名是 cloudide，不是 root，我们也一般不是 root 组的，所以，这些根目录下的这些目录和文件，我一般都没有 write 和 execute 的权限。因此，我想删都删不了。如果我试图去删它，它会报告说：这是 not permit （不允许的）。因为在 Linux 中，它们的设置是不让非 root 的用户写和执行的。

## sudo

当我们实现需要改一些只有 root 才能改的东西的时候，我们可以用 sudo 获得 root 的权限，执行一个命令。sudo 就是 super user do。这样我们就可以删它们了。所以我们就可能会犯很严重的错误。所以用 sudo 一定要小心。

这是 Linux 的一个优点。这样的话，我们用普通用户登录，是干不成什么坏事的。我们最多把自己的目录删了，不会把系统搞崩溃。这和 Windows 操作系统就不一样。在 Windows 里，我们就习惯了什么都可以删。

所以我们平时工作的时候，不要用 root 身份。这就给我们加了一个保险：作为普通用户，我们再折腾，也没事，不会把 IP 地址改了，或者把重要的系统文件给删了，搞得开不了机，因为我们没有这个权限。

只有当真的要干点厉害的活时，我们才会用 sudo 暂时取得 root 权限，执行一个命令。因为要特别输入 sudo，所以，我们也就留意了：我现在是超级用户，就不能一边跟人聊天，一边敲这几条命令了，必须小心行事。

<br/>

|[Index](../) | [Previous](1-marscode) | [Next](3-cmd)|
