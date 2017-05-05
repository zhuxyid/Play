**小米路由3新版不支持opkg命令,需要ssh到路由下载opkg

```
#wget https://github.com/zhuxyid/Play/raw/master/xiaomi-opkg/opkg -P /data
```

**添加环境变量

```
#more /etc/profile
export PATH=/bin:/sbin:/usr/bin:/usr/sbin:/data
#source /etc/profile
```


**添加小米opkg源

```
#more /etc/opkg.conf
src/gz attitude_adjustment_base http://downloads.openwrt.org/barrier_breaker/14.07/ramips/mt7620a/packages/base
src/gz attitude_adjustment_packages http://downloads.openwrt.org/barrier_breaker/14.07/ramips/mt7620a/packages/packages/
src/gz attitude_adjustment_luci http://downloads.openwrt.org/barrier_breaker/14.07/ramips/mt7620a/packages/luci/
src/gz attitude_adjustment_management http://downloads.openwrt.org/barrier_breaker/14.07/ramips/mt7620a/packages/management/
src/gz attitude_adjustment_oldpackages
http://downloads.openwrt.org/barrier_breaker/14.07/ramips/mt7620a/packages/oldpackages/   
src/gz attitude_adjustment_routing http://downloads.openwrt.org/barrier_breaker/14.07/ramips/mt7620a/packages/routing/
src/gz openwrt_dist http://openwrt-dist.sourceforge.net/releases/ramips/packages
dest root /data    #默认安装目录
dest ram /tmp      #opkg临时目录
lists_dir ext /data/var/opkg-lists  #索引文件
option overlay_root /data
arch all 100
arch ramips 200
arch ramips_24kec 300                                                                                                            
```

**更新opkg源

```
#opkg update
```
