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