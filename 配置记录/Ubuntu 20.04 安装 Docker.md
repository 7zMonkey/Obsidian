从Ubuntu 20.04版本开始，Docker已经成为Ubuntu官方软件仓库的一部分，因此你可以直接从官方仓库安装Docker。这使得在Ubuntu 20.04上安装和使用Docker变得更加方便。

可以按照以下步骤在Ubuntu 20.04上安装Docker：

1. 更新软件包列表：打开终端，运行以下命令更新软件包列表：

```
sudo apt update
```

2. 安装Docker：运行以下命令安装Docker：

```
sudo apt install docker.io
```

3. 启动Docker服务：安装完成后，运行以下命令启动Docker服务：

```
sudo systemctl start docker
```

4. 设置Docker开机自启：如果你希望Docker在系统启动时自动启动，可以运行以下命令设置开机自启：

```
sudo systemctl enable docker
```

5. 验证安装：运行以下命令验证Docker是否成功安装：

```
docker --version
```

如果安装成功，你将看到Docker的版本信息。

现在，已经成功在Ubuntu 20.04上安装了Docker