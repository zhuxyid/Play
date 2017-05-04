**系统支持CentOS{6,7},Debian,Ubuntu
**内存:>=128M

**服务器配置

```
server port:default(8989)
client port:default(1080)
setting passwd:default(zhuxyid.com)
setting Method:default(aes-256-cfb)
other setting default
```

**Install

```
#wget --no-check-certificate -O shadowsocks.sh https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks.sh
chmod +x shadowsocks.sh
./shadowsocks.sh 2>&1 | tee shadowsocks.log
```

**Uninstall

```
#./shadowsocks.sh uninstall
```

**Config file
```
#cat /etc/shadowsock.json
{
    "server":"0.0.0.0",
    "server_port":8989,
    "local_address":"127.0.0.1",
    "local_port":1080,
    "password":"yourpassword",
    "timeout":600,
    "method":"aes-256-cfb",
    "fast_open": false
}       #单端口配置

{
    "server":"0.0.0.0",
    "local_address":"127.0.0.1",
    "local_port":1080,
    "port_password":{
         "8989":"password",
         "8990":"password",
         "8991":"password",
         "8992":"password",
         "8993":"password"
    },
    "timeout":600,
    "method":"aes-256-cfb",
    "fast_open": false
}       #多端口配置


```

**Use command

```
/etc/init.d/shadowsocks {start|stop|restart|status}
```
