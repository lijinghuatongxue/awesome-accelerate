# CMD

##Scp

```bash
$ echo "alias scp='scp -c aes128-ctr'"  >> /root/.bashrc
$ source /root/.bashrc
```

## Ssh

to do

# Package download

## Pip

临时生效

```bash
$ pip install -r requirements.txt -i https://pypi.douban.com/simple   #豆瓣源
$ pip install -r requirements.txt -i https://pypi.aliyun.com/simple   #阿里云源
```

永久生效

```bash
$ touch $HOME/.pip/pip.conf ; vim $HOME/.pip/pip.conf 
···
 [global]
 index-url = https://pypi.aliyun.com/simple
···
```

## Docker

https://www.jianshu.com/p/1a4025c5f186

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

## Npm

### cnpm

```bash
$ npm install -g cnpm --registry=https://registry.npm.taobao.org
$ cnpm install package_name
```

### npm 源加速

```bash
$ npm config set registry https://registry.npm.taobao.org
```

#### 验证

```bash
$ npm config get registry
http://registry.npm.taobao.org/
```

#### 临时

```bash
$ npm install package_name --registry https://registry.npm.taobao.org/
```

## Maven

### 阿里云加速

```
$ cd $M2_HOME/conf
$ vim settings.xml
·	· ·
<mirror>
        <id>nexus-aliyun</id>
        <mirrorOf>central</mirrorOf>
        <name>Nexus aliyun</name>
        <url>http://maven.aliyun.com/nexus/content/groups/public</url>
</mirror>
#pom.xlm
<repositories>
        <repository>
            <id>nexus-aliyun</id>
            <name>Nexus aliyun</name>
            <url>http://maven.aliyun.com/nexus/content/groups/public</url>
        </repository>
    </repositories>
·	· ·
```

# Linux System Repositories

## CentOS-Base.repo

### CentOS 5

```bash
$ mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.bak &&  wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-5.repo
```

### CentOS 6

```bash
$ mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.bak &&  wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-6.repo
```

###CentOS 7

```bash
$ mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.bak &&  wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
```

## Ubuntu-source.list

### 16.04

```bash
$ cp /etc/apt/sources.list /etc/apt/sources.list.bak
$ > /etc/apt/sources.list 
$ tee /etc/apt/sources.list  <<-'EOF'
#deb包
deb http://mirrors.aliyun.com/ubuntu/ xenial main restricted universe multiverse  
deb http://mirrors.aliyun.com/ubuntu/ xenial-security main restricted universe multiverse  
deb http://mirrors.aliyun.com/ubuntu/ xenial-updates main restricted universe multiverse  
deb http://mirrors.aliyun.com/ubuntu/ xenial-backports main restricted universe multiverse  
##测试版源  
deb http://mirrors.aliyun.com/ubuntu/ xenial-proposed main restricted universe multiverse  
# 源码  
deb-src http://mirrors.aliyun.com/ubuntu/ xenial main restricted universe multiverse  
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-security main restricted universe multiverse  
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-updates main restricted universe multiverse  
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-backports main restricted universe multiverse  
##测试版源  
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-proposed main restricted universe multiverse  
EOF
```

### 18.04

```bash
$ cp /etc/apt/sources.list /etc/apt/sources.list.bak
$ > /etc/apt/sources.list 
$ tee /etc/apt/sources.list  <<-'EOF'
deb http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse
EOF
```

# Service

需要注意的，软件的速度优化是和业务强绑定的

## Ansible

[Ansible性能提升的总结与1000台服务器实践](https://www.blog.lijinghua.club/article/ansible_faster1)



## to do 1



## to do 2
