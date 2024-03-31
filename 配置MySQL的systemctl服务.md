在Linux系统中，`systemctl`是一个用于管理系统服务的工具，包括启动、停止、重启、查看状态等操作。要配置MySQL的`systemctl`服务，主要是指配置MySQL服务单元文件（通常为`mysqld.service`），以便系统能够通过`systemctl`命令正确管理和控制MySQL服务。以下是配置MySQL服务的步骤：

**步骤1：确认MySQL服务单元文件**

首先，确认MySQL服务单元文件是否存在。在大多数Linux发行版中，MySQL服务单元文件通常位于`/lib/systemd/system`或`/etc/systemd/system`目录下，文件名通常为`mysqld.service`。可以通过以下命令查找：

```bash
ls /lib/systemd/system/mysqld.service /etc/systemd/system/mysqld.service
```

如果文件存在，可以直接编辑它进行配置。如果文件不存在，您可能需要手动创建或通过安装MySQL时提供的脚本自动生成。

**步骤2：编辑MySQL服务单元文件**

使用文本编辑器打开MySQL服务单元文件（如`/lib/systemd/system/mysqld.service`或`/etc/systemd/system/mysqld.service`），进行如下配置：

```ini
[Unit]
Description=MySQL Community Server
After=network.target

[Service]
User=mysql
Group=mysql
ExecStart=/usr/sbin/mysqld --daemonize --pid-file=/var/run/mysqld/mysqld.pid
Restart=on-failure
RestartSec=5

[Install]
WantedBy=multi-user.target
```

以上配置内容简要说明如下：

- `[Unit]`部分：
  - `Description`：为服务提供一个描述性名称。
  - `After`：指定服务启动依赖的系统服务，这里设置为`network.target`，确保网络服务启动后再启动MySQL。

- `[Service]`部分：
  - `User`和`Group`：指定MySQL服务运行的用户和组，通常为`mysql`。
  - `ExecStart`：指定启动MySQL服务的命令，这里使用`mysqld`二进制文件，加上必要的启动参数，如`--daemonize`使其作为守护进程运行，`--pid-file`指定进程ID文件的位置。
  - `Restart`：设置当服务意外退出时的重启策略，`on-failure`表示只有在出现故障时才重启。
  - `RestartSec`：设置服务重启之间的间隔，这里是5秒。

- `[Install]`部分：
  - `WantedBy`：定义该服务属于哪个目标（target），这里设置为`multi-user.target`，意味着在多用户模式下（如运行级别3或5）启动系统时，MySQL服务应被自动启动。

**步骤3：重新加载 systemd 配置并启动MySQL服务**

配置完成后，需要重新加载`systemd`配置以使改动生效，并启动MySQL服务：

```bash
sudo systemctl daemon-reload
sudo systemctl start mysqld
```

**步骤4：设置MySQL服务开机自启动**

如果希望MySQL服务在系统启动时自动运行，可以执行以下命令：

```bash
sudo systemctl enable mysqld
```

至此，您已经完成了MySQL服务的`systemctl`配置。现在可以通过`systemctl`命令轻松管理MySQL服务，如：

```bash
sudo systemctl status mysqld  # 查看服务状态
sudo systemctl restart mysqld  # 重启服务
sudo systemctl stop mysqld  # 停止服务
sudo systemctl enable mysqld #自启动
```

请根据您的实际环境和MySQL安装情况调整配置文件中的路径和参数。如果有特定的MySQL配置需求（如调整配置文件路径、添加额外启动参数等），应在`ExecStart`行中相应修改。