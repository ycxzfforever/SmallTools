# 动态编译：
	更改make-linux.mk下的CROSS，及交叉编译工具
	然后make

# 静态编译zerotier-one：
	1、先make一次；
	2、删除生成的动态zerotier-one；
	3、生成静态zerotier-one：make staticzerotier-one
# 问题
	1、missing port and zerotier-one.port not found in /var/lib/zerotier-one
	执行： zerotier-one -d
	2、ERROR: unable to configure virtual network port: could not open TUN/TAP device: No such file or directory
	重新编译内核，在内核中选中：
	Device Drivers => Network device support => Universal TUN/TAP device driver support
	3、ERROR: unable to add ip address fc36:3cf2:8a3f:8e84:f4ce:0000:0000:0001/40
	重新编译内核，在内核中选中：
	Networking support -> Networking options -> The IPv6 protocol（下面尽量全选）