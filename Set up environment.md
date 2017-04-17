最近给电脑装了块GTX 1080，打算重装系统，然后把开发环境重新配置一边，在这里记录一下，方便以后参考。
# 1 需要安装的东西
## 1.1 开发环境
1. GTX 1080的驱动
2. CUDA
3. Anaconda
4. Tensorflow, TensorLayer
5. IDE: Pycharm, Spyder, Sublime Text
6. Jupyter Notebook
7. 其他常用库： Scikit-Learn, Pandas, Matplotlib, Seaborn
7. Jupyter
## 1.2 其他
1. [Google Chrome浏览器](http://www.cnblogs.com/Michelle-Yang/p/6660331.html)
2. [XX-Net](https://github.com/XX-net/XX-Net/wiki/%E4%B8%AD%E6%96%87%E6%96%87%E6%A1%A3)
# 2 步骤
## 2.1 显卡驱动和CUDA
参考:
[ubuntu 16.04 + GTX 1080 DeepLearning工作站搭建 ](http://blog.csdn.net/Loser__Wang/article/details/52457830?locationNum=12)

[深度学习主机环境配置: Ubuntu16.04+Nvidia GTX 1080+CUDA8.0](http://www.52nlp.cn/%E6%B7%B1%E5%BA%A6%E5%AD%A6%E4%B9%A0%E4%B8%BB%E6%9C%BA%E7%8E%AF%E5%A2%83%E9%85%8D%E7%BD%AE-ubuntu-16-04-nvidia-gtx-1080-cuda-8)

[亲测详解ubuntu14.04+cuda8.0+gtx1080+caffe ](http://blog.csdn.net/i_better/article/details/52812825)

1. 下载GTX 1080最新驱动，
2. 下载CUDA 8.0
3. 此时显示器接在集成显卡的插口上
4. CTRL+ALT+F1 然后登陆你的账号
5. 关闭 X server，sudo service lightdm stop
6. sudo init 3
7. sudu sh NVIDIA-Linux-x86_64-375.39.run
8. 重启，显示器插到显卡上，正常输入密码登录帐号进入图形界面
9. Ctrl + Alt + T 打开Terminal
10. sudo sh cuda_8.0.61_375.26_linux.run
11. 注意刚才已经装过驱动了，这里要选择不安装CUDA带的驱动
12. 安装依赖:
> sudo apt-get install freeglut3-dev build-essential libx11-dev libxmu-dev libxi-dev libgl1-mesa-glx libglu1-mesa libglu1-mesa-dev
12. 安装完毕后，再声明一下环境变量, 在终端输入这两句：

>export PATH=/usr/local/cuda-8.0/bin:$PATH

>export LD_LIBRARY_PATH=/usr/local/cuda-8.0/lib64:$LD_LIBRARY_PATH

13. 然后修改文件中环境变量设置

>sudo vi /etc/profile

14. 输入上面export的两句，保存，退出。

15. sudo ldconfig //环境变量立即生效

16. 通过nvcc -V测试cuda是否安装成功
## 2.2 安装cuDNN
参考：
[深度学习主机环境配置: Ubuntu16.04+GeForce GTX 1080+TensorFlow](http://www.52nlp.cn/%e6%b7%b1%e5%ba%a6%e5%ad%a6%e4%b9%a0%e4%b8%bb%e6%9c%ba%e7%8e%af%e5%a2%83%e9%85%8d%e7%bd%ae-ubuntu16-04-geforce-gtx1080-tensorflow)

1. 下载[cuDNN](https://developer.nvidia.com/rdp/cudnn-download)
2. 安装cuDNN比较简单，解压后把相应的文件拷贝到对应的CUDA目录下即可：

>tar -zxvf cudnn-8.0-linux-x64-v5.1.tgz

>sudo cp cuda/include/cudnn.h /usr/local/cuda-8.0/include/

>sudo cp cuda/lib64/libcudnn* /usr/local/cuda-8.0/lib64/

>sudo chmod a+r /usr/local/cuda-8.0/include/cudnn.h

>sudo chmod a+r /usr/local/cuda-8.0/lib64/libcudnn*

## 2.3 安装Anaconda
1. 在Anaconda官网下载并安装
>bash Anaconda3-4.3.1-Linux-x86_64.sh 
2. 添加[清华大学镜像](https://mirror.tuna.tsinghua.edu.cn/help/anaconda/)
>conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/

>conda config --set show_channel_urls yes

## 2.4安装Tensorflow
参考：
[Tensorflow Install](https://www.tensorflow.org/install/install_linux)
1. 创建一个子环境，命名为dl
>conda create -n dl python=3.6
2. 激活环境dl
>source activate dl
3. 安装libcupti-dev library
>sudo apt-get install libcupti-dev
3. 使用pip安装tensorflow
>pip3 install tensorflow-gpu
