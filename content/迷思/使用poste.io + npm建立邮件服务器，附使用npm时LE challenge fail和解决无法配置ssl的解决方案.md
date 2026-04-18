## 安装poste.io

1. 首先请确保你有安装docker, 如果没有可以参考[文章](使用docker+frp+npm，让旧电脑成为新服务器)
2. 建议使用docker compose进行部署, 对应的端口介绍请参考[官网](https://poste.io/doc/getting-started), 如果对禁用反病毒功能（DISABLE_CLAMAV）、禁用反垃圾邮件功能（DISABLE_RSPAMD）有需求可以把对应的true改成false。但是相应的，可能内存和cpu占用会提高。

```yml
# docker-compose.yml
services:
  mailserver:
    image: analogic/poste.io
    container_name: mailserver
    hostname: mail.yourdomain.com
    ports:
      - "25:25"
      - "110:110"
      - "143:143"
      - "587:587"
      - "993:993"
      - "995:995"
      - "4190:4190"
      - "465:465"
      - "8808:80"
      - "8843:443"
    environment:
      - LETSENCRYPT_EMAIL=admin@yourdomain.com
      - LETSENCRYPT_HOST=mail.yourdomain.com
      - VIRTUAL_HOST=mail.yourdomain.com
      - DISABLE_CLAMAV=TRUE
      - DISABLE_RSPAMD=TRUE
      - HTTPS=OFF
    volumes:
      - ./mail-data:/data
    restart: unless-stopped
```

3. 使用`sudo docker compose up -d`启动mail server
4. 确保你的域名`mail.yourdomain.com`在dns解析中解析到了你的服务器。 更具体的，在你的域名提供商那里选择dns记录，在添加时类型选择`A`， 名称填写`mail`， ipv4地址填写你的服务器ip.
5. 继续添加记录，类型选择`MX`, 名称填写`yourdomain.com`，邮件服务器填写`mail.yourdomain.com`
6. 再添加三个CNAME记录: 名称分别为`smtp`, `pop`, `imap`, 目标则是`mail.yourdomain.com`
7. 再添加txt记录，名称`yourdomain.com`, 目标`"v=spf1 mx ~all"`
8. 再添加txt记录，名称`_dmarc.yourdomain.com`, 目标`"v=DMARC1; p=none; rua=mailto:dmarc-reports@yourdomain.com"` 这里的`dmarc-reports@yourdomain.com`可以换成任意`name@yourdomain.com` 不过记住一会在邮箱服务器中创建对应账号即可。
9. 打开你的npm，如果没有配置过请看之前[文章](使用docker+frp+npm，让旧电脑成为新服务器)，add proxy hosts。domain names填写`mail.yourdomain.com`, forward hostname/IP填写`你的IP`, forward port填写`8808` save。(我在这里把下面的3个选项都勾上了，除此之外我还设置了SSL certificate，这使得我能直接https打开我的mail server但是还是le challenge有问题，所以还是需要底下的解决方案)
10. 打开`mail.yourdomain.com` 按照提示进行配置，点击你的virtual domains，然后点击生成dkim key。根据内容打开你的dns运营商的dns记录，添加txt记录，名称填写内容中类似`_s20160910378._domainkey.yourdomain.com`的部分，目标写入内容中类似`"k=rsa;p=MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEA0FvkMuwN46vvtQCC1JZz7XzRE+l+Lf8/5XUKwWJXOcE7dJoZBbOE0Gz85phZ2q+y4l8D7t/hXDz9q+6/KVQDgJ9muaxSM/uS+KG0ds0QLEiV0GYCVu+ZZQSNPBPjOwlDvo3LraW00lMpd5dUj+xpr07ShfIoULhi7/7t76n5GZMse9yBa4hIhxSG/wCAB4D6IWYBURz9Pc75IDPDTlImr3TP/82YrsULY70CHaPHA1+j1VPA5lE+tnmeqxJW6P537xSutDppv8BZg4nlF3ojg2k6LB/cq15C4QRPAMs77pRA4GVnys1LEJ3JDvV3/csOCZ49oC4m44/TnWXk057OAwIDAQAB"`的部分
11. 现在除了没有配置ssl一切都配置好了

## 使用npm时LE challenge fail 也不能配置ssl的解决方案

[解决方案来自Nginx Proxy Manager Github Issue](https://github.com/NginxProxyManager/nginx-proxy-manager/issues/210#issuecomment-1068955629) 和[官网doc](https://poste.io/doc/faq)

1. 首先请确保你有安装docker, 如果没有可以参考[文章](使用docker+frp+npm，让旧电脑成为新服务器)
2. 如果使用docker-compose进行部署，需要在volume中额外添加well-known的地址。最好使用github issue中提到的解决方案，即创建一个docker volume使得npm和poste io都可以使用.

```sh
# can use this command to creat
sudo docker volume create well-known
```

在创建以后在以下文件中添加(如果不想叫做well-known，请确保下面well-known替换成你的volume name):

```yml
# docker-compose.yml
services:
  mailserver:
    image: analogic/poste.io
    container_name: mailserver
    hostname: mail.yourdomain.com
    ports:
      - "25:25"
      - "110:110"
      - "143:143"
      - "587:587"
      - "993:993"
      - "995:995"
      - "4190:4190"
      - "465:465"
      - "8808:80"
      - "8843:443"
    environment:
      - LETSENCRYPT_EMAIL=admin@yourdomain.com
      - LETSENCRYPT_HOST=mail.yourdomain.com
      - VIRTUAL_HOST=mail.yourdomain.com
      - DISABLE_CLAMAV=TRUE
      - DISABLE_RSPAMD=TRUE
      - HTTPS=OFF
    volumes:
      - ./mail-data:/data
      - well-known:/opt/www/.well-known
    restart: unless-stopped
volumes:
  well-known:
	external: true
```

3. 使用`sudo docker compose restart` 后再去你的mail server点击system settings，点击TLS certificate，带点击change certificate settings. 勾选enabled, common name里写入`mail.yourdomain.com`， alternative names里写入`smtp.yourdomain.com`, `pop.yourdomain.com`,`imap.yourdomain.com` 点击save changes即可

$\in$

## 附录

这里还推荐几个测试网站

1. [MX ToolBox](https://mxtoolbox.com/): 可以检查dmarc，smtp等是否设置正确
2. [mail tester](https://www.mail-tester.com/): test the spammyness of your emails.
