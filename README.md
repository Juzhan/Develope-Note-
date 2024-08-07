由于ROS版本限制所以只能使用的ubuntu14.4下的一些记录

### 第一步 右键命令行
```
sudo apt-get install nautilus-open-terminal
```
安装这个，然后就可以文件夹右键打开命令行了

### 远程服务器文件夹
文件夹里面的 `Network` 的 `Connect to Server`

格式比如：`sftp://172.31.233.78/home/juzhan`

### vscode远程写代码 (时代变了，直接官方remote插件)
1. 安装插件 `Remote Workspace`
2. 写个配置文件，后缀名 `.code-workspace`
3. 格式如下：
```
{
    "folders": [{
        "uri": "sftp://my-user:my-password@my_server.example.com:my_folder_path",
        "name": "Whatever"
    }]
}
```
4. `File` -> `Open Workspace` 打开这 `code-workspace` 文件就可以了

### git最新版本
```
sudo add-apt-repository ppa:git-core/ppa
sudo apt-get install git
```

### pip安装最新
```
curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py 
sudo python get-pip.py
```

### pip 的阿里源
在 `~/.pip/pip.conf`
```
[global]
index-url = http://mirrors.aliyun.com/pypi/simple/                          
[install]
trusted-host=mirrors.aliyun.com
```

### conda的清华源
> https://mirrors.tuna.tsinghua.edu.cn/help/anaconda/

在`~/.condarc`
```
channels:
  - defaults
show_channel_urls: true
default_channels:
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/r
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/msys2
custom_channels:
  conda-forge: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  msys2: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  bioconda: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  menpo: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  pytorch: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  pytorch-lts: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  simpleitk: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  deepmodeling: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/
```

### ubuntu的清华源
> https://mirrors.tuna.tsinghua.edu.cn/help/ubuntu/

### python 2.7 对应的ipython最高版
一般是 `ipython 5.x.x`，比如： `sudo pip install ipython==5.3.0`

### ubuntu的字体
`sudo apt-get install ttf-wqy-microhei  #文泉驿-微米黑`

### ubuntu美化
> https://blog.csdn.net/ghty520/article/details/79524623

### 截图与录制视频
`sudo apt-get install kazam`

### 安全更新cmake到3.0以上版本
> https://blog.csdn.net/love1055259415/article/details/79875113
> 
> https://zhuanlan.zhihu.com/p/93480024
>

> https://askubuntu.com/questions/829310/how-to-upgrade-cmake-in-ubuntu

```
In the new version of cmake (ex: 3.9.6), to install, download tar file from https://cmake.org/download/. Extract the downloaded tar file and then:

cd $CMAKE_DOWNLOAD_PATH
./configure
make
sudo make install
```

> 完美的一句：`sudo pip install --upgrade cmake==3.13.2`

### pytorch的cuda8.0，python2.7安装
```
sudo pip install http://download.pytorch.org/whl/cu80/torch-0.4.1-cp27-cp27mu-linux_x86_64.whl
or > pip install http://download.pytorch.org/whl/cu80/torch-0.1.12.post2-cp27-none-linux_x86_64.whl
```
### blender 2.79的python
> 是系统内自带的python 3.6，所以安装第三方库和pip都是python3.6上进行的

### gazebo的坑
> 自定义模型的mesh路径必须是 file:// 开头，model:// 开头的是默认路径
> 
> gazebo似乎会对默认路径下的模型几何体有初始化到缓存什么的，创建后有碰撞体积
> 
> 但是自己导入的模型如果也是model://开头，就没有碰撞体积了

### OpenEXR 安装问题（为了在blender里面安装bpycv遇见的）[2021.05.03更新：好像官方用了新的方法安装bpycv，更简单了]

+ 情况一：没有“Python.h”，参考bpycv的链接。
+ 情况二：没有“pyconfig.h”，找现有的python环境里面，include文件夹下复制一份。
+ 情况三：没有“ImathBox.h”，得自己手动安装openexrpython，前往这里，找到对应的版本下载https://www.lfd.uci.edu/~gohlke/pythonlibs/

### E-pick
> http://wiki.ros.org/robotiq
> 
> https://github.com/ros-industrial/robotiq
>
> https://github.com/ros-industrial/robotiq/pull/175/files

### Failed to connect to github.com port 443
```
git config --global --unset http.proxy
```

### yntax error near unexpected token `$'\r''
> https://blog.csdn.net/xzm5708796/article/details/88344074

1. sed -i 's/\r//g' javaInstall.sh

2. 其实呢是没有把shell脚本转换成Unix，还有一种解决办法：vim xxxx.sh 输入 : set ff=unix 然后回车保存返回 :wq 再执行sh xxxx.sh即可

### clone fail
`github.com.cnpmjs.org`

### ubuntu18 python3.7 下的python-pcl

代价是与ros冲突
> https://github.com/strawlab/python-pcl/issues/317

### unbuntu20 docker 安装unityhub

> https://github.com/danchitnis/container-xrdp/issues/4

主要问题是安装的时候没有chrome-sandbox，然后基于chrome的一系列软件，在xface里面开不了

比如要执行 google-chrome，必须后面加上 google-chrome --no-sandbox，vscode那些应该也一样。

unityhub也一样，不过它也可以修改文件来设置为默认的，就是安装后到 /opt/unityhub，里面有个unityhub文件，打开文件后，最后那个==0修改为：

```
$UNPRIVILEGED_USERNS_ENABLED == 1
```

这样改完就可以不用输入 --no-sandbox 了

记得把chrome卸载了，别影响后面启动的时候找默认浏览器。现在继续执行还有个报错，就是没有 va_getDriverName() 啥的，这个是缺了 nvidia_drv_video.so，

```
sudo apt install vdpau-va-driver # nvidia
sudo apt install vainfo

vim ~/.bashrc
export LIBVA_DRIVER_NAME=nvidia
export LIBVA_DRIVERS_PATH=/usr/lib/x86_64-linux-gnu/dri
```
这下应该就能正常跑unityhub了。

### Kinect DK

> https://blog.csdn.net/zxxxiazai/article/details/108152376
