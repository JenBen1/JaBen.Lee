在Tomcat服务器部署完成后，要开始搭建自己的网站，可以按照以下详细步骤进行操作：

1. **确定网站结构与内容**：
   - 确定网站的目标、功能和界面设计。
   - 准备所需的静态资源（如HTML、CSS、JavaScript、图片等）和动态内容（如JSP、Servlet、数据库连接等）。
   - 如果网站包含动态功能，设计或选择合适的后台框架（如Spring MVC、Struts等）和数据库管理系统（如MySQL、PostgreSQL等）。

2. **创建Web项目**：
   - 使用集成开发环境（IDE）如Eclipse、IntelliJ IDEA等，创建一个新的Web项目。设置项目的编程语言、框架、构建工具等。
   - 手动创建标准的Web项目结构，确保项目包含以下基本目录：
     - `WEB-INF/`：存放应用的配置文件（如`web.xml`）和类库（`.jar`文件）。
     - `WEB-INF/classes/`：放置编译后的Java源码文件。
     - `WEB-INF/lib/`：存放项目依赖的第三方库。
     - `webapp/` 或 `src/main/webapp/`（Maven项目）：放置静态资源和JSP文件。
   - 编写网站所需的HTML、CSS、JavaScript等前端代码，以及后端Java代码（如Servlet、JSP、控制器类等）。

3. **配置Web应用**：
   - 编写或编辑`web.xml`文件，定义Servlet、过滤器、监听器等组件，以及初始化参数、安全约束等配置。
   - 如果使用框架，可能还需要配置框架相关的XML或注解（如Spring的`applicationContext.xml`、`dispatcher-servlet.xml`等）。
   - 配置数据库连接，如在`context.xml`中添加数据源（适用于Tomcat内置连接池）或在应用代码中配置JDBC连接。

4. **测试本地开发环境**：
   - 在IDE中配置Tomcat服务器（如果尚未配置），将其与Web项目关联。
   - 启动Tomcat服务器，通过访问`http://localhost:8080/your-project-context-path`（替换为实际项目上下文路径）来测试网站功能。
   - 调试代码，修复可能出现的错误，确保所有功能在本地环境中正常工作。

5. **打包Web项目**：
   - 使用IDE的构建工具（如Maven、Gradle）或手动执行命令行工具，将Web项目打包成WAR（Web Application Archive）文件。WAR文件包含了项目的所有依赖、资源和编译后的代码。
   - 对于Maven项目，通常通过运行`mvn clean package`命令生成WAR文件。

6. **部署到Tomcat服务器**：
   - 登录到已安装并运行的远程或本地Tomcat服务器。
   - 将生成的WAR文件复制到Tomcat的`webapps`目录下。
   - 如果Tomcat正在运行，它会自动检测到新添加的WAR文件并解压部署。如果未运行，启动Tomcat后，部署过程将在服务器启动时自动完成。

7. **访问与验证部署**：
   - 使用浏览器访问部署后的网站，URL通常为`http://your-server-ip:port/your-project-context-path`，其中：
     - `your-server-ip`：服务器的IP地址或域名。
     - `port`：Tomcat监听的端口号，通常是8080（如果没有修改默认配置）。
     - `your-project-context-path`：项目部署时的上下文路径，通常与WAR文件名相同（不带`.war`扩展名），或者在`META-INF/context.xml`中指定。
   - 测试网站的各项功能，确保它们在生产环境中正常工作。

8. **后续维护与更新**：
   - 如果需要更新网站内容或修复问题，重复上述打包和部署步骤，用新的WAR文件替换旧的。
   - 对于热部署支持的Tomcat版本，部分更改（如JSP、静态资源）可能无需重启服务器即可生效。

以上就是从零开始在已经部署好的Tomcat服务器上搭建自己网站的具体步骤。根据项目的具体技术和需求，步骤可能会有所调整。在实际操作过程中，务必注意版本兼容性、权限设置、防火墙规则等因素，确保部署过程顺利进行。