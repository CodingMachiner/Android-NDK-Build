gcc编译
参考链接：https://www.jianshu.com/p/5cbddbdac211
1、下载NDK文件，解压。
2、将ndk目录添加到环境变量。尝试ndk-build是否可以运行。
3、配置好Android.mk和Application.mk
4、ndk-build ./jni 执行程序。（可以配置生成可执行文件也可以配置生成.so文件）
5、libs目录下存放不同目录的动态库或者可执行文件。



sudo vi /etc/profile
#add path
export ANDROID_NDK_HOME=/home/kali/Desktop/android-ndk-r16b/
export PATH=${PATH}:${ANDROID_NDK_HOME}:${ANDROID_NDK_HOME}/toolchains/arm-linux-androideabi-4.9/prebuilt/linux-x86_64/bin


gdb调试
参考链接：https://my.oschina.net/u/2424583/blog/739840
1.1、Application.mk中增加
APP_OPTIM := debug

1.2、编译增加DEBUG选项
$ndk-build NDK_DEBUG=1




使用NDK编译的可执行程序的调试步骤整理

1、编译调试版本

1.1、Application.mk中增加
APP_OPTIM := debug

1.2、编译增加DEBUG选项
$ndk-build NDK_DEBUG=1
$ndk-build NDK_PROJECT_PATH=.  NDK_APPLICATION_MK=./Application.mk APP_BUILD_SCRIPT=./Android.mk
2、将生成目录下的gdbserver拷贝到手机上

#拷贝gdbserver
$adb push libs/armeabi-v7a/gdbserver /data/local/tmp

#给权限
$adb shell "chmod 777 /data/local/tmp/gdbserver"

#拷贝可执行程序
$adb push libs/armeabi-v7a/expolit /data/local/tmp

#分配权限
$adb shell "chmod 777 /data/local/tmp/expolit"
3、手机终端启动gdbserver

3.1、
$adb shell
$cd /data/local/tmp
#启动gdbserver,端口号1234,expolit为要启动的可执行文件
$./gdbserver :1234 expolit

3.2、转发端口
$adb forward tcp:1234 tcp:1234


4、主机端连接调试

#切换到jni的上层目录
$cd {jni-dir}

#连接gdb
$D:\android-ndk-r10e\android-ndk-r10e\toolchains\arm-linux-androideabi-4.9\prebuilt\windows-x86_64\bin\arm-linux-androideabi-gdb.exe

#设置符号路径
(gdb)set solib-search-path obj/local/armeabi-v7a
#强制加载带符号的可执行文件 
(gdb)file obj/local/armeabi-v7a/expolit
#连接远程gdb服务
(gdb)target remote :1234
(gdb) bt
#0  init_payloads () at jni/exploit.c:95
#1  0xb6fe557c in main (argc=1, argv=0xbeac5aa4, env=0xbeac5aac) at jni/exploit.c:294
