**1、该工具是小米的ss客户端程序，需要有个ss服务端，ss服务端是国外的vps才可以翻过GFW。**

**2、小米路由系统版本必须是开发版，而且必须开启ssh功能。**

**3、ssh到小米路由器后直接执行**

```bash
cd /tmp && rm -rf *.sh
wget https://github.com/zhuxyid/play/blob/master/xiaomi-ss/miwifi.sh
chmod +x miwifi.sh
sh ./miwifi.sh
rm -rf *.s
```

即可完成安装

** 配置文件说明
```bash
#more /etc/shadowsocks.json
{
  "server":"${serverip}",         #国外vps ip
  "server_port":${serverport},    #国外vps port
  "local_address":"127.0.0.1",    #本地回环口不需要修改
  "local_port":1081,              #本地端口不需要修改
  "password":"${shadowsockspwd}", #国外shadowsockspwd密码
  "timeout":600,                  #超时时间
  "method":"${method}"            #加密方法
}
```
