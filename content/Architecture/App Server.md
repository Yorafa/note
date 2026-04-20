TL;DR
在一个应用中，完整的层级如下：
1. 网络层 & 协议层（Network & HTTP Parsing）
2. 抽象层（Request / Response / Context）
3. 调度层（Router / Middleware）
4. 业务层（Handler）
5. 表现层（Response Rendering，如：HTML / JSON / File）

## build from scratch

### 极简server
一个最简易app server需要什么呢？
1. 设置好一个server socket，并监听某个端口，例如3000
2. 接受client的连接
3. 读取请求并处理

就是这么简单，我们已经可以通过访问server的ip和端口来访问server了。可是不对啊，我的[HTTP](HTTP.md)去哪里了，我的网页又去哪里了？

别急，[HTTP](HTTP.md)本身只是一个通信规则，规定了server和client之间如何通信。在使用`curl`或者浏览器时，会自动加上这个协议头，而在server端，需要自己解析这个协议头，并根据协议头来处理请求。而网页，就是处理的一种结果，把HTML写回给client由浏览器渲染出来的就是一个网页了。而我们常说的`Request`和`Response`，就是client socket和server socket之间的符合[HTTP](HTTP.md)协议的通信内容。

那么现在我们多了一个步骤在server端，就是解析[HTTP](HTTP.md)协议，并根据协议来处理请求。即:
1. 设置好一个server socket，并监听某个端口，例如3000
2. 接受client的连接
3. 解析[HTTP](HTTP.md)协议
4. 根据解析出的协议来处理`Request`并生成`Response`
5. 将`Response`写回给client

### Router & Middleware

说的简单，但是处理请求又具体指的是什么呢？

对于一个web应用来说，就是根据不同的url来处理不同的请求，可以是：
- 返回一个HTML页面
- 返回一个JSON数据
- 返回一个文件
- 重定向到另一个url
- ...

那么，我们最好需要一个数据结构来存储这些url和对应的处理函数，也就是我们常说的`Router`。

同时，我们不难发现，平时上网的时候经常看到不同的url对应着不同的权限，方法，例如`/api/...`, `/admin/...`等，所以我们还需要一个`RouterGroup`来划分管理不同的路由。

对于这些`Router`，我们可能需要验证，logging或者其他操作，所以我们可以把这些操作抽象成`Middleware`。也就是说每个不同的`RouterGroup`甚至于每个`Router` 都可以有自己的`Middlewares`。

那么现在我们的server端需要做的事情就变成了：
1. 设置好一个server socket，并监听某个端口，例如3000
2. 接受client的连接
3. 解析[HTTP](HTTP.md)协议
4. 根据解析出的协议和`Request`来匹配对应的`RouterGroup`，
5. 找到对应的`Router`和`Handler`
6. 基于需求使用`Middlewares`和`Handler`来处理请求，并生成`Response`
7. 将`Response`写回给client

### Context

现在我们输入一串url，比如`http://localhost:3000/api/v1/users`，但进server端，我们就发现我们要带着一大堆东西传来传去，比如：
- `Request`
- `Response`
- 路由参数
- 状态
- 错误
- Middlewares
- ...

所以，我们需要一个数据结构来存储这些东西，也就是我们常说的`Context`。