# Solo

GitHub 地址：`https://github.com/88250/solo`

```bash
docker run --detach --name solo --network=host \
    --env RUNTIME_DB="MYSQL" \
    --env JDBC_USERNAME="root" \
    --env JDBC_PASSWORD="123456" \
    --env JDBC_DRIVER="com.mysql.cj.jdbc.Driver" \
    --env JDBC_URL="jdbc:mysql://127.0.0.1:3306/solo?useUnicode=yes&characterEncoding=UTF-8&useSSL=false&serverTimezone=UTC&allowPublicKeyRetrieval=true" \
    b3log/solo --listen_port=8080 --server_scheme=http --server_host=localhost --server_port=

```

上面的去掉 `\` 换成一行运行

启动参数说明：

- --listen_port：进程监听端口
- --server_scheme：最终访问协议，如果反代服务启用了 HTTPS 这里也需要改为 https
- --server_host：最终访问域名或公网 IP，不要带端口
- --server_port：最终访问端口，使用浏览器默认的 80 或者 443 的话值留空即可
