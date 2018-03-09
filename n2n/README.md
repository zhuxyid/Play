## n2n

**用途**

目前联通、移动、电信三家运营商家庭宽带都是私有ip,并不能在互联网上直接使用，如果想实现访问家里路由可以跟电信申请固定ip或者买个花生棒www.oray.com

**n2n原理图**
```
               ┌─────┐        ┌─────┐                   
               │edge │        │edge │                   
          ┌───▶│node │        │node │                   
          │    └──▲──┘        └──▲──┘                   
          │       │              │                      
          │       │              │                      
┌─────┐   │    ┌──▼──┐        ┌──▼──┐            ┌─────┐
│edge ├───┘    │super│        │super│            │edge │
│node │◀ ─ ─ ─▶┤node ├◀──────▶│node │◀ ─ ─ ─ ─ ─▶│node │
│     │        │     │    ┌──▶┤     ◀───┐        └─────┘
└─────┴◀───┐   └─────┘    │   └─────┘   │               
           │              │             │               
           │              │             │               
           │    ┌─────┐   │             │     ┌─────┐   
           └────▶edge ◀───┘             │     │edge │   
                │node │                 └────▶│node │   
                └─────┘                       └─────┘  

```


**说明**

supernode是中心节点(作用是对两个edge节点进行连接)
edge是边缘节点
由此可以看出supernode需在n2n服务器上部署，edge是在客户端运行

**vps中部署n2n的supernode节点(部署步骤很简单)**
```
#yum install make wget gcc gcc-c++ openssl openssl-devel
#wget https://github.com/zhuxyid/Play/raw/master/n2n/n2n_v2.tar.gz -P /opt
#cd /opt && tar zxvf n2n_v2.tar.gz &&cd n2n_v2 && make &&make install
#\cp supernode /usr/sbin/
#\cp edge /usr/sbin/
```

**vps启动supernode**

```
supernode -l 9001 -v        #9001是开放给边缘节点的端口
```

**客户端启动边缘节点edge(客户端也需要装n2n,只是不需要启动supernode节点)**

```
#edge -d n2n0 -c zhuxyn2n -k encryptme -a 172.16.10.1 -l VPSIP:9001
参数说明：
  -d  指定网卡名称
  -c  指定edge的名称
  -k  指定密码
  -a  指定ip
  -l  指定superedge的ip和端口
```


**小米安装n2n(需要opkg安装,前提支持opkg命令)**

```
#opkg install n2n

启动:
#edge -d n2n0 -c zhuxyn2n -k encryptme -a 172.16.10.3 -l VPSIP:9001
```

**mac安装n2n**

```
$wget https://github.com/zhuxyid/Play/raw/master/n2n/n2n_v2.tar.gz
$tar zxvf n2n_v2.tar.gz
$cd n2n_v2
$wget https://raw.githubusercontent.com/zhuxyid/Play/master/n2n/n2n_v2_osx_fix.diff
$patch < ~/n2n_v2/n2n_v2_osx_fix.diff #macos需打个补丁,不然make不过
$make
```

**windows安装n2n**

```
下载n2n的GUI程序
下载地址:https://github.com/zhuxyid/Play/raw/master/n2n/N2N-GUI.exe
直接安装使用
```


**QA**
CentOS7上可能启动n2n客户端发现网卡down状态
需要安装net-tools工具

