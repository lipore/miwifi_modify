# init.d脚本以及作用

- acsd
对应程序 /usr/sbin/supervisord 
用于进程管理

- ad_filter
对应程序 /usr/sbin/ad_filter.sh 
字面意思是广告过滤，ad_filter.sh 会通过ad_filter_client从网上拉去一个列表，阻止用户访问，其中有广告网站 也有一些xiaomi不想让你访问的网站
该服务依赖rule_mgr

- rule_mgr
不知道是干嘛的，貌似有很多用途。从配置上看security_center,cache_center,content_filter_center,tencent_center,ad_filter_center 都会依赖它

- messagingagent
路由器向小米服务器报告的服务，注重隐私的必须关闭，关闭后远程配置，远程浏览路由器硬盘都不可用，启动后会有一条tcp连接到 42.62.48.195:1888

- xunlei
迅雷下载用的，启动时会有一个进程etm 与不知名服务器相连，感觉不安全。

- sysapihttpd
ngnix服务器，主要提供配置界面。兼职做http劫持后的跳转地址，个别监听端口会重定向到api.xiaomi.com。建议修改配置/etc/sysapihttpd/sysapihttpd.conf 
	- 80 配置，插件接口
	- 5081 无论什么地址都返回一个路由器状态
	- 8192 重定向到baidu或者tencent 提示恶意网站
	- 8193 http_proxy
	- 8194 pre_load
	- 8195 ad_filter
	- 8196 
	- 8197
	- 8191 /error-page 跳到api.xiaomi.com/rr/e...
	- 8190 /跳到api.xiaomi.com/rr/e...
	- 8188 /跳到api.xiaomi.com/rr/e... error_type 不同
	- .....