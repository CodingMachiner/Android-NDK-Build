1������NDK�ļ�����ѹ��
2����ndkĿ¼��ӵ���������������ndk-build�Ƿ�������С�
3�����ú�Android.mk��Application.mk
4��ndk-build ./jni ִ�г��򡣣������������ɿ�ִ���ļ�Ҳ������������.so�ļ���
5��libsĿ¼�´�Ų�ͬĿ¼�Ķ�̬����߿�ִ���ļ���



sudo vi /etc/profile
#add path
export ANDROID_NDK_HOME=/home/kali/Desktop/android-ndk-r16b/
export PATH=${PATH}:${ANDROID_NDK_HOME}:${ANDROID_NDK_HOME}/toolchains/arm-linux-androideabi-4.9/prebuilt/linux-x86_64/bin
