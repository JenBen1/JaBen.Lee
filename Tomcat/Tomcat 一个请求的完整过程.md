Tomcat 一个请求的完整过程:

Tomcat 是一个流行的 Java Web 应用服务器，负责接收、解析和处理 HTTP 请求。以下是一个请求在 Tomcat 中的简单模式化处理过程，以便理解：

**1. **客户端发起请求**:

   - 用户在浏览器中输入 URL 或点击链接，浏览器构建一个 HTTP 请求（包含方法、URL、头信息、可能的请求体等）并发送至指定服务器地址。

**2. **到达 Tomcat 服务器**:
   - 请求通过网络传输到达 Tomcat 监听的端口（默认为 8080）。
   - Tomcat 的 TCP/IP 套接字监听器接收到请求，并将其交给专门处理 HTTP 协议的连接器（Connector）。

**3. **连接器处理**:

   - 连接器解析 HTTP 请求头，可能进行 SSL/TLS 加密解密（如果启用了 HTTPS）。
   - 连接器根据请求的域名和端口找到对应的虚拟主机（Host）。

**4. **映射请求到 Servlet**:

   - 在虚拟主机层面，连接器根据请求的 URL 路径查找对应的 Context（Web 应用上下文）。
   - 在 Context 中，根据 `web.xml` 配置或 `@WebServlet` 注解，找到匹配的 Servlet。
   - 如果存在 URL 重写规则（如通过 `RewriteValve` 或第三方库如 Spring MVC），此时可能进行 URL 转换。

**5. **Servlet 实例化与调用**:
   - 如果 Servlet 实例尚未创建，Tomcat 会使用反射机制实例化 Servlet，并调用其 `init()` 方法进行初始化（仅首次请求时）。
   - 连接器调用找到的 Servlet 的 `service()` 方法（或 `HttpServlet` 的 `doGet()`、`doPost()` 等方法）来处理请求。
   - 在 `service()` 方法中，Servlet 通过 `HttpServletRequest` 获取请求参数、执行业务逻辑，然后通过 `HttpServletResponse` 构建响应。

**6. **生成响应**:
   - Servlet 完成业务处理后，向 `HttpServletResponse` 写入响应状态码、响应头和响应体（HTML、JSON、XML 等）。
   - 连接器将响应封装成 HTTP 响应消息，通过套接字发送回客户端。

**7. **客户端接收响应**:
   - 浏览器接收到 HTTP 响应，解析响应头和响应体。
   - 根据响应状态码判断请求是否成功。
   - 使用响应体数据（如 HTML 文档）渲染页面或处理其他类型的数据（如 JSON）。

**8. **请求结束与资源清理**:
   - 请求处理完成后，如果 Servlet 实现了 `destroy()` 方法且容器决定要卸载该 Servlet，会调用 `destroy()` 方法进行资源清理（例如关闭数据库连接）。

总结来说，一个请求在 Tomcat 中的完整过程包括：
- 客户端发起 HTTP 请求。
- 请求到达 Tomcat 并被连接器接收。
- 连接器解析请求，映射到具体的 Servlet。
- 创建或复用 Servlet 实例，调用其 `service()` 方法处理请求。
- Servlet 构建响应，连接器将响应发送回客户端。
- 客户端接收并处理响应。
- 请求结束后，可能进行 Servlet 资源清理。

这个过程体现了 Tomcat 作为 Web 服务器的核心职责：接收、解析、路由 HTTP 请求，并与 Servlet（或任何其他符合规范的 Web 组件）协作，生成并返回响应给客户端。