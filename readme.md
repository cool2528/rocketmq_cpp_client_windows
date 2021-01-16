## rocketmq-cpp-client-windows

+ 声明

  1、本项目是根据官方client客户端修改版本支持Windows 系统

  源项目地址`https://github.com/apache/rocketmq-client-cpp.git`

  但是官方的例子已经很久没有维护Windows版本的编译环境了 

很多地方无法正常编译 故修改此版本方便编译 
+ 编译环境 
系统：windows10 
MSVS: Visual Studio 2019 版本 16.8.4

+ 依赖第三方库
  1、boost_1.5.8 下载地址https://sourceforge.net/projects/boost/files/boost/1.58.0/
  2、jsoncpp git地址：`git clone https://github.com/jsj020122/jsoncpp-0.10.6.git`
  3、libevent git地址 `https://github.com/libevent/libevent.git`

  libevent 最新版本即可 官方指定的构建版本 不支持 openssl1.1.1 故使用最新的版本即可
  4、openssl 下载编译后的即可使用 下载地址 http://slproweb.com/products/Win32OpenSSL.html

5、zlib 构建boost库的时候需要使用

+ 特别提醒

  boost1.5.8只支持MSVC14.0 也就是vs2015编译工具 所以需要在vs2019 组件中安装msvc2015 14.0的构建工具才能正常构建
+ boost构建方式
1.下载好源码解压到磁盘 使用 `x86 Native Tools Command Prompt for VS 2019` 工具 切换到 boost 源码目录 编译64位的就使用`x64 Native Tools Command Prompt for VS 2019`
2.进入目录以后 执行 `bootstrap.bat` 编译生成 `b2.exe` 构建工具
3.执行如下命令编译
debug 版本
```
b2.exe install --prefix="准备把boost库安装的目录" -sZLIB_INCLUDE="zlib源码根目录" -sZLIB_SOURCE="zlib源码根目录" --build-type=complete link=static variant=debug threading=multi runtime-link=static address-model=32
```
release
```
b2.exe install --prefix="C:\boost_158_x86" -sZLIB_INCLUDE="E:\OpenSourcePaject\zlib-1.2.11" -sZLIB_SOURCE="E:\OpenSourcePaject\zlib-1.2.11" --build-type=complete link=static variant=release threading=multi runtime-link=static address-model=32
```
4、其他库可以自己构建引入也可以使用 我已经构建好的 在项目的`thirdparty`目录中带d的是debug版本 不带d的是release 版本 IDE版本的vs2019 16.8.4版本
+ 执行cmake 构建项目
进入 项目根目录
```
mkdir builds && cd builds
//构建Win32 版本
cmake .. -A Win32 
```
# 本项目只是本人工作中使用时 遇到的问题 解决方案 特此修改希望能帮到有需要的人 本项目默认生成全静态多线程MT静态库 需要其他请自行修改CMakeLists.txt文件

