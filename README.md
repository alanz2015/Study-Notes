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
最近，我在build一个混有32bit和64bit的代码时，遇到如下问题：
* mmoc执行报错
  通过ldd命令，发现mmoc链接的库文件是64bit的ld-linux.so.2，而不是32bit的ld-linux.so.2，所以导致执行mmoc报出PRIVATRE_LIB的错误，通过在mmoc的Makefile的LDFLAGS加上
  -Wl,--rpath=/path/to/newglibc \
  -Wl,--dynamic-linker=/path/to/newglibc/ld-linux.so.2
The -rpath linker option will make the runtime loader search for libraries in /path/to/newglibc (so you wouldn't have to set LD_LIBRARY_PATH before running it), and the -dynamic-linker option will "bake" path to correct ld-linux.so.2 into the application.
  这样修复了mmoc爆出的错误。
  
