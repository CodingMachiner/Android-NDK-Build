1、下载NDK文件，解压。
2、将ndk目录添加到环境变量。尝试ndk-build是否可以运行。
3、配置好Android.mk和Application.mk
4、ndk-build ./jni 执行程序。（可以配置生成可执行文件也可以配置生成.so文件）
5、libs目录下存放不同目录的动态库或者可执行文件。



sudo vi /etc/profile
#add path
export ANDROID_NDK_HOME=/home/kali/Desktop/android-ndk-r16b/
export PATH=${PATH}:${ANDROID_NDK_HOME}:${ANDROID_NDK_HOME}/toolchains/arm-linux-androideabi-4.9/prebuilt/linux-x86_64/bin
