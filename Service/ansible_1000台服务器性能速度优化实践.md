## Environmental
Software：
ansible

host num：
1000+

## Demo

基数为220台，fork设置为50，大概执行时间为20s，1s能发送指令并收集信息的机器是11台

基数为400台，fork设置为100，大概执行时间为34s，1s能发送指令并收集信息的机器是11.7台

1000台服务器Ansible速度CMD测试，200Fork，最终速度稳定在76s，13.15 台/s

[测试视频地址](https://www.bilibili.com/video/av78457543/)

![](https://lijinghua-img.oss-cn-beijing.aliyuncs.com/blog/ansible/iw9xz-ag1nx.gif)

##  Physical aspect

1. 增加server端带宽，减少延迟 ---- 网络
2. 尽量打包发包，用算力换时间  ----- 算力时间权衡
3. 涉及到的目录换为SSD盘  ----- 读写io

## Based on ssh protocol

### Scp_if_ssh

使用scp替代sftp，如果在内网且对安全性要求较高时。ansible默认采用sftp模式传输模块，一般情况下我们保持它不变，除非sftp出问题，我们可以在配置文件中修改为scp模式

sftp是Secure File Transfer Protocol的缩写，安全文件传送协议。可以为传输文件提供一种安全的加密方法。sftp 与 ftp 有着几乎一样的语法和功能。SFTP 为 SSH的一部分，是一种传输档案至 Blogger 伺服器的安全方式。其实在SSH软件包中，已经包含了一个叫作SFTP(Secure File Transfer Protocol)的安全文件传输子系统，SFTP本身没有单独的守护进程，它必须使用sshd守护进程（端口号默认是22）来完成相应的连接操作，所以从某种意义上来说，SFTP并不像一个服务器程序，而更像是一个客户端程序。SFTP同样是使用加密传输认证信息和传输的数据，所以，使用SFTP是非常安全的。但是，由于这种传输方式使用了加密/解密技术，所以传输效率比普通的FTP要低得多，如果您对网络安全性要求更高时，可以使用SFTP代替FTP

`ansible.cfg`

```
[defaults]
···
scp_if_ssh = True
···
```

### SSH PIPElinING

SSH pipelining 是一个加速 Ansible 执行速度的简单方法。ssh pipelining 默认是关闭，之所以默认关闭是为了兼容不同的 sudo 配置，主要是 requiretty 选项。如果不使用 sudo，建议开启。打开此选项可以减少 ansible 执行没有传输时 ssh 在被控机器上执行任务的连接数。不过，如果使用 sudo，必须关闭 requiretty 选项。修改 /etc/ansible/ansible.cfg 文件可以开启 pipelining

`ansible.cfg`

```
[defaults]
···
pipelining = True
···
```

##  Based on ansible Configuration Optimization

### Forks 并发执行主机数量

`ansible.cfg`

```
[defaults]
···
forks = 100
···
```

### 关闭agent检查

`ansible.cfg`

```
[defaults]
···
gather_facts = False
host_key_checking = False    #关闭StrictHostKeyChecking检查,检测主机秘钥
···
```

### 缓存

```
facts_caching_timeout = 86400  #  设置缓存过期时间86400秒,一天
facts_caching = jsonfile              #  cache文件是json格式
facts_caching_connection = /tmp/ansible_facts_cache   #缓存文件的存储路径
```

## Result

`ansible.cfg`

```
[defaults]
deprecation_warnings=False
library        = /usr/share/ansible
remote_tmp     = $HOME/.ansible/tmp
pattern        = *
forks          = 100
poll_interval  = 15
transport      = smart
pipelining = True
# remote_port    = 22
display_failed_stderr = yes
host_key_checking = False
gather_facts = False
log_path = /var/log/ansible.log
ansible_managed = Ansible managed: {file} modified on %Y-%m-%d %H:%M:%S by {uid} on {host}
callback_whitelist = log_plays,timer,oneline
[paramiko_connection]
[ssh_connection]
scp_if_ssh = True
[accelerate]
facts_caching_timeout = 86400  #  设置缓存过期时间86400秒,一天
facts_caching = jsonfile              #  cache文件是json格式
facts_caching_connection = /tmp/ansible_facts_cache   #缓存文件的存储路径
```