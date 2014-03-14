# 如何在Windows 7平台搭建Android Cocos2d-x3.0开发环境

**注意：** 因为cocos2d-x 3.x引擎不需要安装cygwin即可编译Android样本程序，欲了解更多信息可参见本贴。

在Windows 7平台搭建Android Cocos2D-x开发环境不难，但因为框架更新频繁，许多用户在使用过程中还是会遇到很多问题。希望本指南对用户有好处。

**建议：**为避免安全相关问题，所有操作请在管理员身份下进行，在运行命令时，请确保以管理员身份打开控制台（console）。      
本指南将介绍如何在Windows 7平台搭建cocos2d-x Android开发环境。本指南操作要求一台搭载Windows 7平台及安装Visual Studio 2010的电脑。最好拥有快速稳定的网络，因为在指南操作中需要下载许多软件包。


搭建开发环境需要安装工具包括

- Visual Studio 2012/2013 ——— 因为cocos2d-x-v3.x引擎不能用老版本的VS编译，所以我们需要下载安装Visual Studio 2012或2013。VS的安装简单，本教程不做讲解。
- cocos2d-x ———本教程以cocos2d-x 3.beta2版本为例，下载地址：[https://code.google.com/p/cocos2d-x/downloads/list](https://code.google.com/p/cocos2d-x/downloads/list)
- JAVA JDK
- Android SDK


## 下载cocos2d-x 3.0引擎

**注意：**目前最新版本的引擎为cocos2d-x 3.beta2。     
用户可以登陆[cocos2d-x](http://www.cocos2d-x.org/) 官方网站下载最新版的cocos2d-x。点击导航栏的“Download”（下载）后你会看到如下下载页面：

![](./res/download.jpg)

在本指南中，将会以cocos2d-x 3.beta2为例。
（注意：如果你想要下载旧版的cocos2d-x，可点击“looking for an old versoin?”链接。但本人强烈推荐使用最新版本的cocos2d-x，新版引擎有很多新功能，修复了旧版的很多问题。）

右键单击“Download”链接选择“save link as…”（将链接保存为…），然后将压缩文件保存至适当的位置。本机保存位置为 D:\Cocos2d-x\cocos2d-x 3.beta2。    
  
（更新：请不要将cocos2d-x文件夹放置c:\下，因为会导致很多优先级别（privilege）相关的问题。可尝试将该文件夹放到其他盘如D:\及E:\等等。）

打开 “D:\Cocos2d-x\cocos2d-x 3.beta2\build”目录，如下所示：           
![](./cocos2dxdirectory.jpg)
看到上图红色划线部分了吗？双击这个名为“cocos2d-win32.vs2012.sln”的文件，然后会自动启动Visual Studio 2012。
现在你便可以将HelloCpp项目当作默认启动项目来编译，按CTRL-F5运行样本程序。如果编译没有什么错误，同时运行成功的话，你会看到如下画面。

![](./res/hello.jpg)

祝贺你！你已成功在Windows 7平台中运行cocos2d-x引擎。接下里介绍如何配置Android开发环境。


### 安装java jdk
因为我们是针对Android开发，所以我们需要安装的第一个软件包绝对是JDK。如果你用的是64位的Windows 7，那应该下载以下版本软件64 bit JDK for windows 64bit，下载地址：[http://www.oracle.com/technetwork/java/javase/downloads/index.html](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 。    

![](./res/jdk_download.jpg)


下载完成之后，双击exe文件安装JDK，注意最好不要将其安装在有空格或者中文文件夹下，其他无限制，注意记下其安装路径，本机安装路径为：D:\Program Files\Java\jdk1.7.0_51\

配置环境变量：

新建环境变量：JAVA_HOME 值为：D:\Program Files\Java\jdk1.7.0     
新建环境变量：CLASSPATH  值为：.;%JAVA_HOME%\lib;（注意：点号表示当前目录，不能省略）    
在系统变量Path的值的前面加入以下内容：%JAVA_HOME%\bin;(注意:这里的分号不能省略)到这里，JDK安装完毕。     

单击“开始”—>“运行”—>输入：cmd命令，在CMD窗口中输入：java -version  
出现如下界面，就表示安装成功：

![](./res/cmd_java.jpg)


### 配置Android SDK环境

点击进入[http://developer.android.com/sdk/index.html](http://developer.android.com/sdk/index.html)页面，下载ADT包，它能帮你快速开始开发应用程序。它包括了必要的Android SDK组件和一个内置ADT(Android开发者工具)的Eclipse IDE版本，简化了Android应用程序开发。

![](./res/SDK.jpg)

下载Android SDK下载之后解压，并将其放置于你要放置的目录下，在..\adt-bundle-windows-x86_64-20131030\eclipse文件夹中会有一个eclipse.exe程序，本机在桌面上创建了该程序的快捷方式。

现在用户可以双击桌面的快捷方式启动Eclipse，同时会出现一个即时对话框，要求设置默认工作区（workspace）。选择“OK”接受默认设置即可。

在导入样本Android项目之前，需要设置一个名为“ANDROID_SDK”新的环境变量，将其值设为：D:\TDDownload\android\adt-bundle-windows-x86_64-20131030\sdk\platforms\;D:\TDDownload\android\adt-bundle-windows-x86_64-20131030\sdk\tools\;D:\TDDownload\android\adt-bundle-windows-x86_64-20131030\sdk\platform-tools（这个是SDK存放的位置）。

在系统PATH环境变量种加入：%ANDROID_SDK%

单击“开始”—>“运行”—>输入：cmd命令，在CMD窗口中输入：`adb -h` 检验是否安装成功。
![](./res/adb.png)

### 安装NDK
安装完Android SDK之后，还要安装“Android NDK”软件包，用户可前往http://developer.android.com/tools/sdk/ndk/index.html下载。下载完成之后，解压，并将其放置到相应路径，本机路径为 D:\android-ndk-r9，设置另一个名为“NDK_ROOT”同时指向存放路径的环境变量。

Android NDK包含build、docs、samples、sources、GNUmakefile、ndk-build、ndk-gdb及readme等内容。


将刚才下载的压缩包解压到你指定的文件夹里。         
进入到目录**cocos2d-x-3.0beta2/tools/project-creator**   
     
打开终端运行**create_project.py**脚本创建文件

此版本项目创建脚本支持图形界面方式创建项目，执行以上脚本后会出现图形界面:

![](./res/create1.jpg)

填写项目名称，包名称以及项目路径后选择开发语言，即可点击**create**开始创建项目:

![](./res/create2.jpg)

**注:**包名一定要写成cocos2dx

##生成Android项目文件

执行**test/proj.android**下的*build_native.py*脚本进行编译

![build](res/build.jpg)

编译成功！


## 导入Android项目
最后便可启动Eclipse然后导入cocos2d-x文件夹中的样本Android项目。操作步骤如下：

- 右键点击“Package Explorer”并选择“Import…”
- 当出现对话框时，选择“Exsiting Android project into workspace”（将现有Android项目导入工作区）。

![](./res/importandroid.jpg)

![](./res/import.jpg)

![](./res/improt1.jpg)

按照上面的方法导入到Eclipse里面。将您的手机设置成调试模式并用USB线连接到电脑, 在Eclipse中运行HelloWorld, 然后就能在手机上看到已经运行的HelloWorld了！