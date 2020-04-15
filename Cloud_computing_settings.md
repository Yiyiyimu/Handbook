本来想着配国内的云服务器跑深度学习，应该我碰到的坑大家都碰到过，但中文世界怎么都搜不到相关内容，就还是自己记下来一份碰到的流程和坑，也再好好学学linux

## 放在前面
建议使用AWS EC2, 有tf/keras/pytorch/caffe/nvidia driver安装好的镜像，更重要的是有非常完备的手册，对第一次接触使用云主机来跑深度学习的人来说所有疑问都查得到，这两点都比腾讯阿里好太多了。

加上EC2价格比起来也和阿里差不太多，所以现在看起来还是个不错的选择


## 环境配置
基于Ubuntu18.04
### 安装Anaconda

在 https://repo.continuum.io/archive/ 查看需要的版本

以最新版为例，
```shell
apt-get update #更新所有软件
mkdir tmp
cd tmp  #建立并进入临时文件夹
curl -O https://repo.anaconda.com/archive/Anaconda3-2019.03-Linux-x86_64.sh  #下载文件
bash Anaconda3-2019.03-Linux-x86_64.sh  #安装文件
#一路确认直到加完PATH
source ~/.bashrc #激活安装
conda list #测试是否安装成功
```
然后就直接安需要的包好了

### 安装nvidia driver
```shell
sudo ubuntu-drivers autoinstall
sudo reboot #记得重启
```

### 安装Kaggle API
官方文档：https://github.com/Kaggle/kaggle-api

系统自动创建的.kaggle好像是隐藏的，文件不能直接用WinSCP往文件夹拷，sudo往里拷文件就好

### 解决隔一会儿就connection closed问题
如果用腾讯云自带的界面连接
```shell
vim /etc/ssh/sshd_config

/ClientAlive #搜索这一项
#ClientAliveInterval 0    to    ClientAliveInterval 30
#ClientAliveCountMax 3          ClientAliveCountMax 3
```
让服务器每30s发送一次请求

如果用putty连接，在连接界面的左右connection栏有Sending of null packets to keep session active，设置成30就好
（这个AWS在配置的时候就有讲，腾讯阿里就啥都没说）

### 解决每次断开连接的时候python程序也停止运行的问题
真的是很恼火的问题，卡了我一天多花了好多钱。。。提交工单上去倒是三五分钟就有回复，但。。还是很不新手友好的

不过最后还是找到原因了,连接远程服务器都是用的ssh
> ssh打开以后，bash等都是他的子程序，一旦ssh关闭，系统将所有相关进程杀掉，所以一旦ssh关闭，执行中的任务就取消了。
所以要用screen来守护进程，ubuntu应该是自带了，直接输入screen看有没有出现界面，如果没有就apt-get install screen就好

使用方法很简单
```shell
screen [command] #打开一个screen并执行命令
screen -ls #显示当前screen列表
screen -r 16582 #输入显示的数字就可以继续啦
```
详情可以看[这里](https://blog.csdn.net/wind19/article/details/4986458)
