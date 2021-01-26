# Work Trick（持续更新。。。）

## 1、查看文件/文件夹大小

- 查看当前目录的占用总量：`du -sh`
- 查看当前目录下每个文件/文件夹的大小：`du -sh *`

## 2、`ssh`登录`Linux`服务器

- `ssh 用户名@IP`

## 3、`tar`打包

- 打包：`tar -cvf filename.tar filename`

- - 将文件`filename打包成filename.tar`

- 解压：`tar -xvf filename.tar`

- - 解压f`ilename.tar`包

## 4、服务器之间传输文件

- `Python2:`

发送端：`python -m SimpleHTTPServer`

接收端：`wget 发送端IP:8000/Filename`

- `Python3:`

发送端：`python -m http.server`

接收端：`wget 发送端IP:8000/Filename`

## 4、从本地上传/下载文件到服务器

- 使用`scp`命令
  - 从本地上传文件到服务器：`scp local_filename username@ip:/server_path`
  - 把服务器文件拷贝到本机上：`scp username@ip:/server_filename local_path`(应该是拷贝到当前目录下)
  - **备注**：都是在本地执行命令
- 使用`rz、sz`命令（需要给服务器安装`lrzsz`）
  - 上传命令`rz`：输入后命令后会弹出上传框
  - 下载命令`sz`：`sz filename`
  - **备注**：上面两个命令都是在服务器端操作

## 5、上传/更新代码到`GitHub`

- `git init`

- 上传单个文件：`git add FileName`；上传所有文件：`git add .`

- `git remote add origin git@URL `

- `git push -u origin master`

## 6、`split`、`cat`命令分割、合并文件

- 在进行文件传输时，对于超过4G的文件需要进行分割后再进行传输，命令如下：
  - `split -b 2G -d -a 1filename`
  - 合并命令：`cat small_files* > large_file`

## 7、`vim`编辑器设置搜索高亮显示/取消

- 高亮显示：在`~/.vimrc`中添加`set hlsearch`
- 取消高亮：输入`:noh`，回车

## 8、`tmux`使用教程

- 安装：`sudo apt-get install tmux`
- 会话操作
  - 新建会话：`tmux new -s [会话名]`
  - 退出会话：`ctrl+b d`(Windows)、`control +b d`(Mac OS)
  - 查看会话列表：`tmux ls`
  - 进入会话：`tmux a -t [会话名]`
  - 销毁会话：`tmux kill-session -t [会话名]`
- 窗口操作
  - `TODO`

## 9、预训练模型

- `TensorFlow2.0`预训练模型存储位置：`~/.keras/models`
- `Pytorch`预训练模型存储位置：`~`

## 10、`Ubuntu`下解压`rar`文件

- 首先安装`rar`文件：`sudo apt install rar`
- 常用的解压命令：
  - 将文件解压到当前目录：`rar e filr.rar`，包括子目录下的所有文件都被解压到当前目录
  - 带路径解压：`rar x file.rar，保持原有的目录结构`

## 11、`Ubuntu`下解压`7z`文件

- 首先安装`7z`文件：`sudo apt install p7zip`
- 解压命令：`7z x file.7z -o/home…`后面是解压后的文件路径，也可以不带，`-o后面没有空格`

## 12、分割与合并文件

- `Windows/Linux`下分割文件：`split -b 200m filename.zip`(分割后的每个文件大小为200M，文件名命名为`xaa`、`xab`、`xac`)
- 合并文件：
  - `Windows`下：`copy /b xa* filename.zip`
  - `Linux`下：`cat xa* > filename.zip`

## 13、`Ubuntu`查看文件所使用的空间的大小

- 查看当前目录已使用空间大小（G为单位）：`du -h --max-depth=0`
- 查看各个文件占用空间大小（G为单位）：`du -sh *`

## 14、`Linux`统计当前目录下文件和文件夹的数量

- 统计当前目录下文件的个数（包括子目录下面的）
  - `ls -lR | grep "^-" | wc -l`
- 统计当前目录下文件的个数（不包括子目录下的）
  - `ls -l | grep "^-" | wc -l`
- 统计当前目录下文件夹的个数（包括子目录下的）
  - `ls -lR | grep "^d" | wc -l`
- 附：
  - `ls -l`：长列表输出当前目录下文件信息（包括文件夹）
  - `wc -l`：统计输出信息的行数
  - `grep "^-"`：将长列表输出信息过滤一部分，只保留文件，如果只保留目录就是`^d`
  -  `ls -lR`：表示递归到下面的子目录

## 15、卷积输出尺寸计算

- 假设输入特征图尺寸为$W \times W$，卷积核尺寸为$F \times F$，步长为$S$，`padding`的像素数为$P$，那么输出的特征图尺寸为:
$$
W ^ {'} = \frac {W-F+2P}{S}+1
$$

## 16、`TensorFlow2`显存占用问题

- 在使用`TensorFlow2`时，经常会报如下错误：**`Failed to get convolution algorithm. This is probably because cuDNN failed to initialize`**，这是由于`GPU`显存不足造成，根本原因在于`TensorFlow`默认占用所有的`GPU`资源，除了需要指定使用哪块`GPU`，还需要对`GPU`进行按需分配。在程序前添加以下代码：

  ```python
  from tensorflow.compat.v1 import ConfigProto
  from tensorflow.compat.v1 import InteractiveSession
  
  config = ConfigProto()
  config.gpu_options.allow_growth = True
  session = InteractiveSession(config=config)
  ```


## 17、`flask server`

```python
export FLASK_APP=yourapp
export FLASK_ENV=development
# then start the server with:
flask run
```

`windows`下使用`set命令`

## 18、`pip install `拒绝访问错误

在`windows`上安装`tensorflow`时经常碰到如下错误：

`[WinError 5] 拒绝访问。: 'c:\\users\\huyz\\anaconda3\`，可使用以下命令解决：

**`pip install --user tensorflow`**

## 19、`Windows`下使用`make`命令

- 下载`MinGW`，[下载地址](http://sourceforge.net/projects/mingw/files/latest/download?source=files)
- 安装：运行`mingw-get-swtup.exe`，选择默认安装位置，中间需要在线下载文件，全部勾选，点击Apply开始下载安装
- 配置环境变量：将`C:\MinGW\bin`路径添加到系统变量的Path下
- 将`C:\MinGW\bin`路径下的`mingw32-make.exe`重命名为`make.exe`
- 参考：https://blog.csdn.net/yahamatarge/article/details/89380164

## 20、`tensorflow slim`模块弃用问题

在高版本的`tensorflow`中，弃用了`slim`模块，可通过以下方式解决

- 安装`tf_slim`模块
- 调用`import tf_slim as slim`

## 21、拉取`GitHub`更新本地代码

在不同的电脑上进行开发，为了保持各个电脑上代码同步，将代码上传到`github`，在A电脑上开发完毕后将代码上传到`github`，如果需要在B电脑上接着开发，可在B电脑上直接拉取最新的`github`代码来更新B电脑的本地文件，命令如下：

```
git remote -v
git pull
```

## 22 、更新`GitHub`上的代码

```
git remote add origin https://github.com/huyz1117/GoProject.git
git branch -M main
git push -u origin main
```

### 23、`apt-get -f install `

在`Ubuntu`上安装`screen`时出现如下错误：`[E: Unmet dependencies. Try 'apt-get -f install' with no packages (or specify a solution).]`，尝试`sudo apt-get -f install`也不行，应该是安装所有软件都会出现这个问题。

解决方法：`sudo apt-get install --fix-broken install`，执行这个命令又出现`Processing was halted because there were too many errors.Sub-process /usr/bin/dpkg returned an error code (1)`这个错误，解决办法：**`dpkg --configure -a`**（利用`dkpg`包关理工具来修复一些包安装错误），然后再执行**`sudo apt-get install --fix-broken install`**，最后即可成功安装`apt-get -f install screen`