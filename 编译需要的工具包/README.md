# xlog 高性能日志组件
- GitHub地址：https://github.com/Tencent/mars

## iOS xlog 接入步骤

1. git clone  https://github.com/Tencent/mars.git

2.没安装 cmake 需要安装 cmake

3. 检查 python 版本, 必须为 python2 

4. cd /mars-master/mars 文件夹

5.如果项目需要支持 bitcode:
```
mars/build_ios.py
line 15:
DENABLE_BITCODE=0
改为：
DENABLE_BITCODE=1
```

6. 执行 python build_ios.py -> 并选择 2

7.生成framework 路径 mars-master/mars/cmake_build/iOS/Darwin.out/mars.framework

8.将 mars.framework 拉入工程 main.m AppDelegate.m 后缀改成mm


## iOS xlog cocopods 集成 参考：https://www.codenong.com/jsaf0142627f06/


## iOS xlog 解密步骤

1. cd /mars-master/mars/log/crypt

2.执行 python decode_mars_crypt_log_file 沙盒.xlog路径

如果报错：
ImportError: No module named pyelliptic

需要安装 pyelliptic1.5.10 
​​​​​https://github.com/mfranciszkiewicz/pyelliptic/archive/1.5.10.tar.gz#egg=pyelliptic
将 pyelliptic1.5.10 进行解压后，修改pyelliptic-1.5.10/pyelliptic/openssl.py 文件中的内容
```
def find_crypto_lib():
    if sys.platform != 'win32':
       # 注释掉下面路径,写绝对路径
       # return ctypes.util.find_library('crypto')
       return '/usr/lib/libcrypto.dylib'

```

如果还报错
安装如下所需的库：
pip2 install pyelliptic==1.5.7
pip2 install zstd --user
pip2 install zstandard --user

参考： https://www.jianshu.com/p/b863fc0e5d22
参考： https://blog.csdn.net/HanSnowqiang/article/details/121406872
