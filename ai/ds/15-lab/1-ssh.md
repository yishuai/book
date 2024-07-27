---
layout: post
title: SSH
---

# 介绍

我们首先学习 SSH：Secure shell（安全shell）。在大数据系统里，机器之间经常会互相登录，这就需要 SSH。比如 Hadoop 在启动分布式文件系统时需要使用 SSH 连接到本地和远程节点。如果我们不安装和启动 SSH，那么在使用 Hadoop 时，比如在用 start-dfs.sh 启动 Hadoop 时，可能会出现错误 ：

Starting namenodes on [localhost]

localhost: ssh: connect to host localhost port 22: Connection refused

下面我们就学习如何安装和启动 SSH 服务。

# 安装 OpenSSH 服务

在大多数基于 Debian 的系统（如 Ubuntu）上，你可以使用以下命令安装 OpenSSH 服务：

```bash
sudo apt-get update
sudo apt-get install openssh-server
```

# 配置SSH 免密码登录

为了让节点能够自动通过 SSH 连接到本地和远程节点，需要配置免密码登录。以下是步骤：

1. **生成 SSH 密钥对：**

   打开终端，生成 SSH 密钥对：

   ```bash
   ssh-keygen -t rsa -P ""
   ```

   这会生成一对密钥文件（`id_rsa` 和 `id_rsa.pub`）在 `~/.ssh` 目录下。

2. **配置免密码登录：**

   将公钥添加到授权密钥文件中：

   ```bash
   cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
   ```

3. **设置正确的权限：**

   确保 `~/.ssh` 目录和授权密钥文件具有正确的权限：

   ```bash
   chmod 700 ~/.ssh
   chmod 600 ~/.ssh/authorized_keys
   ```

# 启动 SSH 服务：

   ```bash
   sudo service ssh start
   ```

我们还可以配置 SSH 服务在服务器启动时自动运行

```bash
sudo systemctl enable ssh
```

# 测试 SSH 连接

通过以下命令测试 SSH 连接是否成功：

```bash
ssh localhost
```

如果成功登录而不需要输入密码，那么配置正确。

Localhost 就是登录自己。如果登录成功了，那么我们的界面会有一些微小的变化。比如提示词会变了。

要退出 SSH 登录，我们可以用 exit，就又回到原来的 Terminal 里了。

# SSH 配置

如果你仍然遇到问题，请检查 SSH 服务状态，并确保 `sshd_config` 文件中的 `PermitRootLogin` 和 `PasswordAuthentication` 设置正确：

```bash
sudo vi /etc/ssh/sshd_config
```

确保以下设置：

```plaintext
PermitRootLogin yes
PasswordAuthentication yes
```

完成修改后，重新启动 SSH 服务：

```bash
sudo service ssh restart
```

# localhost 定义

确保 `/etc/hosts` 文件中正确配置了 `localhost`：

```plaintext
127.0.0.1   localhost
```

如果你的 Hadoop 集群由多台机器组成，确保每台机器都可以通过主机名互相通信，并且 `/etc/hosts` 文件中包含所有机器的主机名和 IP 地址。

# 防火墙设置

如果你在多台机器上运行 Hadoop，确保防火墙没有阻止 8032 端口。你可以临时禁用防火墙来检查是否是防火墙的问题：

```bash
sudo ufw disable   # 对于基于 Ubuntu 的系统
sudo systemctl stop firewalld  # 对于基于 CentOS 的系统
```

# 确认端口没有被占用

确保 8032 端口没有被其他进程占用。你可以使用以下命令检查：

```bash
sudo netstat -tuln | grep 8032
```

如果端口被占用，可以找到占用端口的进程并停止：

```bash
sudo lsof -i :8032
sudo kill -9 <PID>
```

<br/>

|[Index](../) | [Next](3-java)|
