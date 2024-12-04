# Nginx 安装及配置

## Linux 环境

### 安装

```bash
apt-get install nginx
```

1. 目录说明

```
/usr/sbin/nginx：主程序，启动文件
/etc/nginx：存放配置文件
/var/www/html：存放项目目录
/var/log/nginx：存放日志
```

2. 启动

```bash
service nginx start
```

3. 重启

```bash
service nginx restart
```

4. 停止

```bash
service nginx stop
```

### 配置

. 重启 Nginx 服务。

```bash
sudo systemctl restart nginx
```

. 检测配置文件是否正确

```bash
nginx -t
```

## Windows 环境

在 Windows 环境下配置 Nginx 主要涉及以下几个步骤：

1. 下载与安装 Nginx
   搜索下载：访问 Nginx 官方网站或其在 GitHub 上的发布页面，找到适合 Windows 系统的 Nginx 稳定版本进行下载。
   解压安装：下载完成后，将压缩包解压到你希望安装 Nginx 的目录，如 C:\nginx。解压后，Nginx 的可执行文件（nginx.exe）位于 sbin 文件夹内。

2. 配置 Nginx
   修改配置文件：定位到解压目录下的 conf/nginx.conf 文件，使用文本编辑器（如 Notepad++）打开它。这个文件控制着 Nginx 的行为，包括监听端口、服务器根目录、日志文件位置等。
   若要设置网站根目录，修改 http 块内的 server 部分，如：
   nginx
   server {
   listen 80;
   server_name localhost;
   root /path/to/your/site; # ...
   }
   启用目录列表：如果需要让 Nginx 显示目录内容，可以在某个 location 块中加入如下配置：
   nginx
   autoindex on;

3. 启动与测试 Nginx
   命令行启动：以管理员身份运行命令提示符（CMD）或 PowerShell，切换到 Nginx 的解压目录（例如 cd C:\nginx），然后执行以下命令启动 Nginx：
   sh
   start nginx
   检查运行状态：在浏览器中访问 http://localhost，如果一切配置正确，你应该能看到 Nginx 的默认欢迎页。

4. 开机自启动配置
   为了使 Nginx 在 Windows 启动时自动运行，你可以采取以下几种方法之一：

使用任务计划程序：

打开“任务计划程序”。
创建基本任务，命名（如“启动 Nginx”）。
触发器选择“当计算机启动时”。
操作选择“启动程序”，浏览到 Nginx 的 nginx.exe 路径。
完成创建任务。
使用 NSSM（Non-Sucking Service Manager）：

下载并安装 NSSM。
以管理员身份运行命令提示符，执行类似 nssm install nginx 的命令。
在 NSSM 的界面中，设置应用程序路径为 Nginx 的 nginx.exe，以及启动参数（如果有）。
安装服务并启动。

5. 日志与错误排查
   查看日志：Nginx 的日志通常位于 logs 目录下，包括 access.log（访问日志）和 error.log（错误日志）。遇到问题时，检查这些日志是解决问题的关键。
   异常处理：如果 Nginx 未能启动，检查错误日志，常见的问题包括端口被占用、配置文件语法错误等。根据错误信息进行相应调整。
   以上步骤应该能帮助你在 Windows 环境中成功配置并运行 Nginx。

### 查看 Nginx 服务进程

在 Windows 环境下查看 Nginx 服务进程，你可以采用以下方法：

使用命令提示符或 PowerShell
以管理员身份打开命令提示符或 PowerShell。
输入以下命令来查看所有包含“nginx”关键词的进程：
cmd
tasklist | findstr nginx
这条命令会列出所有进程中包含“nginx”字样的条目，从而帮助你确认 Nginx 服务是否正在运行及其进程 ID。

查看任务管理器
右键点击任务栏，选择“任务管理器”打开，或者通过快捷键 Ctrl+Shift+Esc 直接打开。
在任务管理器的“进程”或“详细信息”标签页中，滚动查找是否有名为“nginx.exe”的进程。这可以直接显示出 Nginx 是否正在运行以及它的资源使用情况。
查看 Nginx PID 文件
虽然这种方法不如前两种直观，但在某些情况下也有所帮助。如果 Nginx 配置中启用了 PID 文件记录（默认情况下通常会），你可以直接查看该文件来获取 Nginx 进程 ID。

打开命令提示符或 PowerShell，进入 Nginx 的安装目录，通常是 C:\nginx\logs。
查看是否存在一个名为 nginx.pid 的文件。如果 Nginx 正在运行，这个文件应该存在，并且里面包含了 Nginx 主进程的 PID。
通过上述任一方法，你都可以有效地查看到 Windows 系统中 Nginx 服务的进程状态。

#### 在 Windows 环境下结束所有 Nginx 进程

可以使用命令提示符或 PowerShell，并以管理员身份运行。以下是最直接有效的方法：

使用 taskkill 命令
打开命令提示符（管理员权限）：右键点击“开始”按钮或按下 Win+X，选择“Windows PowerShell（管理员）”或“命令提示符（管理员）”。

执行命令结束进程：输入以下命令来强制终止所有名为“nginx.exe”的进程：

cmd
taskkill /F /IM nginx.exe
/F 参数表示强制终止进程。
/IM 参数后面跟的是进程的映像名称，在这里是“nginx.exe”。
这条命令会立即结束所有与 Nginx 相关的进程，包括主进程及其子进程。

验证进程是否已结束

执行完上述命令后，你可以再次使用下面的命令来验证是否还有名为“nginx”的进程在运行：

cmd
tasklist | findstr nginx
如果命令输出为空，说明所有 Nginx 进程已经被成功终止。

请注意，强制终止进程可能会导致数据丢失或不一致的状态，特别是在 Nginx 处理请求时。因此，推荐在大多数情况下先尝试正常停止 Nginx 服务（如使用 nginx -s quit 命令优雅关闭），然后再进行操作。但在需要快速关闭所有进程的情况下，上述 taskkill 命令是最直接的解决方案。
