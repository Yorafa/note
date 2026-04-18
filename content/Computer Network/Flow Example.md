用户点击网页：
1. **L7**：发送HTTPS请求, 根据HTTPS构造请求内容，包括 URL、Headers、Cookies 等
2. **L6**：根据TLS进行加密，压缩
3. **L5**：建立TLS 会话，管理连接状态
4. **L4**：使用TCP建立连接，将数据分成多个 TCP segments, 添加源端口 / 目标端口，序号、ACK、窗口大小等控制信息
5. **L3**：将 TCP segment 封装成 IP packet, 添加源 IP 和目标 IP, 选择路由路径
6. **L2**：- 将 IP packet 封装成 Ethernet frame, 添加源 MAC 和目标 MAC 地址, 在局域网内通过交换机转发
7. **L1**：- 将 Ethernet frame 转换成电信号或光信号, 通过网线、Wi-Fi、光纤等物理介质传输
服务器收到信号后，按以下顺序还原数据：
8. **L1**：接收信号 → 比特流 
9. **L2**：解析 Ethernet frame → IP packet
10. **L3**：解析 IP packet → TCP segment
11. **L4**：重组 TCP segment → TLS payload
12. **L5**：恢复 TLS 会话状态
13. **L6**：解密、解压 → HTTP 请求
14. **L7**：处理请求，返回网页内容（HTML、CSS、JS）
然后服务器的响应会按同样的流程从 L7 → L1 发回用户。

所以一个完整的网络请求包有
1. 源 MAC 和目标 MAC 地址
2. 源 IP 和目标 IP
3. 源端口 / 目标端口，序号、ACK、窗口大小等控制信息
4. TLS信息
5. URL、Headers、Cookies 等