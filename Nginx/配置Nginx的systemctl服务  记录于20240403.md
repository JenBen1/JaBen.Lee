配置Nginx的systemctl服务  记录于20240403

1. 创建一个新的服务单元文件：/etc/systemd/system/目录下

sudo vim /etc/systemd/system/nginx.service 

2. 以下内容粘贴到文件中（请根据您的实际情况修改路径和端口）：

 [Unit]

Description=The Nginx HTTP Server

After=network.target

 [Service]

Type=forking

PIDFile=/usr/local/nginx/logs/nginx.pid

ExecStartPre=/usr/local/nginx/sbin/nginx -t -c /usr/local/nginx/conf/nginx.conf

ExecStart=/usr/local/nginx/sbin/nginx -c /usr/local/nginx/conf/nginx.conf

ExecReload=/bin/kill -s HUP $MAINPID

ExecStop=/bin/kill -s TERM $MAINPID

PrivateTmp=true

 [Install]

WantedBy=multi-user.target 

3. 保存并关闭文件。

  4.重新加载systemd配置：

 sudo systemctl daemon-reload

5. 启动Nginx服务：

 sudo systemctl start nginx

6. 设置Nginx服务在系统启动时自动启动：

 sudo systemctl enable nginx

已经成功配置了Nginx以便使用systemctl服务。

7.检查Nginx服务的状态：

 sudo systemctl status nginx

8.检查自启动是否成功：

sudo systemctl is-enabled nginx

9.想禁止Nginx在系统启动时自动启动，使用以下命令：

sudo systemctl disable nginx