使用vs2015 community update3编绎，在windows上编过去。
1.bootstrap\bootstrap.py 加入依赖advapi32.lib，自己加到脚本中即可。
2.修改build/buildflag.h文件
//#define BUILDFLAG(flag) (BUILDFLAG_CAT(BUILDFLAG_INTERNAL_, flag)())
改为 #define BUILDFLAG(flag) 0
3.将base/win/window_version.cc 中注释掉版本检查
#error VS 2015 Update 3 with Cumulative Servicing Release or higher is required


set WINSDK_DIR =""C:\Program Files (x86)\Windows Kits\10\Include\10.0.10586.0\ucrt
 
如果您不能正常git clone google的官网，请使用gn-standalone.7z

以下命令用来强制更新服务器版本
git rebase -i origin/master



1.cd C:\Program Files (x86)\Microsoft Visual Studio 14.0\VC
2.vcvarsall.bat
3.cd tools\gn\
3.python bootstrap\bootstrap.py -s


以下是参考信息

mkdir gn-standalone
cd gn-standalone
mkdir tools
cd tools
git clone https://chromium.googlesource.com/chromium/src/tools/gn
cd ..
mkdir -p third_party/libevent
cd third_party/libevent
wget --no-check-certificate https://chromium.googlesource.com/chromium/chromium/+archive/master/third_party/libevent.tar.gz
tar -xvzf libevent.tar.gz
cd ../..
git clone https://chromium.googlesource.com/chromium/src/base
git clone https://chromium.googlesource.com/chromium/src/build
mkdir testing
cd testing
git clone https://chromium.googlesource.com/chromium/testing/gtest
cd ..

# Build
windows:
1.install vs2015 update3 ,vs14-kb3165756.exe ,window sdk 10 
2.cd C:\Program Files (x86)\Microsoft Visual Studio 14.0\VC\
3.vcvarsall.bat

cd tools/gn
./bootstrap/bootstrap.py -s

# At this point, the resulting binary is at:
# gn-standalone/out/Release/gn