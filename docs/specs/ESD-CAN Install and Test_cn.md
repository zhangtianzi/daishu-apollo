## 方法一 编译带ESD-CAN的Apollo-RT-Kernel
该方法是将原生的Linux内核（linux-4.4.32）打上esdcan的补丁(esdcan_patch),然后使用apollo提供的build.sh 脚本编译成实时内核。下面具体介绍操作步骤。

### 下载apollo-kernel,命令如下：
```
git clone https://github.com/ApolloAuto/apollo-kernel.git
```
### 内核文件准备工作
- 下载Linux内核
点击该链接即可下载：
[Linux Kernel 4.4.32](https://www.kernel.org/pub/linux/kernel/v4.x/linux-4.4.32.tar.gz)

    ```
    tar zxvf linux-4.4.32.tar.gz
    ```
    将解压后目录下的所有文件copy到 apollo-kernel/linux路径下。你会发现在linux/drivers/路径中没有esdcan的目录。所有的内核驱动都是在其根目录drivers下的，esdcan驱动不是linux支持的，因此没有其源代码。
- 打esdcan的补丁
    在 ~/apollo-kernel/linux/patches路径下，将文件esdcan.patch复制到linux目录中。

    在linux目录下，执行如下命令进行打补丁操作：
    ```
    patch -p1 < esdcan.patch
    ```
    此时查看./drivers/路径 ，发现esdcan目录已经存在。
- 根据你选用的ESD-CAN卡型号，在附赠光盘中选取对应的驱动，解压，将 src/路径下除Makefile之外的所有文件copy到  ~/apollo-kernel/linux/drivers/esdcan/ 路径下。命令为：
    ```
    cd ~/apollo-kernel/linux/drivers/esdcan/
    cp -ri ./src/* .  #请将源路径替换成自己驱动src目录所在的路径
    ```
- 执行如下命令
    ```
    cd drivers/esdcan/;ln -s Makefile.esd Makefile;ln -s Kconfig.esd Kconfig;cd ../..  #如果链接不成功，删掉 Makefile或 Kconfig重新进行进行即可
    ```
### 编译
成功执行完上述操作，你当前的路径应该是 
    ```
        ~/apollo-kernel/linux/$
    ```
 在该路径下执行apollo官方提供的脚本进行编译：
```
./build.sh rt #rt参数表示只编译实时（RT）内核，其他参数参数请用"./build help"查看，或者直接打开该脚本一饱眼福，哈哈
```
 编译整个内核啊，这是一个漫长的过程，在我新嘎嘎的 Nuvo-6108GGC E3-1275-V5 八核处理器上，编译了半个多小时呢。编译刚开始时，你可以看看前面输出的信息，说是编译的RT内核，ESD-CAN支持  ，blablabla...... 蓦然回首，一个编译好的鲜活生动的内核已经出炉！你可以在
    ```
        ~/apollo-kernel/linux/install/rt/    
    ```路径下看到install.tgz文件，这就是内核安装包。解压，执行install路径下的脚本进行安装。如果你多看一眼，你会发现还有一个装N卡驱动的脚本，在本人的机器上，亲测可用。
    
### 内核默认启动选项修改
至此，带有ESD-CAN支持的apollo-rt-kernel的编译安装工作已经结束。但是你reboot会发现，启动的还是之前的内核。此时，你需要在grub.cfg中修改默认启动内核选项啦，具体做法，不会的请自行
    ```
        百度一下。
    ```

## 方法二 Build & Install Out-of-Tree ESD Kernel Driver
这个比较快，操作也简单，请参考[apollo官方文档](https://github.com/ApolloAuto/apollo-kernel/blob/master/linux/ESDCAN-README.md)
    ```
        方法一
    ```
操作那么复杂，存在意义是什么呢，我简单唠叨两句：

- 编译好的内核，你可以保存下来，以后直接安装就行(ESD-CAN的型号一致的话)。
- 艺多不压身啊，有些时候你不得不编译内核


## ESD-CAN调试
折腾这么久，你肯定想看看这个CAN能不能正常工作喽 ，等我调试好立即更新。

**ATTENTION**: 入行不深，疏漏难免，欢迎批评&&指正，不胜感激！

**References**:[1] [https://github.com/ApolloAuto/apollo-kernel/blob/master/linux/ESDCAN-README.md](https://github.com/ApolloAuto/apollo-kernel/blob/master/linux/ESDCAN-README.md)
[2][https://github.com/ApolloAuto/apollo-kernel](https://github.com/ApolloAuto/apollo-kernel)
