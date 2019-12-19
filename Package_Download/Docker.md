适用于绝大多数发行版

```bash
$ sudo mkdir -p /etc/docker
$ sudo tee /etc/docker/daemon.json <<-'EOF'
{
    "registry-mirrors": [
        "https://1nj0zren.mirror.aliyuncs.com",
        "https://docker.mirrors.ustc.edu.cn",
        "http://f1361db2.m.daocloud.io",
        "https://registry.docker-cn.com"
    ]
}
EOF
$ sudo systemctl daemon-reload
$ sudo systemctl restart docker
```

| **镜像加速器**                                               | **镜像加速器地址**                      | **获取渠道**     |
| ------------------------------------------------------------ | --------------------------------------- | ---------------- |
| [Docker 中国官方镜像](https://docker-cn.com/registry-mirror) | https://registry.docker-cn.com          | 公开             |
| [DaoCloud 镜像站](https://daocloud.io/mirror)                | http://<your_code>.m.daocloud.io        | 需要注册登陆获取 |
| [Azure 中国镜像](https://github.com/Azure/container-service-for-azure-china/blob/master/aks/README.md#22-container-registry-proxy) | https://dockerhub.azk8s.cn              | 公开             |
| [科大镜像站](https://mirrors.ustc.edu.cn/help/dockerhub.html) | https://docker.mirrors.ustc.edu.cn      | 公开             |
| [阿里云](https://cr.console.aliyun.com/)                     | https://<your_code>.mirror.aliyuncs.com | 需要注册登陆获取 |
| [七牛云](https://kirk-enterprise.github.io/hub-docs/#/user-guide/mirror) | https://reg-mirror.qiniu.com            | 公开             |
| [网易云](https://c.163yun.com/hub)                           | https://hub-mirror.c.163.com            | 公开             |
| [腾讯云](https://cloud.tencent.com/document/product/457/9113) | https://mirror.ccs.tencentyun.com       | 公开             |
| ···                                                          | ···                                     | ···              |

验证

```bash
$ docker info
···
Registry Mirrors:
 https://<your _code>.mirror.aliyuncs.com/
···
```