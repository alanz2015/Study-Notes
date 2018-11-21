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
