目前主流的session management有两种
1. cookie: 在登录之后建立session，服务端会生成session id，记录并设置好session cookie(一般来说会使用[redis](redis)等memory based数据库以防止服务器崩溃而导致的信息丢失)。
2. token: 在登录之后，服务端会生成token，客户端保存然后请求带 `Authorization: Bearer TOKEN`。