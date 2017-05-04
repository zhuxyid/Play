**System:CentOS,Debian,Ubuntu

**Memory:>=128M

**System configure

```
server port:default(8989)
client port:default(1080)
setting passwd:default(zhuxyid.com)
setting Method:default(aes-256-cfb)
other setting default
```

**Install

```
#wget --no-check-certificate -O shadowsocks.sh https://github.com/zhuxyid/Play/blob/master/ssserver/shadowsocks.sh
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
}       #single port

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
}       #multiple port


```

**Use command

```
/etc/init.d/shadowsocks {start|stop|restart|status}
```


**client shadowsock

download url:https://github.com/shadowsocks/shadowsocks-windows/releases/download/4.0.1/Shadowsocks-4.0.1.zip

input server ip

input port

input method
