```ini
[Unit]
Description=MySQL Community Server
After=network.target
[Service]
User=mysql
Group=mysql
ExecStart=/etc/rc.d/init.d/mysqld --daemonize --pid-file=/var/run/mysqld/mysqld.pid
Restart=on-failure
RestartSec=5s

[Install]
WantedBy=multi-user.target
```

/usr/local/mysql/bin/mysqld_safe



[Unit]
Description=MySQL Community Server
After=network.target

[Service]
ExecStart=/usr/local/mysql/bin/mysqld_safe --daemonize --pid-file=/usr/local/mysql/data/mysqld.pid

ExecStop=/usr/local/mysql/bin/mysqladmin shutdown

Restart=on-failure
RestartSec=5s

[Install]
WantedBy=multi-user.target



手动启动：

/usr/local/mysql/bin/mysqld_safe --defaults-file=/etc/my.cnf

sudo /usr/local/mysql/bin/mysql start



要给 `/var/run/mysqld/mysqld.pid` 文件添加可执行权限，可以使用以下命令：

```bash
sudo chmod +x /var/run/mysqld/mysqld.pid
```