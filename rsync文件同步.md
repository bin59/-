# 上传文件

安装

```bash
sudo apt-get install rsync
```

## rsync 命令

rsync 命令是远程同步命令，可以将本地文件或目录同步到远程服务器。

```bash
rsync -avz /local/path/ user@hostname:/remote/path/
```

这个命令将通过 SSH 将本地计算机上的文件夹上传到远程主机的目标路径下。您需要将/local/path/替换为本地计算机上的源文件夹路径，/remote/path/替换为远程主机上的目标路径，user 替换为远程主机上的用户名，hostname 替换为远程主机的主机名或 IP 地址。 参数解释：

- a：表示 archive 模式，包括所有文件，包括隐藏文件和目录。
- v：表示显示详细的进度和统计信息
- z：表示压缩数据。 使用 rsync 上传文件夹时，只需要指定源文件夹的路径，目标路径将自动创建。如果目标路径不存在，rsync 将自动创建它。您可以通过在目标路径后面添加/来确保它是一个目录。 此外，您还可以使用其他选项来自定义 rsync 的行为，例如--progress 表示显示传输进度，--partial 表示在传输中断时保留部分传输的文件等。您可以在 rsync 命令的手册页中找到更多选项和用法的信息。

rsync 用法教程：`http://www.ruanyifeng.com/blog/2020/08/rsync.html`
