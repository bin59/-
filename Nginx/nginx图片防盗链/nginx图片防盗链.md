# nginx 图片防盗链

```
在Nginx中配置图片防盗链的步骤如下：

在Nginx的配置文件中打开或创建用于配置图片防盗链的location块。例如，以下代码将打开一个名为image防盗链的location块：
location @image防盗链 {
    # 防盗链配置代码
}
在location块中设置允许访问的源IP地址或域名。可以使用allow和deny指令来配置白名单或黑名单。例如，以下代码将只允许来自192.168.0.0/16网段的访问：
location @image防盗链 {
    allow 192.168.0.0/16;
    deny all;
}
设置Referer防盗链。使用referer模块，并使用referer in正则表达式来限制Referer地址。例如，以下代码将只允许来自以.example.com结尾的Referer地址：
location @image防盗链 {
    referer /example.com$;
    deny all;
}
设置HTTP Referer和Origin防盗链。使用sub_filter模块和sub_filter_once on参数来替换返回的图片链接。例如，以下代码将替换返回的图片链接中的http://example.com为http://othersite.com：
location @image防盗链 {
    sub_filter http://example.com http://othersite.com;
    sub_filter_once on;
    ...
}
设置Content-Disposition防盗链。使用if指令和$arg_url正则表达式来判断请求参数中的url是否符合要求。例如，以下代码将只允许返回attachment类型的图片：
location @image防盗链 {
    if ($arg_url ~* ^attachment$) {
        set $content_disposition attachment;
    } else {
        set $content_disposition inline;
    }
    ...
}
以上是一些基本的图片防盗链配置方法，你可以根据自己的需求进行组合使用。注意，在配置防盗链时应该考虑到误拦截的情况，及时添加例外规则。
```

```
要在 Nginx 中实现图片防盗链，你可以按照以下步骤进行配置：

步骤 1：编辑 Nginx 配置文件
使用文本编辑器打开 Nginx 的配置文件，通常位于 /etc/nginx/nginx.conf 或 /etc/nginx/conf.d/default.conf。如果是使用虚拟主机配置，可以编辑相应虚拟主机的配置文件。

shell
sudo nano /etc/nginx/nginx.conf
步骤 2：添加图片防盗链配置
在 server 块中添加如下代码，用于设置图片防盗链规则。

nginx
location ~* \.(jpg|jpeg|png|gif)$ {
    valid_referers none blocked yourdomain.com;
    if ($invalid_referer) {
        return 403;
    }
}
这段配置指定了允许访问的图片类型（这里是 jpg、jpeg、png 和 gif）。valid_referers 指令设置允许的 referer 来源，其中 none 表示不允许任何来源访问，blocked 表示不允许直接链接访问，只允许通过合法的 referer 访问，yourdomain.com 表示允许自己网站的页面访问。

if ($invalid_referer) 条件判断用于检查请求的 referer 是否合法。如果 referer 不合法，则返回 403 Forbidden 错误。

步骤 3：保存并关闭配置文件
完成配置后，保存并关闭 Nginx 配置文件。

步骤 4：检查配置是否有效
使用以下命令验证 Nginx 配置是否正确：

shell
sudo nginx -t
如果输出显示 nginx: configuration file /etc/nginx/nginx.conf test is successful，则表示配置有效。

步骤 5：重新加载 Nginx 配置
重新加载 Nginx 配置使其生效。

shell
sudo systemctl reload nginx
现在，Nginx 已经配置了图片防盗链。只有允许的 referer 才能正常加载图片资源，其他网站无法直接链接到图片。

请注意，该方法并非绝对安全，因为 referer 可以被伪造。但对于大多数情况下防止盗链已经足够了。
```
