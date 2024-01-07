# Nginx 安装及配置

## 安装

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

## 配置

. 重启 Nginx 服务。

```bash
sudo systemctl restart nginx
```

. 检测配置文件是否正确

```bash
nginx -t
```
