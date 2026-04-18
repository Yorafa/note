配置ssh以便免密快速连接, 首先先检查`~/.ssh/`文件夹下
1. 如果之前没有生成过`id_rsa`相关文件, 可以通过`ssh-keygen -t rsa -b 4096 -C "your_email@example.com"`生成ssh密钥。其中`-t rsa`指定了使用`rsa`加密算法, `-b 4096` 指定了密钥的位数, `-C "your_email@example.com"` 添加备注为自己的邮箱(备注也可以是其他的)。 
2. 非windows可以直接使用`ssh-copy-id user@server`进行复制。如果是windows打开`~/.ssh/`目录下的`id_rsa.pub`文件，复制里面的内容。进入server的`~/.ssh/authorized_keys`文件中，添加刚刚复制的内容。

### 配置SSH Client
可以通过`~/.ssh/config`文件来配置SSH客户端设置，以便简化连接命令。示例如下:
```sh
Host server
    HostName hostname
    User user
```
