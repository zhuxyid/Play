**ngrok**
```
什么是ngrok
 假设你有个web项目，想给外面的人访问那该怎么办?
 传统都是利用路由的地址的路由转换实现，假设你没有路由权限，假设你加没有公网ip怎么办？
 这个时候就需要利用ngrok实现。

```

**安装ngrok**
```bash
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
#cp server.key assets/server/tls/snakeoil.key

#GOOS=linux GOARCH=amd64
#make release-server release-client 
```

**可以看到在ngrok/bin下生成ngrok,ngroked执行文件**

ngrok(客户端)   ngrokd(服务端)


**注:这里编译适用于linux.x86-64位的平台，如果使用其他平台可参考如下**
```
GOOS=windows GOARCH=386   #编译windows 32位,如果是64位的那就GOARCH=amd64
GOOS=darwin GOARCH=amd64  #编译MAC OS 64位
GOOS=linux GOARCH=mips    #编译mips平台(小米路由)
参考文章https://golang.org/doc/install/source
```

**启动ngrokd服务**
```
#export $PATH=$PATH:/usr/local/ngrok/bin
#ngrok -domain='zhuxyid.com' -httpAddr=':9999'
#ngrok -domain='zhuxyid.com' -tlsKey=server.key -tlsCrt=server.crt -httpAddr=':9999' -httpsAddr=':9443'
注:httpAddr和httpsAddr是ngrok转发http和https服务
```
