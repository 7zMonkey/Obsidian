1. 更新软件包列表：打开终端，运行以下命令更新软件包列表：

```
sudo apt update
```

2. 安装MySQL服务器：运行以下命令安装MySQL服务器：

```
sudo apt install mysql-server
```

在安装过程中，你将会被要求设置MySQL的root用户密码。请确保设置一个强密码并记住它。

3. 启动MySQL服务：安装完成后，运行以下命令启动MySQL服务：

```
sudo systemctl start mysql
```

4. 设置MySQL开机自启：如果你希望MySQL在系统启动时自动启动，可以运行以下命令设置开机自启：

```
sudo systemctl enable mysql
```

5. 验证安装：运行以下命令验证MySQL是否成功安装：

```
mysql --version
```

如果安装成功，你将看到MySQL的版本信息。