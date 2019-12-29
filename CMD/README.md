## Scp

```bash
$ echo "alias scp='scp -c aes128-ctr'"  >> /root/.bashrc
$ source /root/.bashrc
```

## Ssh

vim /etc/ssh/sshd_config

```
UseDNS no
GSSAPIAuthentication no
```

```bash
$ service sshd restart
```

