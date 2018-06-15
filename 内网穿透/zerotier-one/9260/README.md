# 动态编译：
1、更改`make-linux.mk`下的CROSS，即交叉编译工具，由于没有找到4.9以后支持`arm-none-linux-gnueabi`的交叉编译器，我使用4.8编译的，但是编译过程中有个地方在检查编译器版本，可以更改下，使其能够使用小于4.9版本的编译器编译，由于需支持`-std=c++11`,所以版本至少需4.7以后<br>
2、然后`make`

# 静态编译zerotier-one：
1、先`make`一次；<br>
2、删除生成的动态zerotier-one；<br>
3、生成静态zerotier-one：`make staticzerotier-one`<br>
# 问题
## 1、terminate called after throwing an instance of '__gnu_cxx::__concurrence_broadcast_error'<br>
在google上搜了一通，找到了解决的方案，在g++的选项中加入：`-Wl,--whole-archive -lpthread -Wl,--no-whole-archive -lc`<br>
[__gnu_cxx::__concurrence_broadcast_error错误解决方法](https://blog.csdn.net/skyflying2012/article/details/22855179)<br>
## 2、zerotier-one join超时,查看本地环路ip是否开启，若未开启执行以下命令
执行`ifconfig lo up`后再join
## 3、每次重启后zerotier-one的mac地址都变了，而且`/var/lib`下的`zerotier-one`文件夹都没了
解决办法：设置好所有东西，确保拥有正确IP地址过后，拷贝一份`/var/lib`下的`zerotier-one`文件夹到其他地方（如根目录下），然后在上电重启后的自启动脚本中加入`cp -r -a /zerotier-one/ /var/lib/`，然后在`zerotier-one -d`
	