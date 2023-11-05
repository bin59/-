# MySQL root 用户禁止远程登录 mysql 允许远程登录授权

Mysql 为了安全性，在默认情况下用户只允许在本地登录，可是在有此情况下，还是需要使用用户进行远程连接，因此为了使其可以远程需要进行如下操作：[原文](https://blog.51cto.com/u_16213604/7013865)

一、允许 root 用户在任何地方进行远程登录，并具有所有库任何操作权限，
具体操作如下：

在本机先使用 root 用户登录 mysql： mysql -u root -p"youpassword" 进行授权操作：

mysql>
GRANT ALL PRIVILEGES ON _._ TO 'root'@'%' IDENTIFIED BY 'youpassword' WITH GRANT OPTION;

1.
2. 重载授权表：

FLUSH PRIVILEGES;
退出 mysql 数据库：
exit

1.
2.
3. 这个可以指定任何一个用户的任何密码进行远程的登录,不建议使用 root 远程登录,有条件还是限制一个特定的 ip 进行登录最好.

二、允许 root 用户在一个特定的 IP 进行远程登录，并具有所有库任何操作权限，
具体操作如下： 在本机先使用 root 用户登录 mysql： mysql -u root -p"youpassword" 进行授权操作：

GRANT ALL PRIVILEGES ON _._ TO root@"xxxxxx" IDENTIFIED BY "youpassword" WITH GRANT OPTION;
重载授权表： FLUSH PRIVILEGES;
退出 mysql 数据库： exit

1.
2.
3.
4.
5. 三、允许 root 用户在一个特定的 IP 进行远程登录，并具有所有库特定操作权限，
   具体操作如下： 在本机先使用 root 用户登录 mysql： mysql -u root -p"youpassword" 进行授权操作：
   GRANT select，insert，update，delete ON _._ TO root@"xxxxxx" IDENTIFIED BY "youpassword";

重载授权表： FLUSH PRIVILEGES;
退出 mysql 数据库： exit

1.
2.
3.
4.
5. 四、删除用户授权，需要使用 REVOKE 命令，
   具体命令格式为： REVOKE privileges ON 数据库[.表名] FROM user-name;
   具体实例，先在本机登录 mysql: mysql -u root -p"youpassword"
   进行授权操作： GRANT select，insert，update，delete ON TEST-DB TO test-user@"xxxxxx" IDENTIFIED BY "youpassword";
   再进行删除授权操作： REVOKE all on TEST-DB from test-user;
6.
7.
8.
9. \*\*\*\*注：该操作只是清除了用户对于 TEST-DB 的相关授权权限，但是这个“test-user”这个用户还是存在。

最后从用户表内清除用户： DELETE FROM user WHERE user="test-user";
重载授权表： FLUSH PRIVILEGES;
退出 mysql 数据库： exit

1.
2.
3. 五、MYSQL 权限详细分类：
   全局管理权限：

FILE: 在 MySQL 服务器上读写文件。
PROCESS: 显示或杀死属于其它用户的服务线程。
RELOAD: 重载访问控制表，刷新日志等。
SHUTDOWN: 关闭 MySQL 服务。 数据库/数据表/数据列权限：
ALTER: 修改已存在的数据表(例如增加/删除列)和索引。
CREATE: 建立新的数据库或数据表。
DELETE: 删除表的记录。
DROP: 删除数据表或数据库。
INDEX: 建立或删除索引。
INSERT: 增加表的记录。
SELECT: 显示/搜索表的记录。
UPDATE: 修改表中已存在的记录。
特别的权限：

ALL: 允许做任何事(和 root 一样)。
USAGE: 只允许登录–其它什么也不允许做。
