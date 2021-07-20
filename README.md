# Summary on Several Technical Subjects
Persisent Memory (NVDIMM) <br />
Chromium OS Test Criteria <br />
Machine Learning <br />
Android Application Development <br />
Nativescript-Vue based Application Development <br />
Face Detection & Recognition <br />

# Reference:
https://www.groundai.com/project/a-fast-face-detection-method-via-convolutional-neural-network/ <br />
http://eyalarubas.com/face-detection-and-recognition.html <br />
https://medium.com/@ageitgey/machine-learning-is-fun-part-4-modern-face-recognition-with-deep-learning-c3cffc121d78 <br />
https://github.com/sagartesla/flops-cnn/blob/master/flops_calculation.py <br />
https://www.zhihu.com/question/65305385 <br />
http://imatge-upc.github.io/telecombcn-2016-dlcv/slides/D2L1-memory.pdf <br />
https://pdfs.semanticscholar.org/64db/333bb1b830f937b47d786921af4a6c2b3233.pdf <br />
https://www.slideshare.net/Eduardyantov/face-recognition-from-scratch-to-hatch <br />

How to train Yolo V3 Tiny : https://chtseng.wordpress.com/2018/09/01/%E5%BB%BA%E7%AB%8B%E8%87%AA%E5%B7%B1%E7%9A%84yolo%E8%BE%A8%E8%AD%98%E6%A8%A1%E5%9E%8B-%E4%BB%A5%E6%9F%91%E6%A9%98%E8%BE%A8%E8%AD%98%E7%82%BA%E4%BE%8B/  <br />

# How to solve building failure involving with pygraphviz
在Ubuntu上直接
sudo apt-get install graphviz graphviz-dev
pip install pygraphviz
使用pygraphviz绘制图像的时候会出现
ImportError: /usr/local/lib/python3.4/dist-packages/pygraphviz/_graphviz.cpython-34m.so: undefined symbol: Agundirected
错误。

下面给出我的解决方法：
pkg-config --libs-only-L libcgraph
pkg-config --cflags-only-I libcgraph
运行完这两句命令后会出现graphviz的路径比如-I/usr/include/graphviz/
先卸载已经安装好的graphviz
pip uninstall pygraphviz
再安装
pip install pygraphviz --install-option="--include-path='/usr/include/graphviz/'" --install-option="--library-path='/usr/lib/graphviz/'"

作者：穆弋
链接：https://www.jianshu.com/p/a3da7ecc5303
來源：简书
简书著作权归作者所有，任何形式的转载都请联系作者获得授权并注明出处。

# How to solve building failrue inside a 32bit and 64bit hybrid codebase
Reference: 
https://stackoverflow.com/questions/847179/multiple-glibc-libraries-on-a-single-host
https://stackoverflow.com/questions/34042873/gcc-specs-file-how-to-get-the-installation-path

最近，我在build一个混有32bit和64bit的代码时，遇到如下问题：
* mmoc执行报错
  通过ldd命令，发现mmoc链接的库文件是64bit的ld-linux.so.2，而不是32bit的ld-linux.so.2，所以导致执行mmoc报出PRIVATRE_LIB的错误，通过在mmoc的Makefile的LDFLAGS加上
  -Wl,--rpath=/path/to/newglibc \
  -Wl,--dynamic-linker=/path/to/newglibc/ld-linux.so.2
The -rpath linker option will make the runtime loader search for libraries in /path/to/newglibc (so you wouldn't have to set LD_LIBRARY_PATH before running it), and the -dynamic-linker option will "bake" path to correct ld-linux.so.2 into the application.
  这样修复了mmoc爆出的错误。
  
# 关于企业IT部署和应用关注点汇总
1.简化企业IT管理和部署
2.数据漫游 & 在不同终端设备之间实现数据同步
3.存储数据加密 & 可信任计算
4.切换设备时等待时间过长 (类似于one driver, 所有数据同时备份在云端)
5.修电脑问题, 远程重装电脑，保留个人设置 (镜像恢复)和个人设置如何保留？
6.企业OS image需要支持尽可能多的不同硬件配置
7.云端、设备端如何智能分配任务，这需要在OS层面实现智能sense

  
# Boot Chain w/ UEFI Bootloader such as GRUB
Reference: 
https://segmentfault.com/a/1190000020850901
https://zhuanlan.zhihu.com/p/28708585

# Fix "Failed to load ldlinux.c32"
Reference: 
https://github.com/kuzoncby/misc-tutorial/blob/master/Troubleshooting-Failed-to-Load-ldlinux.c32.md

# Beginner’s Guide to LVM (Logical Volume Management)
Reference: 
https://www.thegeekdiary.com/redhat-centos-a-beginners-guide-to-lvm-logical-volume-manager/
https://www.2daygeek.com/create-lvm-storage-logical-volume-manager-in-linux/

# Understanding on UEFI for ARM
Reference:
https://www.programmersought.com/article/67683565129/ <br/>
https://rpi4-uefi.dev/ <br/>
