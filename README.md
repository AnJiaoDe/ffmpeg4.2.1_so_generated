文章目录

ffmpeg入门教程[https://www.jianshu.com/p/042c7847bd8a](https://www.jianshu.com/p/042c7847bd8a)

视频播放器原理

Windows编译ffmpeg so从下载到安装到坚持再到放弃

Linux编译ffmpeg so从下载坚持到成功

deepin

安装双系统linux（安装deepin）

安装linux虚拟机（安装deepin）

安装VMware Workstation

下载NDK-r14b-linux-x86_64

下载ffmpeg源码4.2.1

温馨提示

安装make

修改configure文件

创建so配置文件

开始编译（成败在此一举）

linux编译ffmpeg 4.2.1 .so深坑

温馨提示

Unknown option "--disable-ffserver"

recipe for target 'libavformat/udp.o' failed

recipe for target 'libavcodec/aaccoder.o' failed

libavcodec/hevc_mvs.c:208:15: error: 'y0000000' undeclared (first use in this function) ((y ## v) >> s->ps.sps->log2_min_pu_size))

其他错误

已经修改过的ffmpeg4.2.1源码，可直接编译，应该不会报错 GitHub:[https://github.com/AnJiaoDe/ffmpeg4.2.1_so](https://github.com/AnJiaoDe/ffmpeg4.2.1_so)

 CSDN下载：[https://download.csdn.net/download/confusing_awakening/11970250](https://download.csdn.net/download/confusing_awakening/11970250)
 
编译好的ffmpeg4.2.1的so库，GitHub:[https://github.com/AnJiaoDe/ffmpeg4.2.1_so_generated](https://github.com/AnJiaoDe/ffmpeg4.2.1_so_generated)

欢迎分享、转载、联系、指正、批评、撕逼

## ffmpeg入门教程[https://www.jianshu.com/p/042c7847bd8a](https://www.jianshu.com/p/042c7847bd8a)

## 视频播放器原理

 ————————————————  版权声明

此处摘抄部分为CSDN博主「雷霄骅」的原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接及本声明。
原文链接：[https://blog.csdn.net/leixiaohua1020/article/details/18893769](https://blog.csdn.net/leixiaohua1020/article/details/18893769)

 视音频技术主要包含以下几点：封装技术，视频压缩编码技术以及音频压缩编码技术。如果考虑到网络传输的话，还包括流媒体协议技术。

 视频播放器播放一个互联网上的视频文件，需要经过以下几个步骤：解协议，解封装，解码视音频，视音频同步。如果播放本地文件则不需要解协议，为以下几个步骤：解封装，解码视音频，视音频同步。他们的过程如图所示。

 
![在这里插入图片描述](https://upload-images.jianshu.io/upload_images/11866078-fed1e08d71ea9d76?imageMogr2/auto-orient/strip%7CimageView2/2/w/500)


**解协议的作用**

就是将流媒体协议的数据，解析为标准的相应的封装格式数据。视音频在网络上传播的时候，常常采用各种流媒体协议，例如HTTP，RTMP，或是MMS等等。这些协议在传输视音频数据的同时，也会传输一些信令数据。这些信令数据包括对播放的控制（播放，暂停，停止），或者对网络状态的描述等。解协议的过程中会去除掉信令数据而只保留视音频数据。例如，采用RTMP协议传输的数据，经过解协议操作后，输出FLV格式的数据。

**解封装的作用**

就是将输入的封装格式的数据，分离成为音频流压缩编码数据和视频流压缩编码数据。封装格式种类很多，例如MP4，MKV，RMVB，TS，FLV，AVI等等，它的作用就是将已经压缩编码的视频数据和音频数据按照一定的格式放到一起。例如，FLV格式的数据，经过解封装操作后，输出H.264编码的视频码流和AAC编码的音频码流。

**解码的作用**

就是将视频/音频压缩编码数据，解码成为非压缩的视频/音频原始数据。音频的压缩编码标准包含AAC，MP3，AC-3等等，视频的压缩编码标准则包含H.264，MPEG2，VC-1等等。解码是整个系统中最重要也是最复杂的一个环节。通过解码，压缩编码的视频数据输出成为非压缩的颜色数据，例如YUV420P，RGB等等；压缩编码的音频数据输出成为非压缩的音频抽样数据，例如PCM数据。

**视音频同步的作用**

就是根据解封装模块处理过程中获取到的参数信息，同步解码出来的视频和音频数据，并将视频音频数据送至系统的显卡和声卡播放出来。

## Windows编译ffmpeg so从下载到安装到坚持再到放弃
这个小编尝试过无数次，死活整不出来。

![1X{OVLAHG{{7}RYY6(YARH2.gif](https://upload-images.jianshu.io/upload_images/11866078-47c9fc0509bfddab.gif?imageMogr2/auto-orient/strip)

劝大家放弃这个方式，即使成功也是得不偿失。

## Linux编译ffmpeg so从下载坚持到成功
既然瘟都思支持不友好，那咱们整个Linux行了吧。
![YCQ_LOII$B%T7}U0P2OLW9B.gif](https://upload-images.jianshu.io/upload_images/11866078-4a01f5f992c4b5a7.gif?imageMogr2/auto-orient/strip)

给大家推荐个好东西：deepin

## deepin
Deepin原名Linux Deepin、deepin os、深度系统、深度操作系统。在2014年4月改名Deepin，2015年4月从deepin 2014.3开始改名为deepin。deepin团队基于Qt/C++（用于前端）和Go（用于后端）开发了的全新深度桌面环境（DDE），以及音乐播放器，视频播放器，软件中心等一系列特色软件。

deepin操作系统是由武汉深之度科技有限公司开发的Linux发行版。deepin操作系统是一个基于 Linux 的操作系统，专注于使用者对日常办公、学习、生活和娱乐的操作体验的极致，适合笔记本、桌面计算机和一体机。它包含了所有您需要的应用程序，网页浏览器、幻灯片演示、文档编辑、电子表格、娱乐、声音和图片处理软件，即时通讯软件等等。deepin 的历史可以追溯到 2004年，其前身 Hiweed Linux 是中国第一个基于 Debian的本地化衍生版，并提供轻量级的可用LiveCD，旨在创造一个全新的简单、易用、美观的 Linux 操作系统。

deepin操作系统拥有自主设计的特色软件：深度软件中心、深度截图、深度音乐播放器和深度影音，全部使用自主的deepinUI，其中有深度桌面环境，deepinTalk（深谈）等。

deepin操作系统是中国最活跃的 Linux 发行版，deepin 为所有人提供稳定、高效的操作系统，强调安全、易用、美观。其口号为“免除新手痛苦，节约老手时间”。在社区的参与下，“让 Linux 更易用”也不断变成可以触摸的现实。

此处转载于百度百科：[https://baike.baidu.com/item/deepin/3432935?fr=aladdin](https://baike.baidu.com/item/deepin/3432935?fr=aladdin)

## 安装双系统linux（安装deepin）
deepin提供的镜像有2种安装方式，1种无需U盘，1种需要U盘，安装过程及其简单。
当然会遇到有些电脑启动时没有deepin选项，这个可以百度下解决方案,小编尝试过，貌似有点麻烦。

**注意：有些镜像必须通过U盘安装，15.6版本的可以不通过U盘安装。**

下载地址：[https://www.deepin.org/](https://www.deepin.org/)

![在这里插入图片描述](https://upload-images.jianshu.io/upload_images/11866078-bbb0c67fe1a28581?imageMogr2/auto-orient/strip%7CimageView2/2/w/500)
往下拉找到15.6版本：

![在这里插入图片描述](https://upload-images.jianshu.io/upload_images/11866078-7308279dd10aee80?imageMogr2/auto-orient/strip%7CimageView2/2/w/500)
选择百度网盘下载即可：

![在这里插入图片描述](https://upload-images.jianshu.io/upload_images/11866078-aeaf05afc5378be1?imageMogr2/auto-orient/strip%7CimageView2/2/w/500)

安装教程：[https://www.jianshu.com/p/e8fd4d03e444](https://www.jianshu.com/p/e8fd4d03e444)
## 安装linux虚拟机（安装deepin）
如果不想安装双系统，觉得切换麻烦的话，可以安装虚拟机，用虚拟机装linux


## 安装VMware Workstation

![在这里插入图片描述](https://upload-images.jianshu.io/upload_images/11866078-c2b07fa4c6883659?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
windows10用WMware安装Linux虚拟机详细步骤:[https://blog.51cto.com/13438667/2059926](https://blog.51cto.com/13438667/2059926)

配置镜像的时候选择deepin镜像即可
## 下载NDK-r14b-linux-x86_64
下载地址：[https://blog.csdn.net/liujian8654562/article/details/81033829](https://blog.csdn.net/liujian8654562/article/details/81033829)

注意：选择NDK-r14b,其他版本容易GG，各种奇怪的报错
[图片上传失败...(image-58d531-1573412376389)]

![在这里插入图片描述](https://upload-images.jianshu.io/upload_images/11866078-13cc344aa52ba31e?imageMogr2/auto-orient/strip%7CimageView2/2/w/500)

## 下载ffmpeg源码4.2.1

[http://ffmpeg.org/download.html](http://ffmpeg.org/download.html)

最新版本：![在这里插入图片描述](https://upload-images.jianshu.io/upload_images/11866078-5e22f733a4123cd2?imageMogr2/auto-orient/strip%7CimageView2/2/w/500)

## 温馨提示
4.0系列的源码编译会疯狂报错，如果你想一下子体验编译成功的快感，建议先下载3.2.14版本编译。

老版本：
![在这里插入图片描述](https://upload-images.jianshu.io/upload_images/11866078-094bacb26d58b479?imageMogr2/auto-orient/strip%7CimageView2/2/w/500)
可如此放置：

![在这里插入图片描述](https://upload-images.jianshu.io/upload_images/11866078-709ba3c61d59c5ad?imageMogr2/auto-orient/strip%7CimageView2/2/w/500)

## 安装make
桌面右击在终端中打开，输入命令 

```c
sudo apt -get install make
```
回车

![在这里插入图片描述](https://upload-images.jianshu.io/upload_images/11866078-150b852e906b6a78?imageMogr2/auto-orient/strip%7CimageView2/2/w/500)


## 修改configure文件
在源码根目录下：

![在这里插入图片描述](https://upload-images.jianshu.io/upload_images/11866078-746cb34d9174f342?imageMogr2/auto-orient/strip%7CimageView2/2/w/500)
双击，显示，找到如下代码

```c
SLIBNAME_WITH_MAJOR='$(SLIBNAME).$(LIBMAJOR)'
LIB_INSTALL_EXTRA_CMD='$$(RANLIB) "$(LIBDIR)/$(LIBNAME)"'
SLIB_INSTALL_NAME='$(SLIBNAME_WITH_VERSION)'
SLIB_INSTALL_LINKS='$(SLIBNAME_WITH_MAJOR) $(SLIBNAME)' 
```
默认编译后的.so文件格式为：文件名+.so+三段版本号的格式比如libavformat.so.57.0.101。这样的文件格式不太符合我们的使用要求，而且即便是将这样的文件名称简单粗暴的删除.so后面的版本号，在实际使用时也无法编译

故修改为如下代码：

```c
SLIBNAME_WITH_MAJOR='$(SLIBNAME).$(LIBMAJOR)'
LIB_INSTALL_EXTRA_CMD='$$(RANLIB) "$(LIBDIR)/$(LIBNAME)"'
SLIB_INSTALL_NAME='$(SLIBNAME_WITH_VERSION)'
SLIB_INSTALL_LINKS='$(SLIBNAME_WITH_MAJOR) $(SLIBNAME)' 
```

## 创建so配置文件
在ffmpeg 根目录下创建build_android.sh(名称随意)：

![在这里插入图片描述](https://upload-images.jianshu.io/upload_images/11866078-104b41a5a0654aeb?imageMogr2/auto-orient/strip%7CimageView2/2/w/500)
填入如下代码：
```c
#!/bin/bash
make clean
export NDK=/media/cy/文件/IT/ffmpeg/android-ndk-r14b
export SYSROOT=$NDK/platforms/android-24/arch-arm/
export TOOLCHAIN=$NDK/toolchains/arm-linux-androideabi-4.9/prebuilt/linux-x86_64
export CPU=arm
export PREFIX=$(pwd)/android/$CPU
export ADDI_CFLAGS="-marm"
./configure --target-os=linux \
--prefix=$PREFIX --arch=arm \
--disable-doc \
--enable-shared \
--disable-static \
--disable-yasm \
--disable-symver \
--enable-gpl \
--disable-ffmpeg \
--disable-ffplay \
--disable-ffprobe \
--disable-doc \
--disable-symver \
--cross-prefix=$TOOLCHAIN/bin/arm-linux-androideabi- \
--enable-cross-compile \
--sysroot=$SYSROOT \
--extra-cflags="-Os -fpic $ADDI_CFLAGS" \
--extra-ldflags="$ADDI_LDFLAGS" \
$ADDITIONAL_CONFIGURE_FLAG
make clean
make
make install
```
**注意**：记得修改NDK路径，否则GG；
还要检查如下路径：
如果路径不存在，也会GG

```c
export NDK=/media/cy/文件/IT/ffmpeg/android-ndk-r14b
export SYSROOT=$NDK/platforms/android-24/arch-arm/
export TOOLCHAIN=$NDK/toolchains/arm-linux-androideabi-4.9/prebuilt/linux-x86_64
--cross-prefix=$TOOLCHAIN/bin/arm-linux-androideabi- \
```
注意不要有空格，否则GG

## 开始编译（成败在此一举）

进入源码根目录，右击在终端打开，输入如下指令,回车：

```c
chmod +x build_android.sh
```
继续输入如下指令，回车
```c
./build_android.sh
```

![在这里插入图片描述](https://upload-images.jianshu.io/upload_images/11866078-c4671752c741338a?imageMogr2/auto-orient/strip%7CimageView2/2/w/500)

如果人品好，那么半小时左右后会看到如下输出：

![在这里插入图片描述](https://upload-images.jianshu.io/upload_images/11866078-96d7a53b474247e9?imageMogr2/auto-orient/strip%7CimageView2/2/w/500)
同时会在源码根目录下生成android/arm文件夹，里面有so库：

![在这里插入图片描述](https://upload-images.jianshu.io/upload_images/11866078-3a464c0fad8cbdc1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/500)

![在这里插入图片描述](https://upload-images.jianshu.io/upload_images/11866078-3adb822dd0589c54?imageMogr2/auto-orient/strip%7CimageView2/2/w/500)
![ON_C4_M{M$A2EP8Z`7EXKFS.gif](https://upload-images.jianshu.io/upload_images/11866078-2e4a4040a0b4f97c.gif?imageMogr2/auto-orient/strip)

## linux编译ffmpeg 4.2.1 .so深坑
然而并没有那么简单，你以为这样就能成功？
![{67{[68)D2_6SBRP]~DEZ)Q.jpg](https://upload-images.jianshu.io/upload_images/11866078-b5ab943e82ab0367.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/500)

## 温馨提示
编译需要很久才会报错，如果不想浪费时间，建议先把如下所有问题都改好再开始编译(当然3.0系列的不需要)
## Unknown option "--disable-ffserver"
输出如下错误：

```c
Unknown option "--disable-ffserver"
```

![在这里插入图片描述](https://upload-images.jianshu.io/upload_images/11866078-cafbf7213c2ae188?imageMogr2/auto-orient/strip%7CimageView2/2/w/500)

**解决方法**：

Unknown option先一律删掉重新编译

## recipe for target 'libavformat/udp.o' failed
输出如下错误：
```c
libavformat/udp.c: In function 'udp_set_multicast_sources':
libavformat/udp.c:290:28: error: request for member 's_addr' in something not a structure or union
         mreqs.imr_multiaddr.s_addr = ((struct sockaddr_in *)addr)->sin_addr.s_addr;
                            ^
libavformat/udp.c:292:32: error: incompatible types when assigning to type '__be32' from type 'struct in_addr'
             mreqs.imr_interface= ((struct sockaddr_in *)local_addr)->sin_addr;
                                ^
libavformat/udp.c:294:32: error: request for member 's_addr' in something not a structure or union
             mreqs.imr_interface.s_addr= INADDR_ANY;
                                ^
libavformat/udp.c:295:29: error: request for member 's_addr' in something not a structure or union
         mreqs.imr_sourceaddr.s_addr = ((struct sockaddr_in *)&sources[i])->sin_addr.s_addr;
                             ^
ffbuild/common.mak:60: recipe for target 'libavformat/udp.o' failed
make: *** [libavformat/udp.o] Error 1
+ make install
CC	libavformat/udp.o

```
![在这里插入图片描述](https://upload-images.jianshu.io/upload_images/11866078-0c62893f8f8d2c22?imageMogr2/auto-orient/strip%7CimageView2/2/w/500)

**解决方法**：

找到libavformat/udp.c:290行，注释如下代码即可

![在这里插入图片描述](https://upload-images.jianshu.io/upload_images/11866078-1b43c0194b5626fa?imageMogr2/auto-orient/strip%7CimageView2/2/w/500)

## recipe for target 'libavcodec/aaccoder.o' failed

  输出如下错误：
```c
libavcodec/aaccoder.c: In function 'search_for_ms': 
libavcodec/aaccoder.c:803:25: error: expected identifier or '(' before numeric constant 
libavcodec/aaccoder.c:865:28: error: lvalue required as left operand of assignment 
libavcodec/aaccoder.c:866:25: error: 'B1' undeclared (first use in this function) 
libavcodec/aaccoder.c:866:25: note: each undeclared identifier is reported only once for each function it appears in 
ffbuild/common.mak:60: recipe for target 'libavcodec/aaccoder.o' failed 
make: *** [libavcodec/aaccoder.o] Error 1
```

![在这里插入图片描述](https://upload-images.jianshu.io/upload_images/11866078-33430c59c2af0989?imageMogr2/auto-orient/strip%7CimageView2/2/w/500)
**解决方法：**

找到libavcodec/aaccoder.c，将定义的B0变量改为b0，注意：使用该变量的地方都要改，小心不要改到其他变量去了。

![在这里插入图片描述](https://upload-images.jianshu.io/upload_images/11866078-6cb8ec7a75a0a43e?imageMogr2/auto-orient/strip%7CimageView2/2/w/500)

## libavcodec/hevc_mvs.c:208:15: error: 'y0000000' undeclared (first use in this function) ((y ## v) >> s->ps.sps->log2_min_pu_size))
输出如下错误：
```c
libavcodec/hevc_mvs.c: In function 'derive_spatial_merge_candidates':
libavcodec/hevc_mvs.c:208:15: error: 'y0000000' undeclared (first use in this function)
             ((y ## v) >> s->ps.sps->log2_min_pu_size))
               ^
libavcodec/hevc_mvs.c:204:14: note: in definition of macro 'TAB_MVF'
     tab_mvf[(y) * min_pu_width + x]
              ^
libavcodec/hevc_mvs.c:274:16: note: in expansion of macro 'TAB_MVF_PU'
     (cand && !(TAB_MVF_PU(v).pred_flag == PF_INTRA))
                ^
libavcodec/hevc_mvs.c:368:23: note: in expansion of macro 'AVAILABLE'
     is_available_b0 = AVAILABLE(cand_up_right, B0) &&
                       ^
libavcodec/hevc_mvs.c:208:15: note: each undeclared identifier is reported only once for each function it appears in
             ((y ## v) >> s->ps.sps->log2_min_pu_size))
               ^
```


![在这里插入图片描述](https://upload-images.jianshu.io/upload_images/11866078-993dd253b36a831b?imageMogr2/auto-orient/strip%7CimageView2/2/w/500)
**解决方法：**

将libavcodec/hevc_mvs.c文件的变量B0改成b0，xB0改成xb0，yB0改成yb0
，小心别改错了，否则GG

![在这里插入图片描述](https://upload-images.jianshu.io/upload_images/11866078-8b84917c9579b264?imageMogr2/auto-orient/strip%7CimageView2/2/w/500)

## 其他错误
其他错误，总有解决办法，百度即可。
![}N8G`S@}SY`FDID}4ACWR$M.gif](https://upload-images.jianshu.io/upload_images/11866078-f96f2de5f130dd65.gif?imageMogr2/auto-orient/strip)



## 已经修改过的ffmpeg4.2.1源码，可直接编译，应该不会报错 GitHub:[https://github.com/AnJiaoDe/ffmpeg4.2.1_so](https://github.com/AnJiaoDe/ffmpeg4.2.1_so)

## CSDN下载：[https://download.csdn.net/download/confusing_awakening/11970250](https://download.csdn.net/download/confusing_awakening/11970250)


如果下载很慢，可以加小编的QQ群，去群里下载

![JB`~O0J_SH{U{VA0U{3%X~I.gif](https://upload-images.jianshu.io/upload_images/11866078-f3a0efd9bfc500f1.gif?imageMogr2/auto-orient/strip)
## 编译好的ffmpeg4.2.1的so库，GitHub:[https://github.com/AnJiaoDe/ffmpeg4.2.1_so_generated](https://github.com/AnJiaoDe/ffmpeg4.2.1_so_generated)


## 欢迎分享、转载、联系、指正、批评、撕逼



Github:[https://github.com/AnJiaoDe](https://github.com/AnJiaoDe)

简书：[https://www.jianshu.com/u/b8159d455c69](https://www.jianshu.com/u/b8159d455c69)

CSDN：[https://blog.csdn.net/confusing_awakening](https://blog.csdn.net/confusing_awakening)

ffmpeg入门教程:[https://www.jianshu.com/p/042c7847bd8a](https://www.jianshu.com/p/042c7847bd8a)

 微信公众号
 ![这里写图片描述](https://upload-images.jianshu.io/upload_images/11866078-91c0fb75e4534af2?imageMogr2/auto-orient/strip%7CimageView2/2/w/500)

QQ群

![这里写图片描述](https://upload-images.jianshu.io/upload_images/11866078-a69dd828697f78a6?imageMogr2/auto-orient/strip%7CimageView2/2/w/500)




