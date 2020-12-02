## 深澜SURN 网页认证 食用方式：
+ 网页认证绕过检测相对简单，只需在路由器伪造MAC并更改所有包的ttl值即可
> 大体实现方式：
> + 使用openwrt作为路由器系统
> + 修改WAN口的MAC地址
> + 通过自定义iptables规则修改ttl值

+ 具体实现方法：（不知什么是OpenWrt的请移步至
>+ 在接口设置页面，进入WAN接口设置-物理设置，取消勾选桥接改接口
>+ WAN 接口类型选择DHCP（根据你的需要选
>+ 将接口分配至vlan交换机（在下面选
>+ 进入LAN口设置，勾选为指定接口创建桥接，并分配至与WAN口不同的交换机
>+ 使用自定义iptables：
```
iptables -t mangle -A PREROUTING -i eth0.2 -j TTL --ttl-set 64 //修改 WAN 口 TTL 值
iptables -t mangle -A PREROUTING -i br-lan -j TTL --ttl-set 64 //修改 LAN 口 TTL 值
```
至此，大部分工作已经完成，
下面你需要连接好路由和主机，并在路由下的任意一台主机上进行认证，认证后该路由下所有设备均可上网。
