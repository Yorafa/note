每个人在外都或多或少有访问自己家里设备的需求，但是给家里的网络配上ipv6或者公网ipv4都是费时费力的事情。这里我推荐使用 [frp](https://github.com/fatedier/frp) 进行内网穿透，使家庭内的网络可以在外部访问。而这仅仅需要一台具有公网的设备, 最简单的方法是买一台服务器。

这里我推荐[vultr](https://www.vultr.com/?ref=7560304), 在全球多个城市都有节点可以选择。云计算最低只需6美刀一个月。我使用了相当长的一段时间，直到我毕业没有经济来源。

如果你像我一样贫困，那么更推荐你使用 [cloudcone](https://app.cloudcone.com/?ref=12028), 它经常会有活动。即使在没有活动的情况下最低配置也只需21.6美刀一年。

在根据自己的偏好(建议大家使用linux, 本文将以ubuntu系统为背景介绍) deploy好自己的vps后接下来就需要安装docker了
## 安装Docker

为什么要安装docker？docker是一种广泛使用的容器化技术，它提供了一种轻量级、便携和高效的方式来构建、运行和共享应用程序. 对于环境配置苦手来说简直就是神器，只需要pull image然后run container就可以轻松运行服务，再也不用担心运行一大堆script结果还有很多报错，然后查了很久最后放弃的这种情况了。

安装最好参考[docker 官网](https://docs.docker.com/engine/install/ubuntu/), 一般情况下参考 Install using the apt repository下的3个步骤即可成功安装。

如果实在偷懒不想看官网介绍，那么就复制下面的命令到命令行中 
```sh
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

PS: 一般情况下如果你是root登录到vps中，可以省去sudo
## 安装npm

此npm非彼npm，这里的npm指的是[nginx proxy manager](https://nginxproxymanager.com/),  愿意自己看文档的建议看文档以加深对npm的理解. 如果不需要配置域名直接连接到对应web service，申请ssl等服务的话可以跳过这步。

**注意npm只需要在cloud server中安装**. 安装npm只需要创建一个空目录, 然后进这个目录里
```sh
# to home directory
cd ~ 
# create a directory named npm
mkdir npm
# go to directory
cd ./npm
# create docker compose configuration file
touch docker-compose.yml
# create docker network
sudo docker network create npmcontrol
```

创建一个docker network是为了使所有的docker container都在同一个网络下，这将方便npm后续的管理。

复制下面的配置文件到`docker-compose.yml`中:
```yml
version: '3.8'
services:
  app:
    image: 'jc21/nginx-proxy-manager:latest'
    restart: unless-stopped
    ports:
      # These ports are in format <host-port>:<container-port>
      - '80:80' # Public HTTP Port
      - '443:443' # Public HTTPS Port
      - '81:81' # Admin Web Port
    volumes:
      - ./data:/data
      - ./letsencrypt:/etc/letsencrypt
networks:
  default:
    external: true
    name: npmcontrol
```
保存并在命令行中使用
``` sh
sudo docker compose up -d
```

等看到类似`container npm-app-1 running`之类的文字的时候表示你已经安装好了npm。

现在赶紧打开浏览器输入`http://公网ip:81` (一般情况下vps的公网ip会显示在运营商页面上，会直接告诉你). 如果不知道自己的ip，也可以使用下面命令:
```sh
ifconfig
```
在出来结果后，找到`eth0`，下面的`inet`一般来说就是你的公网ip.

在浏览器访问以后，会看到npm让你登录的界面，默认的账号密码为
```
Email:    admin@example.com
Password: changeme
```
登录后会让你修改邮箱密码。

如果你打算使用npm发挥出它的功能，那么你需要有一个或数个域名，并绑定到你的云服务器上。

老样子，在浏览器输入`http://ip:81`并进行登录，分别执行下面几步操作
1. 选择hosts -> proxy hosts
2. 点击add proxy host
3. 在domain names填入你刚刚绑定的域名例如`npm.domain.com` 
4. 在forward hostname/IP一栏填入`npm` (如果你给你的npm取了其他的container name就填那个),
5. forward port填写`81`
6. 下面三个可以去了解一下作用在决定开不开。
7. 此外如果你想通过https访问那么点击ssl, 选择request a new ssl certificate。
8. 点击save
9. 稍等片刻你就可以通过`npm.domain.com`进入你的npm了。
## 安装frp

[frp](https://github.com/fatedier/frp) 指代的是fast reverse proxy, 具体分为frps和frpc. s表示server, c表示client.

首先来让我们安装client
### 本地电脑
请先确保本地电脑也装了docker，如果没有请follow上面的安装docker的步骤。此外本地电脑很有可能需要配置用户组，官网同样有介绍。如果有需求请评论。

1. 创建一个folder
```sh
# to home directory
cd ~ 
# create a directory named npm
mkdir frpc
# go to directory
cd ./frpc
# create docker compose configuration file
touch docker-compose.yml
# create frps configuration file
touch frpc.toml
```
2. 同样的copy下面的配置
```yml
# docker-compose.yml
services:
  frps:
    image: 'snowdreamtech/frpc'
    restart: always
    network_mode: "host"
    volumes:
      - './frpc.toml:/etc/frp/frpc.toml'
```
这里使用host network就可以监管主机上的所有端口，无需自己手动添加进docker-compose 里了
3. 保存后我们还需要配置frpc
```toml
# frpc.toml
serverAddr = "your.ip.add.ress"
serverPort = 7000
auth.method = "token"
auth.token = "yourtoken"

[[proxies]]
name = "ssh"
type = "tcp"
localIP = "127.0.0.1"
localPort = 22
remotePort = 6000
```

这里添加了一个ssh proxy，如果后续vps上的fprs布置成功，就可以使用`ssh -P 6000 user@ip` 连接到本地的shell. （user是你本地电脑用户的用户名，但是ip还是你的公网ip，如果不知道的话可以参考上面安装npm的介绍). 此外auth是你所需的验证，如果你不需要或者不想添加验证直接删除即可(记得`frps.toml`也要删除).
4. 在命令运行指令
```sh
sudo docker compose up -d
```
### vps

1. 同样的创建一个folder
```sh
# to home directory
cd ~ 
# create a directory named npm
mkdir frps
# go to directory
cd ./frps
# create docker compose configuration file
touch docker-compose.yml
# create frps configuration file
touch frps.toml
```
2. 同样的copy下面的配置
```yml
# docker-compose.yml
services:
  frps:
    image: 'snowdreamtech/frps'
    restart: always
    volumes:
      - './frps.toml:/etc/frp/frps.toml'
    ports:
      # if any more ports require add here
	  - "7000:7000"
	  - "6000:6000"
# if you don't use npm ignore following
networks:
  default:
    external: true
    name: npmcontrol
```
3. 保存后我们还需要配置frps
```toml
# frps.toml
bindPort = 7000
auth.method = "token"
auth.token = "yourtoken"
```
这里port是7000, 如果你需要改成其他的port, 那么记得在本地电脑的frpc configuration里，以及上面的`docker-compose.yml`也做对应的修改。此外如果你不想连接需要验证的话可以把两行auth删掉，同样的也把本地电脑的auth也删掉。

4. 在命令行中使用
``` sh
sudo docker compose up -d
```
这样就部署好了.

使用`sudo docker log frps`可以查看是否连接成功。也可以使用上面介绍连接ssh的方法测试是否连接成功

## 在外连接本地的web service

假设我有个web service运行在本地8080端口，即在自己电脑上可以通过使用浏览器`localhost:8080`访问。那么我只需要在本地电脑的`~/frpc/frpc.toml`文件中添加新的
```toml
[[proxies]]
name = "my local web service"
type = "tcp"
localIP = "127.0.0.1"
localPort = 8080
remotePort = 8080
```
这里remote port是指frps的docker network中的port，请确保没被占用. 在添加完之后使用:
```sh
sudo docker compose restart
```
### 不使用npm的设置
如果你不打算使用npm，那么现在连接到云服务上，在`~/frps/docker-compose.yml`文件中
```yml
# docker-compose.yml
services:
  frps:
    image: 'snowdreamtech/frps'
    restart: always
    volumes:
      - './frps.toml:/etc/frp/frps.toml'
    ports:
      # if any more ports require add here
	  - "7000:7000"
	  - "6000:6000"
	  - "8080:8080"
# if you don't use npm ignore following
networks:
  default:
    external: true
    name: npmcontrol
```
添加了8080端口，现在使用:
```sh
sudo docker compose restart
```
然后稍等片刻，就可以使用`ip:8080`访问你的内网服务了！

### 使用npm的设置
使用npm与刚开始设置`npm.domain.com`的操作别无不同。
在浏览器输入`https://npm.domain.com`并进行登录(如果你没有ssl那么输入`http://npm.domain.com`，如果你没有设置npm的域名请回到上面安装npm进行设置(如果你不想的话也可以直接进行下面操作))，分别执行下面几步操作
1. 选择hosts -> proxy hosts
2. 点击add proxy host
3. 在domain names填入你刚刚绑定的域名例如`inetwebservice.domain.com` 
4. 在forward hostname/IP一栏填入`frps` (如果你给你的frps取了其他的container name就填那个),
5. forward port填写`8080` (填的是frpc中的remote port)
6. 下面三个可以去了解一下作用在决定开不开。
7. 此外如果你想通过https访问那么点击ssl, 选择request a new ssl certificate。
8. 点击save
9. 稍等片刻你就可以通过`inetwebservice.domain.com`进入你的内网应用了。