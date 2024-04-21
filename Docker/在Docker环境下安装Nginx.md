在Docker环境下安装Nginx，可以按照以下步骤进行：

#### 1-安装Docker

确保你的系统上已安装Docker。如果你还没有安装，可以从[Docker官方网站](https://www.docker.com/)下载适用于你操作系统的Docker安装包，并按照官方文档的指示进行安装。

#### 2-拉取Nginx镜像

打开终端或命令提示符，输入以下命令来从Docker Hub下载最新版本的Nginx镜像：

```bash
docker pull nginx
```
如果你想拉取特定版本的Nginx，可以在`nginx`后加上版本标签，例如：
```bash
docker pull nginx:1.19
```

#### 3-查看下载的镜像

确认Nginx镜像是否成功下载：

```bash
docker images
```

#### 4-启动Nginx容器

使用以下命令启动Nginx容器，其中：

- `--name nginx` 指定容器的名称为`nginx`。
- `-p 80:80` 将宿主机的80端口映射到容器的80端口，以便外部可以访问Nginx服务。
- `-d` 表示以后台模式运行容器。
- 最后的`nginx`是指使用刚刚拉取的Nginx镜像。
```bash
docker run --name nginx -p 80:80 -d nginx
```

#### 5-验证Nginx是否启动成功

可以通过访问`http://localhost`（如果你是在本地宿主机上操作）来验证Nginx是否正确启动并对外提供服务。另外，可以使用以下命令检查容器状态：

```bash
docker ps
```

#### 6-（可选）自定义Nginx配置

如果你需要修改Nginx的配置或部署项目到Nginx，可以采取以下步骤：

- **进入容器**：使用`docker exec -it nginx /bin/bash`命令进入运行中的Nginx容器。
- **修改配置文件**：在容器内，Nginx的配置文件通常位于`/etc/nginx/nginx.conf`，你可以使用文本编辑器如`vi`或`nano`来修改它。
- **复制项目文件**：将你的项目文件复制到Nginx的默认网站根目录，通常是`/usr/share/nginx/html`。
- **重新加载配置**：修改配置后，执行`nginx -s reload`命令以重新加载Nginx配置，使更改生效。如果修改了配置文件路径或有其他重大更改，可能需要使用`nginx -t`测试配置文件，无误后再重启Nginx。

#### 7-（可选）持久化配置和数据

为了使你的Nginx配置和数据在容器重启后仍然存在，你可以通过映射卷的方式在启动容器时挂载宿主机的目录。例如，挂载配置文件和数据目录：

```bash
docker run --name nginx -p 80:80  --privileged=true -v /path/to/nginx/conf:/etc/nginx/conf.d -v /path/to/nginx/html:/usr/share/nginx/html -d nginx
```
这里，`/path/to/nginx/conf`和`/path/to/nginx/html`是你宿主机上存放Nginx配置文件和网页文件的目录。

按照以上步骤，你就能在Docker环境中成功安装并运行Nginx了。