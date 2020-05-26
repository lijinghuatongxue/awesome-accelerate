临时生效

```bash
$ pip install -r requirements.txt -i https://pypi.douban.com/simple   #豆瓣源
$ pip install -r requirements.txt -i http://mirrors.aliyun.com/pypi/simple/   #阿里云源
```

永久生效

```bash
$ touch $HOME/.pip/pip.conf ; vim $HOME/.pip/pip.conf 
···
 [global]
 index-url = http://mirrors.aliyun.com/pypi/simple
···
```