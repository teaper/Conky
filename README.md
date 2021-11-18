![封面](https://raw.githubusercontent.com/9527tech/conkyrc/master/screenshot.png)
  
### 系统环境  
* 系统：ArchLinux  
* 桌面：GNOME  
* 核心：4  
* 线程：4  
  
### 安装 Conky  
这项目是 Conky 的主题包，所以需要先安装 Conky-lua  
```bash
yay -S conky-lua
```
然后会出现多个包，这里就说三个
* `aur/conky-nvidia 1.11.3-1 (+123 0.27%)` 支持 Nvidia 的 conky 包  
* `aur/conky-lua 1.11.3-1 (+50 0.71%)` 支持 Lua 的 conky 包  
* `aur/conky-lua-nv 1.11.3-2 (+118 0.87%)` 支持 Lua 和 Nvidia 的 conky 包  

这里选择 `aur/conky-lua 1.11.3-1 (+50 0.71%)` 这个，输入它的编号回车，输入 `y` 回车  
安装成功之后再安装 `conky-manager` 管理器  
```bash
sudo pacman -S conky-manager
```
再开始菜单中运行 `conky-manager` ，使用以下命令刷新字体缓存
```bash
fc-cache -vf
```

### 使用该主题  
克隆本项目到 `.Conky` 隐藏文件夹，本主题文件在 [deviantart](https://www.deviantart.com/trollpunny/art/Conky-Rings-Revamped-591137228) 也可以下载到  
```bash
git clone git@github.com:teaper/Conky.git ~/.Conky
cd ~/.Conky #进入文件夹
sh startconky.sh #运行启动脚本
```

### 修改模块
可以修改对应的模块代码文件，例如时钟
```bash
vim clock #编辑clock文件
```
把 `own_window yes` 改成 `own_window no` 即可关闭时间
模块的具体参数可以根据[参考文档](http://conky.sourceforge.net/docs.html)配置

### 网络和存储模块
运行之后，如果 `NETWORK` 和 `DISK` 模块无效果，需要分别指定你自己的网卡和硬盘
```bash
-----------network文件----------
Down:$alignr${downspeed wlp2s0}/s   #wlp2s0就是我的网卡，不知道网卡名字可以使用ifconfig查看
Up:$alignr${upspeed wlp2s0}/s
${downspeedgraph wlp2s0 324D23 77B753}  #324D23 77B753 是颜色渐变改成 51A8DD 7DB9DE

${upspeedgraph wlp2s0 324D23 77B753}
```
```bash
-----------disk文件----------
Read:$alignr${diskio_read /dev/sda}/s  #sda是我固态盘(不是分区)，不知道名字使用lsblk查看
Write:$alignr${diskio_write /dev/sda}/s
${diskiograph_read /dev/sda 324D23 77B753} 

${diskiograph_write /dev/sda 324D23 77B753}
```

### 开机自启
```bash
sudo gedit ~/.config/autostart/conky.desktop    #创建自启快捷方式
```
内容如下
```bash
[Desktop Entry]
Type=Application
Name=conky
Exec=/home/teaper/.Conky/startconky.sh --daemonize --pause=5
StartupNotify=false
Terminal=false
```


