现在docker hub已经无法连接了，就算是国内镜像基本已经GG了，需要代理一下：
```bash
按照 https://github.com/yxyy/clash-for-linux.git 的代理安装好
```

修改docker代理配置,下面是ubuntu默认位置,如果没有该文件就添加:
```bash
vim /etc/systemd/system/docker.service.d/http-proxy.conf
```
添加下面配置,代理的配置按实际的填写，下面的我本地默认的配置：
```ini
[Service]
Environment="HTTP_PROXY=http://127.0.0.1:7890"
Environment="HTTPS_PROXY=http://127.0.0.1:7890"
Environment="NO_PROXY=localhost,127.0.0.1"

```

最后重启`docker`:
```bash
systemctl daemon-reload
systemctl restart docker
```

验证代理是否配置成功：
```bash
docker info | grep -i proxy
```
输出显示 HTTP Proxy 和 HTTPS Proxy 的相关信息。如果没有，请检查文件路径和内容是否正确。
```
 docker info | grep -i proxy
 HTTP Proxy: http://127.0.0.1:7890
 HTTPS Proxy: http://127.0.0.1:7890
 No Proxy: localhost,127.0.0.1
```