由于一些不可抗力因素，现在`docker hub`已经无法连接了，就算是使用国内镜像源也基本`GG`了，需要代理一下：
代理设置有两种方式：
1. 直接设置`Docker`的守护进程配置：
2. 通过`systemd`配置环境变量，影响`Docker`守护进程的网络行为

**注意**：确保系统本身已经支持代理。如果尚未配置，可以使用以下方法安装代理工具（适用于 Linux）：
```bash
git clone https://github.com/yxyy/clash-for-linux.git 
```

#### 方法一：直接设置`docker`的守护进程配置：
```bash
vim /etc/docker/daemon.json
```
如果没有该文件就添加 ，添加`proxies`配置：
```json
{
  "proxies": {
    "default": {
      "httpProxy": "http://127.0.0.1:7890",
      "httpsProxy": "http://127.0.0.1:7890",
      "noProxy": "localhost,127.0.0.1"
    }
  }
}

```

#### 方法二：通过 systemd 设置代理环境变量

修改systemd的docker代理配置,下面是ubuntu默认位置,如果没有该文件就添加:
```bash
vim /etc/systemd/system/docker.service.d/http-proxy.conf
```
添加下面配置：
```ini
[Service]
Environment="HTTP_PROXY=http://127.0.0.1:7890"
Environment="HTTPS_PROXY=http://127.0.0.1:7890"
Environment="NO_PROXY=localhost,127.0.0.1"

```

哪种方式最后都需要重启`docker`:
```bash
systemctl daemon-reload
systemctl restart docker
```

验证代理是否配置成功：
```bash
docker info | grep -i proxy
```
输出显示 HTTP Proxy 和 HTTPS Proxy 的相关信息。

```
 docker info | grep -i proxy
 HTTP Proxy: http://127.0.0.1:7890
 HTTPS Proxy: http://127.0.0.1:7890
 No Proxy: localhost,127.0.0.1
```

如果没有，请检查文件路径和内容是否正确。