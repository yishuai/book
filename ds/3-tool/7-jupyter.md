---
layout: post
title: Jupyter Notebook
---

Jupyter Notebook 是我们常用的一个学习 Python 的工具。

# 安装

要启动 Jupyter Notebook，你需要先确保已经安装了 Jupyter。

可以使用 `pip` 进行安装：

```bash
pip install jupyter
```

# 配置

有时候我们想要配置 Jupyter Notebook 启动后不要求 token 验证等。这时我们需要修改它的配置文件。以下是具体步骤：

首先生成配置文件。如果还没有生成 Jupyter Notebook 的配置文件，使用以下命令生成：

```bash
jupyter notebook --generate-config
```

这会在我们的用户主目录下生成一个配置文件，通常位于 `~/.jupyter/jupyter_notebook_config.py`。

然后编辑配置文件。比如用 vi 打开 ~/.jupyter/jupyter_notebook_config.py，通过斜杠进行搜索，然后进入编辑模式，进行修改：

禁用 token 验证（仅在安全环境下推荐），可以设置：

```python
c.ServerApp.token = ''
c.ServerApp.password = ''
```

注意，虽然禁用 token 和密码可以方便地启动 Jupyter Notebook，但它会降低安全性。如果在公共网络或多人共享的系统上使用 Jupyter Notebook，建议不要禁用 token 和密码验证，以确保你的环境安全。

启用自动登录，确保不需要任何形式的认证：

```python
c.ServerkApp.disable_check_xsrf = True
```

允许远程接入：

```python
c.ServerApp.allow_remote_access = True
```

设置监听所有 IP 地址，接受来自任何 IP 地址的连接

```python
c.ServerApp.ip = '0.0.0.0'
```

注意：确保你的防火墙允许外部访问所配置的端口（例如 8888）。

设置 Jupyter Notebook 服务器使用的端口：

```python
c.ServerApp.port = 8888
```

启动后不自动打开浏览器

```python
c.ServerApp.open_browser = False
```

# 启动

默认情况下，Jupyter Notebook 会在启动命令执行时的当前目录下运行。所以，一般我们在启动它之前，先 cd 进入我们的工作目录。比如：

cd /cloudide/workspace/All-in-One/

然后启动

```bash
jupyter notebook
```

如果你希望在特定目录下运行，可以使用 `--notebook-dir` 参数：

```bash
jupyter notebook --notebook-dir=/path/to/your/directory
```

你也可以通过命令行选项临时允许远程访问。例如：

```bash
jupyter notebook --ip='0.0.0.0' --port=8888 --allow-root --no-browser --ServerkApp.token=''
```

这种方法适用于一次性启动而不修改全局配置文件。这样，Jupyter Notebook 应该可以在启动时不需要 token 进行验证。

# 访问

访问 Marscode 的 Networking Tab，找到 8888 端口的 URL，打开链接。

# 主界面

打开链接，进入主界面后，显示的是目录下的文件列表。在文件列表旁边，还有一个 Tab 叫 Running，里面显示所有我们正在跑着的 Notebook。在这里，我们可以把它们 Shut down （关掉）。

# Notebook 界面

我们下面打开我们的 Jupyter Notebook。打开它之后，我们看到一个特别好看的界面。它是一个笔记本。

首先，它右上角这个圆圈，如果是空心的，就代表着它现在是 idle 的，就是说它没有在运行。如果它在跑，比如说我们执行了一个 for 循环，这个圆圈就会变成黑的。

我们下面简单学习它的使用。它里面包括两种格子（Cell）。

第一种格子是 Markdown 格子。它能用 Markdown 语法写文字。比如说第一个格子，咱们双击它一下，就可以编辑了。

Markdown 让我们可以很简单地格式化文档。比如 ChatGPT 就是用它来给我们回复的。比如：如果我们在文字前面加两个 # 号，它就会给我们显示为二级标题。这比我们在 Word 里选“二级标题”的格式，是不是方便多了？写完之后，你点右边这个勾，它就会开始渲染，显示我们想要看到的样子。

在 Markdown 格子里，我们还可以写 Latex 公式。比如 $$\mu$$。这样显示出来就会特别漂亮。

第二种格子是代码格子。这种格子的左上角有一个三角，这就是“执行”按钮。点它之后，这个格子里的 Python 代码就会执行。

我们第一次点击的时候，它会让我们选择内核。我们要选一个 Python 的。然后它让我们选择一个 Python 环境。大家看到这些东西别慌哈！就慢慢地观察。然后你看到这一行的后面有一个“Recommended”，就是“推荐”的意思。那就点这个推荐的吧。这个代码就会开始执行了。

代码执行的时候，可能会出错。这时候大家也不要着急，就慢慢地看错误的提示。如果它会报这个模块没有安装，那我们就安装这个模块就好了。

有两种办法安装模块。第一种是你到 Terminal 里用命令行敲 pip install xx. 它就会自动到网上帮我们下载后安装。第二种方法是在 Jupyter Notebook 的代码格子里运行这个命令。但代码格子本来是运行 Python 代码的，所以我们得在前面加个感叹号，这样就告诉它，这是一个命令行的代码了。然后我们执行这个格子，它就会去装了。

## 参考

-《Dive in Deep Learning》课本的章节 [23.1. Using Jupyter Notebooks](https://d2l.ai/chapter_appendix-tools-for-deep-learning/jupyter.html) 

<br/>

|[Index](../) | [Previous](5-file) | [Next](9-python)|
