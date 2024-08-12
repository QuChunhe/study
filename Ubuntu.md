
apt Advanced Package Tool
* apt update ：更新包缓存（可以知道包的哪些版本可以被安装或升级）
* apt upgrade ：升级包到最新版本
* apt autoclean 删除已从软件源中删除的软件包的旧版本

https://www.sysgeek.cn/

speed-up-ubuntu-linux-top-10/

https://mirrors.tuna.tsinghua.edu.cn/ubuntu-releases/22.04.2/

用户名
vboxuser


```
dpkg -i ***.deb 

sudo apt-get install ntfs-3g //读取win硬盘

```



https://wiki.archlinux.org/title/Display_Power_Management_Signaling

```
xset -q
xset s 600

```

```shell
sudo apt install build-essential cmake software-properties-common g++ gcc
```


```shell
sudo apt install linux-tools-common linux-tools-generic 
```


```
.\VBoxManage.exe modifymedium  --resize 81920 "D:\VirtualBox\Ubuntu22.04.4\Ubuntu22.04.4.vdi"

apt install gparted
gparted


lvdisplay
lvextend -l +100%FREE /dev/mapper/ubuntu--vg-ubuntu--lv
resize2fs /dev/mapper/ubuntu--vg-ubuntu--lv

```


在 Windows 11 中，启用或禁用休眠模式最简单的方法是通过「控制面板」中的电源选项菜单，步骤如下：
1. 按下Windows + R快捷键打开「运行」对话框，执行control打开「控制面板」。
2. 选择「硬件和声音」>「电源选项」>「选择电源按钮的功能」。
3. (可选）如果以下选项是灰色，请点击「更改当前不可用的设置」。
4. 在「关机设置」中勾选或取消「休眠」选项，然后点击「保存更改」。

无论属于哪种原因，你都可以通过命令快速启用 Windows 11 休眠模式，并重建休眠文件：
1. 右键点击「开始」菜单，选择「终端管理员」，以管理员权限打开 Windows Terminal。
2. 在「命令提示符」或 Windows PowerShell 交互窗口中，执行以下命令启用休眠模式
```
powercfg /hibernate on
powercfg /h /type full
powercfg -h off
```