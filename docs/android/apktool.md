# Apk反编译
2015-12-12 13:02:30

反编译只是为了学习，研究别人优秀的代码，切忌用于任何商业途径，对版权原作者造成侵权等行为。

## 一、准备工作
* Java环境搭建
* ApkTool下载：[官网](https://ibotpeaches.github.io/Apktool)
    -  进入官网Install页面
    -  进入wrapper script页面，保存页面为`apktool.bat`
    -  进入ApkTool.jar下载页面，下载最新版，完成后并重命名为`apktool.jar`
    -  移动`apktool.bat`和`apktool.jar`到`C://Windows`路径下
    -  打开CMD输入apktool验证  
    ![apk-decompilation](assets/images/gitpages-apktool-devtools.png)
* dex2jar下载：[官网](https://github.com/pxb1988/dex2jar)
* Jd-Gui下载：[官网](http://jd.benow.ca)

## 二、ApkTool反编译
ApkTool主要功能

* Decoding；解码
* Building；编译
* Frameworks
通过ApkTool工具反编译apk应用，可以得到布局，AndroidManifest.xml，项目配置源代码以及图片资源，而原本的java文件被反编译成了smali的文件  

!!! note
    smali文件：可理解为可以运行在java虚拟机上的汇编语言，即这种文件是可以直接运行在davila虚拟机里

反编译过程
CMD中输入：`apktool d < apk文件所在路径 > -o < 反编译到哪个路径 >`  
![apk-cmd](assets/images/gitpages-apktool-cmd.png)
反编译结构如图，其中smali目录下是apk应用java源代码，不过这些是smali文件，可用sublime编辑器打开[`需要安装smali插件`](https://github.com/ShaneWilton/sublime-smali)，如果你懂 smali语言，那么可以直接进行对smali文件修改  
![apk-structure](assets/images/gitpages-apktool-structure.png)

## 三、Jd-Gui反编译
Jd-Gui主要功能

JD-GUI is a standalone graphical utility that displays Java source codes of ".class" files
反编译过程

1. 将apk应用后缀改为zip并解压，得到其中的`classes.dex`
2. 将`classes.dex`复制到`d2j-dex2jar.bat`所在目录`dex2jar`文件夹
3. 在命令行下定位到`dex2jar.bat`所在目录，运行：`d2j-dex2jar.bat classes.dex`命令，生成`classes_dex2jar.jar`文件  
![devtools-dex2jar](assets/images/gitpages-apktool-dex2jar.png)
4. 进入jdgui文件夹双击`jd-gui.exe`，打开上面生成的jar包`classes_dex2jar.jar`，即可看到源代码  
![devtools-jd-gui](assets/images/gitpages-apktool-jdgui.png)

## 注意
经过代码混淆的apk，这种方法无法反编译出源码  
在ApkTool使用过程中，常出现如下错误  

!!! bug
    * Input file was not found or was not readable
    * Destination directory (C:\Users\user) already exists. Use -f switch if you want to overwrite it.
    * Exception in thread "main" brut.androlib.AndrolibException: Could not decode ars c fil...  

解决方法：  
!!! check
    * 1.2问题是因为ApkTool升级到2.0以上时,使用方式已经替换,格式为:`apktool d [-s] -f < apkPath > -o < folderPath >`  
    * 3问题是因为apktool版本过低导致,请升级到最新版本