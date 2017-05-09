**ngrok**
```
什么是ngrok
 假设你有个web项目，想给外面的人访问那该怎么办?
 通常都是利用DNAT实现，假设你是个屌丝php，在公司既没有路由权限，在家也没有公网ip怎么办？
 这个时候就需要利用ngrok实现。
 当然你的需要一个vps最好是国外的(香港的也行)不需要备案
```

**安装ngrok**
```
系统版本:CentOS7.x86_64
git版本 1.8
golang版本 1.6
安装所依赖的包
#yum -y install zlib-devel openssl-devel perl hg cpio expat-devel gettext-devel curl curl-devel perl-ExtUtils-MakeMaker hg wget gcc gcc-c++
#yum -y git golang

下载ngrok
#wget https://github.com/zhuxyid/Play/raw/master/ngrok/ngrok.tar.gz -P /usr/local/
#cd /usr/local/
#tar zxvf ngrok.tar.gz &&rm ngrok.tar.gz && cd ngrok
#openssl genrsa -out rootCA.key 2048
#openssl req -x509 -new -nodes -key rootCA.key -subj "/CN=zhuxyid.com" -days 36500 -out rootCA.pem
#openssl genrsa -out server.key 2048
#openssl req -new -key server.key -subj "/CN=zhuxyid.com" -out server.csr
#openssl x509 -req -in server.csr -CA rootCA.pem -CAkey rootCA.key -CAcreateserial -out server.crt -days 36500
#cp rootCA.pem assets/client/tls/ngrokroot.crt
#cp server.crt assets/server/tls/snakeoil.crt
#cp server.key assets/server/tls/snakeoil.key            #上面的都是生成域名证书，通常是微信接口使用
#GOOS=linux GOARCH=amd64 make release-server release-client 
```

**可以看到在ngrok/bin下生成ngrok,ngroked执行文件**
```
ngrok (客户端)
ngrokd(服务端)
```


**注:这里编译适用于linux.x86-64位的平台，如果使用其他平台可参考如下**
```
GOOS=windows GOARCH=386 make release-client  #编译windows 32位,如果是64位的那就GOARCH=amd64
GOOS=darwin GOARCH=amd64 make release-client #编译MAC OS 64位
GOOS=linux GOARCH=mips make release-client   #编译mips平台(小米路由)
GOOS=linux GOARCH=arm make release-client    #编译arm平台(如树莓派)
如果不确定平台可以用go env查看，前提需要装go环境
参考文章https://golang.org/doc/install/source
```

**启动ngrokd服务**
```
#export $PATH=$PATH:/usr/local/ngrok/bin
#ngrok -domain='zhuxyid.com' -httpAddr=':9999'
#ngrok -domain='zhuxyid.com' -tlsKey=server.key -tlsCrt=server.crt -httpAddr=':9999' -httpsAddr=':9443'
注:httpAddr和httpsAddr是ngrok转发http和https服务

ngrok默认启动的端口4443
```

**测试是否正常**

访问:http://zhuxyid.com:9999  #前提需要将域名@记录执行vps的ip
如果出现Tunnel zhuxyid.com:9999 not found那就说明正常


**客户端配置**
```
#vi /etc/ngrok.cfg
server_addr: "zhuxyid.com:4443"              #这个端口是服务端的默认建立通道的端口
trust_host_root_certs: false
```

**客户端启动**
```
#ngrok -config=ngrok.cfg -subdomain=www 80    #将本地的80端口于服务器的9999端口绑定

如果有多个应用可以直接写在配置文件中
#vi /etc/ngrok.cfg
server_addr: "zhuxyid.com:4443"
trust_host_root_certs: false
tunnels:
    http:
        subdomain: "www"     #二级域
        auth: "user:123"     #开启身份验证
        proto:               #本地端口
            http: "80"
    ssh:
        proto:
            tcp: "22"
    tomcat.zhuxyid.com:      #绑定域名
        proto:
            http: "8080"
#ngrok -config=ngrok.cfg start http ssh tomcat.zhuxyid.com  #可以启动配置文件中三个隧道服务
#ngrok -config=ngrok.cfg start ssh   #也可以单个启动
```
