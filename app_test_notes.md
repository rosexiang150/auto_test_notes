##  01.移动端测试知识概览

### 01.1 移动端测试是什么？

移动端测试是指对移动应用进行的测试，即实体的特性满足需求的程度。

### 01.2 移动端测试分类？

- app功能测试
  - 业务逻辑正确性测试
    - 文档
  - 兼容性测试
    - 系统版本
    - 分辨率
    - 网络情况
  - 异常测试
    - 热启动应用
    - 网络切换&中断恢复
    - 电话&信息中断恢复
  - 升级&安装卸载测试
  - 健壮性测试
    - 手机资源消耗
    - 流量消耗
    - 崩溃恢复等测试
- app自动化测试
  - 通过场景和数据的预设，把以人为驱动的测试行为转化为机器执行的一种过程，并不是所有功能都能进行自动化。
- app安全测试
  - 通过安全测试技术，保证app尽可能的不存在安全漏洞.

### 01.3 市场招聘如何？

互联网移动场景下业务的爆发，导致移动端开发和测试人员需求量增大，市场很缺移动端的人才。

公司待遇：

1. app功能测试，一般1-3年的功能测试人员月薪8k-15k
2. app自动化测试，一般1-3年的自动化测试月薪13k-25k


真机也是可以测试的:在手机里打开USB调试选项,模拟器怎么操作,真机就怎么操作.

安卓手机--设置---关于手机--版本号 双击,直到弹出toast'您现在处于开发者模式'---点击返回---会多出一个'开发者选项',点击---调试里的USB调试,打开----然后用appium作调试

定位手机上一个点的坐标:

继续上面的操作-----往下滑至输入----指针位置,打开----屏幕最上方就出现坐标值

xiang

JRE:     java的最简单的运行环境

JDK:    java的SDK的缩写,

SDK:    开发环境,是系统准备的文档+文件+示例代码.是一套包.

API:   系统准备好的文件



## 02.移动端测试环境搭建

我们的目标是Android测试，所以环境需要搭建三个，Java，AndroidSDK，Android模拟器。

为什么要安装这三个环境，我们倒着来说：

Android模拟器：实际上就是一台手机，方便我们给大家展示效果。

AndroidSDK：Android SDK给你提供开发测试所必须的Android API类库。

Java：Android的底层是c、c++，应用层用的语言是Java所以需要使用Java环境。

### 02.1 Java环境

#### windows

安装JDK1.8

```
运行jdk-8u151-windows-x64.exe文件，默认安装即可(例如我的安装目录：C:\Program Files\Java\jdk1.8.0)
```

配置java环境变量(Windowns7为例)

```
1.进入我的电脑 -> 属性 -> 高级系统设置 -> 环境变量

2.在系统变量下点击新建 -> 变量名: JAVA_HOME -> 变量值: C:\Program Files\Java\jdk1.8.0 -> 点击确定按钮

3.在系统变量下点击新建 -> 变量名: CLASSPATH -> 变量值: .;%JAVA_HOME%\lib;%JAVA_HOME%\lib\tools.jar(***变量值最前面有一个".") -> 点击确定按钮

4.在系统变量下找到系统的path变量，进入在最后添加：;%JAVA_HOME%\bin;%JAVA_HOME%\jre\bin(最前面是一个分号，如果path变量最后已有分号，可不用添加) -> 点击确定按钮
```

验证环境变量

```
1.win+r 或者 开始 -> 搜索框输入cmd

2.在界面运行java -version

3.出现版本即可
```

#### macOS

安装JDK

```
安装 jdk-8u151-macosx-x64.dmg
```

配置环境变量

```
1.进入命令行， vim ~/.bash_profile 
2.# set jdk1.8
JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk1.8.0_151.jdk/Contents/Home
CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
PATH=$PATH:$JAVA_HOME/bin
export JAVA_HOME CLASSPATH
export PATH
```

验证

```
1.打开终端

2.在界面运行java -version

3.出现版本即可
```

### 02.2 AndroidSDK环境

#### windows

将SDK保存到硬盘

```
Android SDK文件夹解压到任意目录(记住这个目录的位置，目录不要有中文)
```

配置环境变量

```
1.进入我的电脑 -> 属性 -> 高级系统设置 -> 环境变量

2.在系统变量下点击新建 -> 变量名: ANDROID_HOME -> 变量值: D:\android-sdk -> 点击确定按钮

3.在系统变量下找到系统的path变量，最后添加：;%ANDROID_HOME%\platform-tools;%ANDROID_HOME%\tools;(最前面是一个分号，如果path变量最后已有分号，可不用添加) -> 点击确定按钮
```

验证环境变量

```
重启命令行工具，命令行输入adb，不报错即可
```

#### macOS

将SDK保存到硬盘

```
Android SDK文件夹解压到任意目录(记住这个目录的位置，目录不要有中文)
```

配置环境变量

```
1.进入命令行， vim ~/.bash_profile
2.# set android
ANDROID_HOME=电脑存放的路径/android-sdk-macosx

PATH=$PATH:$ANDROID_HOME/tools:$ANDROID_HOME/platform-tools

export ANDROID_HOME 
export PATH
```

验证环境变量

```
重启命令行工具，命令行输入adb，不报错即可
```

#### 可能出现的问题

- 尽量不要手写
- 注意分号
- 配置好以后，cmd需要重启再输入adb
- 选择androidSDK的目录，不是jdk的目录

#### 补充：下载其他版本SDK

1.win或mac的命令行中输入android

2.因国外下载较慢，所以需要配置国内镜像

**windows**

```
在弹出的Android SDk Manager页面，点击Tools ，下拉框点击Options...
```

![Snip20180122_6](移动端测试_image/Snip20180122_7.png)

![Snip20180122_6](移动端测试_image/Snip20180122_8.png)

**mac**

```
点击Android SDk Manager，点击preferences
```

![Snip20180122_6](移动端测试_image/Snip20180122_6.png)

```
镜像地址列表(也可以网上查找最新的)：

	中国科学院开源协会镜像站地址:

		IPV4/IPV6: mirrors.opencas.cn 端口：80

		IPV4/IPV6: mirrors.opencas.org 端口：80

		IPV4/IPV6: mirrors.opencas.ac.cn 端口：80

	上海GDG镜像服务器地址:

		sdk.gdgshanghai.com 端口：8000

	北京化工大学镜像服务器地址:

		IPv4: ubuntu.buct.edu.cn/ 端口：80

		IPv4: ubuntu.buct.cn/ 端口：80

		IPv6: ubuntu.buct6.edu.cn/ 端口：80

	大连东软信息学院镜像服务器地址:

		mirrors.neusoft.edu.cn 端口：80
```

### 02.3 Android模拟器安装

#### windows

模拟器Genymotion安装

```
1.执行genymotion-2.11.0-vbox.exe(是一个集合程序，包含genymotion和virtualbox) -> 不需要更改配置，直接下一步默认安装

2.安装完genymotion继续等待，会提示安装virtualbox，继续安装，期间会提示安装oracle插件，全部允许安装

3.安装完成后会在桌面展示genymotion和virtualbox两个图标
```

![Snip20180122_4](移动端测试_image/Snip20180122_4.jpg)

虚拟机镜像导入

```
1.打开virtualbox

2.进入virtualbox -> 管理 -> 导入虚拟电脑

3.点击文件选择(Samsung Galaxy S6 - 5.1.0 - API 22 - 1440x2560.ova) -> 点击下一步

4.勾选 重新初始化所有网卡的MAC地址

5.点击导入按钮 -> 等待倒入完成

6.virtualbox列表会展示如下图圈出的选项
```

![Snip20180122_4](移动端测试_image/Snip20180122_3.png)

启动android模拟器

```
1.点击genymotion图标 -> 弹出框点击 >Personal Use

2.同意条款

3.genymotion主界面选择系统后点机start按钮

4.启动成功
```

![Snip20180122_4](移动端测试_image/Snip20180122_2.png)

#### macOS

请阅读Windows的使用方法后再阅读mac，因为两者基本一致。

模拟器Genymotion安装

```
1.安装VirtualBox-5.1.30-OSX.dmg

2.安装genymotion-2.11.0.dmg
```

虚拟机镜像导入

```
1.双击Samsung Galaxy S6 - 5.1.0 - API 22 - 1440x2560.ova

2.点击导入
```

启动android模拟器

```
同 windows
```

#### 可能出现的问题

- VirtualBox 创建com对象失败 应用程序被中断
  - https://www.cnblogs.com/iluzhiyong/p/5597557.html
- genymotion unable to start the virtual XXXXXX
  - 更新vm
  - 管理 - 检查更新

#### 为虚拟机提供安装apk功能

```
1.安装genymotion ARM插件，此插件可提供x86运行环境，即可运行apk，需要下载对应版本的插件(本次使用android 5.1版本插件)

2.拖动ARM_Translation_Lollipop_20160402.zip到已启动的android虚拟机上

3.点击提示的ok按钮

4.重启后生效
```

![Snip20180122_4](移动端测试_image/Snip20180122_1.png)

#### 补充：下载其他版本模拟器

需要注册一个genymotion账号，官网：https://www.genymotion.com

进入genymotion，点击Add按钮

![Snip20180122_4](移动端测试_image/Snip20180123_1.png)

点击Sign in，输入注册的genymotion用户名和密码

![Snip20180122_4](移动端测试_image/Snip20180123_2.png)

![Snip20180122_4](移动端测试_image/Snip20180123_3.png)

选择下载需要版本的模拟器

![Snip20180122_4](移动端测试_image/Snip20180123_4.png)

![Snip20180122_4](移动端测试_image/Snip20180123_5.png)

等待下载完成(下载时间根据网络)

![Snip20180122_4](移动端测试_image/Snip20180123_6.png)

![Snip20180122_4](移动端测试_image/Snip20180123_7.png)

## 03.包名和启动名

### 03.1 包名

决定程序的唯一性（不是应用的名字）

包名默任是反向域名+项目名

### 03.2 启动名

**目前可以理解**，一个启动名，对应着一个界面。

## 04.adb命令介绍

### 04.1 adb的含义

ADB全名Andorid Debug Bridge。 是一个Debug工具。为何称之为Bridge呢？因为adb是一个标准的C/S结构的工具, 是要连接开发电脑和调试手机的。包含如下几个部分:

```
1.Client端，运行在开发机器中，即你的开发PC机。用来发送adb命令。
2.Daemon守护进程, 运行在调试设备中, 即的调试手机或模拟器。
3.Server端, 作为一个后台进程运行在开发机器中, 即你的开发PC机. 用来管理PC中的Client端和手机的Daemon之间的通信。
```

### 04.2 adb常用命令

#### adb帮助

```
adb --help
```

#### 启动adb server

```
adb start-server
```

#### 关闭adb server

```
adb kill-server
```

#### 获取设备号

```
adb devices
```

#### 获取系统版本

```
adb -s 设备号 shell getprop ro.build.version.release
```

#### 发送文件到手机

```
adb push 电脑端文件路径/需要发送的文件  手机端存储的路径

示例：
	将桌面的xx.png发送到手机sdcard目录下
	adb push C:\Users\win\Desktop\xx.png  /sdcard
```

#### 从手机拉取文件

```
adb pull 手机端的路径/拉取文件名 电脑端存储文件路径

示例：
	将手机/sdcard目录中的xx.png文件，发送到电脑桌面
	adb pull /sdcard/xx.png C:\Users\win\Desktop
```

#### 查看手机运行日志

```
adb logcat
```

#### 手机shell命令行

```
adb shell
```

#### 获取app包名和启动名

手机需要先打开对应app

```
1.Mac/Linux: 'adb shell dumpsys window windows | grep mFocusedApp’
2.在 Windows 终端运行 'adb shell dumpsys window windows’ 然后去看mFocusedApp这一行的内容。
```

#### 安装app到手机

```
adb install 路径/xx.apk
```

#### 卸载手机手机app

```
adb uninstall 包名
```

#### 获取app启动时间

```
adb shell am start -W 包名/启动名

示例：
	adb shell am start -W com.yly.drawpic/.MainActivity
解释：
	ThisTime  该activity启动耗时
	TotalTime  应用自身启动耗时 = ThisTime + 应用application等资源启动时间
	WaitTime  系统启动应用耗时 = TotalTime + 系统资源启动时间
	WaitTime = 页面启动时间 + 应用启动时间 + 系统资源启动时间 xiang
```

## 05.移动端自动化测试工具

### 05.1 主流的移动端自动化工具

- Robotium

​    1.支持语言：Java

​    2.仅支持Android系统

​    3.不支持跨应用

- Macaca

​    1.支持语言：Java，Python，Node.js

​    2.支持Android和iOS系统

​    3.支持跨应用

- Appium

​    1.支持语言：Java，C#，Python，php，perl，ruby，Node.js

​    2.支持Android和iOS系统

​    3.支持跨应用

- 自动化工具选择的关注点

​    1.是否支持native，webview

​    2.是否支持获取toast

​    3.是否支持跨应用

### 05.2 Appium介绍 

Appium是一个移动端的自动化框架，可用于测试原生应用，移动网页应用和混合型应用，且是跨平台的。可用于iOS和Android以及firefox的操作系统。原生的应用是指用android或ios的sdk编写的应用，移动网页应用是指网页应用，类似于ios中safari应用或者Chrome应用或者类浏览器的应用。混合应用是指一种包裹webview的应用,原生应用于网页内容交互性的应用。
重要的是Appium是跨平台的，何为跨平台，意思就是可以针对不同的平台用一套api来编写测试用例。

### 05.3 Appium特点

1.使用自动化来测试一个app，但是不需要重新编译它
2.写自动化case，不需要学习特定的语言
3.一个自动化框架不需要重复造轮子
4.一个自动化框架需要开源，在精神和实践上实现开源

### 05.4 Appium自动化测试环境搭建

我们使用Appium和python来进行自动化测试，需要安装两个东西，一个是Appium的客户端，一个是Appium-python库。这两个需要安装的东西在加上手机就可以进行自动化测试，它们之间的关系是：python代码 -> Appium-python库 -> Appium -> 手机。

用python写代码,写的代码需要import一些库,模块,这时需要Appium-python库里面的一些函数,然后Appium-python库连接appium客户端,appium客户端再对手机进行操作.   appium客户端(跨平台)会知道你是测ios的还是安卓的, xiang

#### Appium客户端安装

##### Appium背景介绍

```
1.官网：www.appium.io,由SauceLab公司开发

2.Appium是由nodejs的express框架写的Http Server,Appium使用WebDriver的json wire协议，来驱动Apple系统的UIAutomation库、Android系统的UIAutomator框架
```

##### Appium安装软件位置xiang

```
E:\testProgram  的appium-desktop-setup-1.10.02.rar一路next即可
```



##### Appium桌面客户端安装方式

```
1. 运行appium-desktop-Setup-1.2.7.exe，默认安装即可
2. 启动客户端，按图片步骤 1 -> 2 -> 3 -> 4 设置
```

![启动appium界面](移动端测试_image/启动appium.png)

```
3. 启动成功展示如下图
```

![appium启动成功](移动端测试_image/启动成功.png)

##### Appium命令行安装方式

```
1. 安装Node.js ->Win:官网下载可执行包安装(Linux: yum install; Macos: brew install)
2. 安装完成后 命令行运行npm或node -v 来查看是否安装成功
```

![node](移动端测试_image/node.png) 

![npm](移动端测试_image/npm.png)

```
敲黑板: npm国内一般被墙，所以选择淘宝镜像安装，官网:http://npm.taobao.org
3. 安装cnpm: npm install -g cnpm --registry=https://registry.npm.taobao.org
```

![cnpm](移动端测试_image/cnpm.png)

```
4. 安装appium: cnpm install -g appium
```

![appium_install](移动端测试_image/appium_install.png) ![appium_result](移动端测试_image/appium_result.png)

```
4. 启动appium服务命令: appium &，如下图即正确安装
敲黑板: Windows安装会提示os的模块错误，这个需要mac系统支持，不影响windows操作使用
```

![appium_start](移动端测试_image/appium_start.png)

#### Appium-python库安装

##### 命令行安装(需要联网)

此命令行在cmd回车后写xiang

```
pip install Appium-Python-Client
```

##### 安装包安装

```
前提：python已安装setuptools包
安装setuptools:
	1.解压setuptools-38.2.4.zip
	2.进入解压后文件夹执行命令: python setup.py install
	3.等待安装完成，无错误信息即可

安装Appium-Python-Client:
	1.解压Appium-Python-Client-0.25.tar.gz
	2.进入解压后文件夹执行命令: python setup.py install
	3.等待安装完成，无错误信息即可
```

##### 网页应用&原生应用&混合应用

原生应用:指用android或ios的sdk编写的应用，

移动网页应用:网页应用，类似于ios中safari应用或者Chrome应用或者类浏览器的应用(拿浏览器就能操作的应用就叫网页应用)。

混合应用是指一种包裹webview的应用,原生应用于网页内容交互性的应用。

原生应用:用谷歌提供的java代码

webview应用:用html写的

## 06.Hello Appium 

### 需求

使用Python打开android模拟器中的设置界面。

![](移动端测试_image/第一个例子.gif)

### 思路

python代码到手机的过程是需要先经过Appium-python库再经过Appium再到手机。也就是python代码 -> Appium-python库 -> Appium -> 手机。



### 方法

```
  from appium import webdriver

  import time

  # server 启动参数
  desired_caps = {}
  # 设备信息
  desired_caps['platformName'] = 'Android'
  desired_caps['platformVersion'] = '5.1'
  desired_caps['deviceName'] = '192.168.56.101:5555'
  # app信息
  desired_caps['appPackage'] = 'com.android.settings'
  desired_caps['appActivity'] = '.Settings'

  driver = webdriver.Remote('http://localhost:4723/wd/hub', desired_caps)

  # time.sleep(2)

  # driver.quit()
```

##### uiautomatorviewer安装包 xiang

```
E:\testProgram\android-sdk-windows\tools\bin
```

##### 手机端的开发:

app端相对web端简单,因为不需要涉及复杂的业务逻辑,手机做的是ui界面的设计,比如按钮位置,文本框位置等,数据是从哪来的,直接服务器一个接口就来的,然后把数据展现在对应控件上. xiang

## 07.Appium 基础API

### App基础操作API

#### 前置代码

```
  # server 启动参数

  desired_caps = {}
  desired_caps['platformName'] = 'Android' 
  desired_caps['platformVersion'] = '5.1'
  desired_caps['deviceName'] = '192.168.56.101:5555'
  desired_caps['appPackage'] = 'com.android.settings'
  desired_caps['appActivity'] = '.Settings'
  desired_caps['unicodeKeyboard'] = True
  desired_caps['resetKeyboard'] = True

  # 声明driver对象
  driver = webdriver.Remote('http://127.0.0.1:4723/wd/hub', desired_caps)

```

appium通过adb命令操作手机

adb命令能操作手机,python代码也能操作手机. xiang

```
import os

deviceName = os.popen('adb shell getprop ro.product.model').read()
print(deviceName)
platformVersion = os.popen('adb shell getprop ro.build.version.release').read()
print(platformVersion)
device = os.popen('adb shell getprop ro.product.name ').read()
print(device)
# 前三个对应的输出为Android SDK built for x86, 6.0, sdk_google_phone_x86
此python代码也可获取前置代码的信息 xiang
```



####获取app包名和启动名

```
	获取包名方法：current_package
	获取启动名：current_activity
```
```
	业务场景：
		1.启动设置
		2.获取包名和启动名
```
```
	代码实现：
		print(driver.current_package)
    	print(driver.current_activity)
    执行结果：
    	com.tencent.news
    	.activity.SplashActivity
```
#### 脚本内启动其他app

```
    driver.start_activity(appPackage,appActivity)
    参数：
    	appPackage：包名
    	appActivity：启动名
    示例：
    	driver.start_activity('com.android.mms', '.ui.ConversationList')
```

#### 关闭app

```
	driver.close_app()  # 关闭当前操作的app，不会关闭驱动对象
```

#### 关闭驱动对象

```
	driver.quit()   # 关闭驱动对象，同时关闭所有关联的app
```

#### 安装APK到手机

```
	driver.install_app(app_path) 
	参数：
		app_path：脚本机器中APK文件路径
	示例：
		driver.install_app("/Users/Yoson/Downloads/anzhishichang_6450.apk")
```

#### 手机中移除APP

```
	driver.remove_app(app_id) 
	参数：
		app_id：需要卸载的app包名
	示例：
		driver.remove_app('cn.goapk.market')
```

#### 判断APP是否已安装

```
	driver.is_app_installed(app_id) 
	参数：
		bundle_id: 可以传入app包名,返回结果为True(已安装) / False(未安装)
	示例：
	print(driver.is_app_installed('cn.goapk.market'))
```

编码:encode

解码:decode

#### 发送文件到手机

```
	import base64
	data = str(base64.b64encode(data.encode('utf-8')),'utf-8')
	driver.push_file(path,data)
	参数：
		path：手机设备上的路径(例如：/sdcard/a.txt)
		data：文件内数据,要求base64编码
		Python3.x中字符都为unicode编码，而b64encode函数的参数为byte类型，需要先转码；生成的数据为byte类型，需要将byte转换回去。
	示例：
		import base64
		data = str(base64.b64encode('test 123'.encode('utf-8')), 'utf-8')
		driver.push_file('/sdcard/test.txt', data)
```

#### 从手机中拉取文件

```
	import base64
	data = driver.pull_file(path) # 返回数据为base64编码
	print(str(base64.b64decode(data),'utf-8')) # base64解码
	参数：
		path: 手机设备上的路径
	示例：
		import base64
		data = driver.pull_file('/sdcard/test.txt') # 返回数据为base64编码
		print(str(base64.b64decode(data), 'utf-8')) # base64解码
```

#### 获取当前屏幕内元素结构

```
	driver.page_source  
	作用：
		返回当前页面的文档结构，判断特定的元素是否存在
	示例：
		print(driver.page_source)
```

####应用置于后台事件

```
	APP放置后台，模拟热启动
	方法：background_app(seconds)
	参数：
		1.seconds:停留在后台的时间，单位：秒
```
```
	业务场景：
		1.进入设置页
		2.将APP置于后台5s
```
```
	代码实现：
		driver.background_app(5)
	效果：
		app置于后台5s后，再次展示当前页面
```



## 08.UIAutomatorViewer

### 工具简介

用来扫描和分析Android应用程序的UI控件的工具.

### 如何使用

1.进入SDK目录下的tools目录，打开uiautomatorviewer

2.电脑连接真机或打开android模拟器

3.启动待测试app

4.点击uiautomatorviewer的左上角Device Screenshot,会生成app当前页面的UI控件截图

![Snip20180122_4](移动端测试_image/UI01.png)

![Snip20180122_4](移动端测试_image/UI02.png)

## 09.元素定位API

```
文字类元素定位有id,class,xpath等,我觉得还是xpath定位比较方便,因为id,class属性,会有好几个元素都有,你要定位一个元素会有麻烦,除非这个元素的id或class唯一,这样定位比较快.xpath定位是最简单易操作的,比如通过元素的文本定位,一般情况下页面中的元素的文本是唯一的,就可以用//*[@text='Display'],但也是会有其他元素的文本为Display,但xpath定位还是很方便,因为可以肉眼在页面上一扫,如果确实是唯一的,就用xpath,但id,class就不行. xiang
```



手工测试主要通过可见按钮操作，而自动化是通过元素进行交互操作.
⚠️⚠️⚠️ 元素的基本定位基于当前屏幕范围内展示的可见元素。

* Appium常用元素定位方式

| name  | value       |
| ----- | ----------- |
| id    | id属性值    |
| class | class属性值 |
| xpath | xpath表达式 |

* 前置代码

```
	from appium import webdriver
	# server 启动参数
	desired_caps = {}
	# 设备信息
	desired_caps['platformName'] = 'Android'
	desired_caps['platformVersion'] = '5.1'
	desired_caps['deviceName'] = '192.168.56.101:5555'
	# app的信息
	desired_caps['appPackage'] = 'com.android.settings'
	desired_caps['appActivity'] = '.Settings'

	# 声明我们的driver对象
	driver = webdriver.Remote('http://127.0.0.1:4723/wd/hub', desired_caps)
```

### 定位一个元素 element

#### 通过id定位

```
	方法：find_element_by_id(id_value) # id_value:为元素的id属性值
```
```
	业务场景:
		1.进入设置页面
		2.通过ID定位方式点击搜索按钮
```
```
	代码实现：
		driver.find_element_by_id("com.android.settings:id/search").click()
		driver.quit()
```

#### 通过class定位

```
	方法：find_element_by_class_name(class_value) # class_value:为元素的class属性值
```

```
	业务场景:
		1.进入设置页面
		2.点击搜索按钮
		3.通过class定位方式点击输入框的返回按钮
```
```
	代码实现：
		# id 点击搜索按钮
		driver.find_element_by_id("com.android.settings:id/search").click()
		# class 点击输入框返回按钮
		driver.find_element_by_class_name('android.widget.ImageButton').click()
		driver.quit()
```

#### 通过xpath定位

```
	方法：find_element_by_xpath(xpath_value) # xpath_value:为可以定位到元素的xpath语句
```
```
	*** android端xptah常用属性定位：
		1. id ://*[contains(@resource-id,'com.android.settings:id/search')] 
		2. class ://*[contains(@class,'android.widget.ImageButton')]
		3. text ://*[contains(@text,'WLA')]

	*** 模糊定位 contains(@key,value): value可以是部分值
```

```
	业务场景:
		1.进入设置页面
		2.点击WLAN菜单栏
```
```
	代码实现：
		# xpath 点击WLAN按钮
	    driver.find_element_by_xpath("//*[contains(@text,'WLA')]").click()
```

### 定位一组元素 elements

```
	应用场景为元素值重复，无法通过元素属性直接定位到某个元素，只能通过elements方式来选择，返回一个定位对象的列表.
```

#### 通过id方式定位一组元素

```
	方法： find_elements_by_id(id_value) # id_value:为元素的id属性值
```

```
	业务场景:
		1.进入设置页面
		2.点击WLAN菜单栏(id定位对象列表中第1个)
```

```
	代码实现：
		# 定位到一组元素
		title = driver.find_elements_by_id("com.android.settings:id/title")
		# 打印title类型，预期为list
    	print(type(title))
    	# 取title返回列表中的第一个定位对象，执行点击操作
    	title[0].click()
```

#### 通过class方式定位一组元素

```
	方法：find_elements_by_class_name(class_value) # class_value:为元素的class属性值
```

```
	业务场景:
		1.进入设置页面
		2.点击WLAN菜单栏(class定位对象列表中第3个)
```

```
	代码实现：
		# 定位到一组元素
		title = driver.find_elements_by_class_name("android.widget.TextView")
		# 打印title类型，预期为list
    	print(type(title))
    	# 取title返回列表中的第一个定位对象，执行点击操作
    	title[3].click()
```

#### 通过xpath方式定位一组元素

```
	方法:find_elements_by_xpath(xpath_value) # xpath_value:为可以定位到元素的xpath语句
```

```
	业务场景:
		1.进入设置页面
		2.点击WLAN菜单栏(xpath中class属性定位对象列表中第3个)
```

```
	代码实现：
		# 定位到一组元素
		title = driver.find_elements_by_xpath("//*[contains(@class,'widget.TextView')]")
		# 打印title类型，预期为list
    	print(type(title))
    	# 取title返回列表中的第一个定位对象，执行点击操作
    	title[3].click()
```
### WebDriverWait 显示等待 

```
	在一个超时时间范围内，每隔一段时间去搜索一次元素是否存在，
	如果存在返回定位对象，如果不存在直到超时时间到达，报超时异常错误。
```

```
	方法:WebDriverWait(driver, timeout, poll_frequency).until(method)
	参数：
		1.driver：手机驱动对象
		2.timeout：搜索超时时间
		3.poll_frequency：每次搜索间隔时间，默认时间为0.5s
		4.method：定位方法(匿名函数)
```

```
	匿名函数: 
		lambda x: x
	等价于python函数：
		def test(x):
    		return x
```

```
	使用示例：
		from selenium.webdriver.support.wait import WebDriverWait
		WebDriverWait(driver, timeout, poll_frequency).until(lambda x: x.find_elements_by_id(id_value))
	解释：
		1.x传入值为：driver，所以才可以使用定位方法.
	函数运行过程：
		1.实例化WebDriverWait类，传入driver对象，之后driver对象被赋值给WebDriverWait的一个类变量：self._driver
		2.until为WebDriverWait类的方法，until传入method方法(即匿名函数)，之后method方法会被传入self._driver
		3.搜索到元素后until返回定位对象，没有搜索到函数until返回超时异常错误.
```

```
	业务场景:
		1.进入设置页面
		2.通过ID定位方式点击搜索按钮
```

```
	代码实现：
		from selenium.webdriver.support.wait import WebDriverWait # 导入WebDriverWait类
		# 超时时间为30s，每隔1秒搜索一次元素是否存在，如果元素存在返回定位对象并退出
		search_button = WebDriverWait(driver, 30, 1).until(lambda x: x.find_elements_by_id(com.android.settings:id/search))
		search_button.click()
		driver.quit()
```
## 10.元素操作API

​	本节讲介绍手机端元素信息的获取以及基本的输入操作。

* 前置代码

```
	from appium import webdriver
	# server 启动参数
	desired_caps = {}
	# 设备信息
	desired_caps['platformName'] = 'Android'
	desired_caps['platformVersion'] = '5.1'
	desired_caps['deviceName'] = '192.168.56.101:5555'
	# app的信息
	desired_caps['appPackage'] = 'com.android.settings'
	desired_caps['appActivity'] = '.Settings'

	# 声明我们的driver对象
	driver = webdriver.Remote('http://127.0.0.1:4723/wd/hub', desired_caps)
```
### 点击元素
```
	方法：click() 
```
```
	业务场景:
		1.打开设置
		2.点击搜索按钮
```

```
	代码实现：
		# 点击搜索按钮
    	driver.find_element_by_id("com.android.settings:id/search").click()
```
### 发送数据到输入框

```
	方法：send_keys(vaue) # value：需要发送到输入框内的文本
```
```
	业务场景:
		1.打开设置
		2.点击搜索按钮
		3.输入内容abc
```

```
	代码实现：
		# 点击搜索按钮
    	driver.find_element_by_id("com.android.settings:id/search").click()
    	# 定位到输入框并输入abc
    	driver.find_element_by_id("android:id/search_src_text").send_keys("abc")

    重点:
    	大家可以将输入的abc 改成 输入中文，得到的结果:输入框无任何值输入且程序不会抱错
```
```
	解决输入中文问题：

		1.server 启动参数增加两个参数配置
			desired_caps['unicodeKeyboard'] = True
			desired_caps['resetKeyboard'] = True

		2.再次运行会发现运行成功
			# 点击搜索按钮
	    	driver.find_element_by_id("com.android.settings:id/search").click()
	    	# 定位到输入框并输入abc
	    	driver.find_element_by_id("android:id/search_src_text").send_keys("传智播客")
```
### 清空输入框内容

```
	方法：clear()
```
```
	业务场景:
		1.打开设置
		2.点击搜索按钮
		3.输入内容abc
		4.删除已输入abc
```
```
	代码实现：
		# 点击搜索按钮
	    driver.find_element_by_id("com.android.settings:id/search").click()
	    # 定位到输入框并输入abc
	    input_text = driver.find_element_by_id("android:id/search_src_text")
	    # 输入abc
	    input_text.send_keys("abc")
	    time.sleep(1)
	    # 删除abc
	    input_text.clear()
```

### 获取元素的文本内容

```
	方法: text
```
```
	业务场景：
		1.进入设置
		2.获取所有元素class属性为“android.widget.TextView”的文本内容
```
```
	代码实现：
		text_vlaue = driver.find_elements_by_class_name("android.widget.TextView")
	    for i in text_vlaue:
	        print(i.text)
	执行结果：
		设置

		无线和网络
		WLAN
		更多
		设备
		显示
		提示音和通知
		存储
```
### 获取元素的属性值

```
	方法: get_attribute(value) # value:元素的属性
	⚠️ value='name' 返回content-desc / text属性值
	⚠️ value='text' 返回text的属性值
	⚠️ value='className' 返回 class属性值，只有 API=>18 才能支持
	⚠️ value='resourceId' 返回 resource-id属性值，只有 API=>18 才能支持
```
```
	业务场景：
		1.进入设置
		2.获取搜索按钮的content-desc属性值
```
![搜索属性](移动端测试_image/搜索属性.png)
```
	代码实现：
		# 定位到搜索按钮
		get_value = driver.find_element_by_id("com.android.settings:id/search")
    	print(get_value.get_attribute("name"))
    执行结果：
    	搜索
```
### 获取元素在屏幕上的坐标

```
	方法:location
```
```
	业务场景：
		1.进入设置页面
		2.获取搜索按钮在屏幕的坐标位置
```
```
	代码实现:
		# 定位到搜索按钮
	    get_value = driver.find_element_by_id("com.android.settings:id/search")
	    # 打印搜索按钮在屏幕上的坐标
	    print(get_value.location)
	执行结果:
		{'y': 44, 'x': 408}
```

出现appium卡到code 0, signal null的bug:解决方法:将手机中(需要adb shell进入)/data/local/tmp的那个jar文件重新命名为"AppiumBootStrap.jar"

```
eles = driver.find_elements_by_id('com.android.settings:id/category_title')
time.sleep(3)
print(eles[1].location)
通过id查找元素,发现找了好几个,但只要1个,可以在元素集后加索引    xiang
```





## 11.滑动和拖拽事件

* 前置代码

```
	from appium import webdriver
	# server 启动参数
	desired_caps = {}
	# 设备信息
	desired_caps['platformName'] = 'Android'
	desired_caps['platformVersion'] = '5.1'
	desired_caps['deviceName'] = '192.168.56.101:5555'
	# app的信息
	desired_caps['appPackage'] = 'com.android.settings'
	desired_caps['appActivity'] = '.Settings'

	# 声明我们的driver对象
	driver = webdriver.Remote('http://127.0.0.1:4723/wd/hub', desired_caps)
```
### swipe 滑动事件

```
	⚠️从一个坐标位置滑动到另一个坐标位置,只能是两个点之间的滑动
	方法：swipe(start_x, start_y, end_x, end_y, duration=None)
	参数：
		1.start_x：起点X轴坐标
		2.start_y：起点Y轴坐标
		3.end_x：  终点X轴坐标
		4.end_y,： 终点Y轴坐标
		5.duration： 滑动这个操作一共持续的时间长度，单位：ms
```
```
	业务场景：
		1.进入设置
		2.从坐标(148,659)滑动到坐标(148,248)
```
```
	代码实现：
		# 滑动没有持续时间
		driver.swipe(188,659,148,248)
		# 滑动持续5秒的时间
		driver.swipe(188,659,148,248,5000)
```

### scroll 滑动事件

```
	⚠️ 从一个元素滑动到另一个元素，直到页面自动停止
	方法：scroll(origin_el, destination_el)
	参数：
		1.origin_el：滑动开始的元素
		2.destination_el：滑动结束的元素
```
```
	业务场景：
		1.进入设置页
		2.模拟手指从存储菜单位置 到 WLAN菜单位置的上滑操作
```
```
	代码实现：
		# 定位到存储菜单栏
		el1 = driver.find_element_by_xpath("//*[contains(@text,'存储')]")
		# 定位到WLAN菜单栏
	    el2 = driver.find_element_by_xpath("//*[contains(@text,'WLAN')]")
	    # 执行滑动操作
	    driver.scroll(el1,el2)
```
### drag 拖拽事件

```
	⚠️ 从一个元素滑动到另一个元素,第二个元素替代第一个元素原本屏幕上的位置
	方法：drag_and_drop(origin_el, destination_el)
	参数：
		1.origin_el：滑动开始的元素
		2.destination_el：滑动结束的元素
```
```
	业务场景：
		1.进入设置页
		2.模拟手指将存储菜单 滑动到 WLAN菜单栏位置
```
```
	代码实现：
		# 定位到存储菜单栏
		el1 = driver.find_element_by_xpath("//*[contains(@text,'存储')]")
		# 定位到WLAN菜单栏
	    el2 = driver.find_element_by_xpath("//*[contains(@text,'WLAN')]")
	    # 执行滑动操作
	    driver.drag_and_drop(el1,el2)
```

测试某一段代码运行的时间 xiang

```python
print(time.time())
driver.swipe(100, 200, 100, 500)
print(time.time())
```

通用代码一之:找页面的某一个元素,如果有,就点击.没有先翻页,然后找,再点击(即滚动页面---点击)

```python
    while True:
        try:
            driver.find_element_by_xpath("//*[@text='关于手机']").click()
            break
        except Exception:
            # 翻页,滑动的时候从下往上直着滑,x坐标不动,在屏幕宽度的一半位置,y坐标从屏幕高度
            # 的3/4滑到1/4
            window_width = driver.get_window_size()['width']
            window_height = driver.get_window_size()['height']
            start_x= window_width * 0.5
            end_x = start_x
            start_y = window_height * 0.75
            end_y = window_height * 0.25

            driver.swipe(start_x, start_y, end_x, end_y, 5000)
        # 现在需要是在点击了的'关于手机'页面,看副标题有没有5.1
    time.sleep(1)
    eles = driver.find_elements_by_class_name('android.widget.TextView')
    for i in eles:
        if i.text == '5.1':
            print('有')
            break
    else:
        print('没有')
```

```
脚本怎么判断模拟机一个页面滑到底了?????????????xiang
```

## 12.高级手势TouchAction

```
	TouchAction是AppiumDriver的辅助类，主要针对手势操作，比如滑动、长按、拖动等，
	原理是将一系列的动作放在一个链条中发送到服务器，服务器接受到该链条后，解析各个动作，逐个执行。
```
⚠️ 所有手势都要通过执行perform()函数才会运行.

链条Action:一堆动作通过 动作.动作.动作.perform() 这一串动作就是链条

### 手指轻敲操作

```
	模拟手指轻敲一下屏幕操作
	方法：tap(element=None, x=None, y=None)
	方法：perform() # 发送命令到服务器执行操作
	参数：
		1.element：被定位到的元素
		2.x：相对于元素左上角的坐标，通常会使用元素的X轴坐标
		3.y：通常会使用元素的Y轴坐标
```
```
	业务场景：
		1.进入设置
		2.点击WLAN选项
```
```
	代码实现：
		# 通过元素定位方式敲击屏幕
	    el = driver.find_element_by_xpath("//*[contains(@text,'WLAN')]")
	    TouchAction(driver).tap(el).perform()

	    # 通过坐标方式敲击屏幕，WLAN坐标:x=155,y=250
	    # TouchAction(driver).tap(x=155,y=250).perform()
```

手指轻敲的效果和click效果一样  xiang

### 手指按下和抬起操作

```
	模拟手指按下屏幕,按就要对应着离开.
```
```
	方法:press(el=None, x=None, y=None)
	方法:release() # 结束动作，手指离开屏幕
	参数：
		1.element：被定位到的元素
		2.x：通常会使用元素的X轴坐标
		3.y：通常会使用元素的Y轴坐标
```
```
	业务场景:
		1.进入设置
		2.点击WLAN选项
```
```
	代码实现：
		# 通过元素定位方式按下屏幕
	    el = driver.find_element_by_xpath("//*[contains(@text,'WLAN')]")
	    TouchAction(driver).press(el).release().perform()

	    # 通过坐标方式按下屏幕，WLAN坐标:x=155,y=250
	    # TouchAction(driver).tap(x=155,y=250).release().perform()
```
### 等待操作

```
	方法：wait(ms=0)
	参数：
		ms：暂停的毫秒数

```

```
	业务场景:
		1.进入设置
		2.点击WLAN选项
		3.长按WiredSSID选项5秒

```

```
	代码实现：
		# 点击WLAN
	    driver.find_element_by_xpath("//*[contains(@text,'WLAN')]").click()
	    # 定位到WiredSSID
	    el =driver.find_element_by_id("android:id/title")
	    # 通过元素定位方式长按元素
	    TouchAction(driver).press(el).wait(5000).perform()

	    # TouchAction(driver).press(x=171,y=245).wait(5000).release().perform() ⚠️ 该方法未能完成长按操作，没有报任何错误

```

### 手指长按操作

```
	模拟手机按下屏幕一段时间,按就要对应着离开.
```
```
	方法：long_press(el=None, x=None, y=None, duration=1000)
	参数：
		1.element：被定位到的元素
		2.x：通常会使用元素的X轴坐标
		3.y：通常会使用元素的Y轴坐标
		4.duration：持续时间，默认为1000ms
```
```
	业务场景:
		1.进入设置
		2.点击WLAN选项
		3.长按WiredSSID选项5秒
```
```
	代码实现：
		# 点击WLAN
	    driver.find_element_by_xpath("//*[contains(@text,'WLAN')]").click()
	    # 定位到WiredSSID
	    el =driver.find_element_by_id("android:id/title")
	    # 通过元素定位方式长按元素
	    TouchAction(driver).long_press(el,duration=5000).release().perform()
```
### 手指移动操作

```
	模拟手机的滑动操作
	方法：move_to(el=None, x=None, y=None)
	参数:
		1.el:定位的元素
		2.x:相对于前一个元素的X轴偏移量
		3.y:相对于前一个元素的Y轴偏移量
```
```
	业务场景：
		1.进入设置
		2.向上滑动屏幕
```

```
	代码实现：
    	# 定位到存储
	    el = driver.find_element_by_xpath("//*[contains(@text,'存储')]")
	    # 定位到更多
	    el1 = driver.find_element_by_xpath("//*[contains(@text,'更多')]")
	    # 元素方式滑动
	    TouchAction(driver).press(el).move_to(el1).release().perform()
	    # 坐标的方式滑动
	    # TouchAction(driver).press(x=240,y=600).wait(100).move_to(x=100,y=100).release().perform()

```
### 案例-手势解锁

```
	需求：
		1.进入设置
		2.向上滑动屏幕到可见"安全"选项
		3.进入到安全
		4.点击屏幕锁定方式
		5.点击图案
		6.绘制图案
```

```
示例代码：

# 需要进入的页面
page_name = "安全"

# 如果找到就点击，如果没有往下滑，再次重新找，直到找到。
while True:
    try:
        driver.find_element_by_xpath("//*[contains(@text,'" + page_name + "')]").click()
        break
    except Exception:
        driver.swipe(100, 2000, 100, 1000)
        time.sleep(1)

driver.find_element_by_xpath("//*[contains(@text,'屏幕锁定')]").click()
time.sleep(1)
driver.find_element_by_xpath("//*[contains(@text,'图案')]").click()
time.sleep(1)
TouchAction(driver).press(x=233, y=834).move_to(x=0, y=480).move_to(x=480, y=0).move_to(x=480, y=-480).move_to(x=0, y=480).move_to(x=0, y=480).release().perform()
```
![屏幕图案](./移动端测试_image/屏幕图案.gif)

python代码换行xiang:

```python
换行的2种方法.
法1:一个括号包住首尾,在需要换行的地方按回车.此法代码中不会出现斜杠\. 如果有很多小圆点,在小圆点的前面按回车,这样比较规范
    (TouchAction(driver).press(x=20, y=60).move_to(x=50, y=0)
     .move_to(x=50, y=0).move_to(x=0, y=50).move_to(x=0,y=50)
     .release().perform())
  法2:在需要换行的地方按回车,会自动在上一行加斜杠\,并且会换行.在小圆点的前面按回车
    TouchAction(driver).press(x=20, y=60).move_to(x=50, y=0)\
        .move_to(x=50, y=0).move_to(x=0, y=50).move_to(x=0,y=50)\
        .release().perform()
```





## 13.手机操作API

```
	针对手机的一些常用设置功能进行操作.
```
### 获取手机时间

```
	方法：device_time
```
```
	代码实现：
		# 获取当前手机的时间
		print(driver.device_time)
	执行结果：
		Wed Dec 27 08:52:45 EST 2017
```
### 获取手机的宽高

```
	获取手机的宽高，可以根据宽高做一些坐标的操作
```
```
	方法：get_window_size()
```
```
	代码实现：
		print(driver.get_window_size())
	执行结果：
		{'height': 800, 'width': 480}
```
### 发送键到设备

百度搜Android Keycode,即找到系统键值对应的码 xiang

```
	模拟系统键值的操作，比如操作honme键，音量键,返回键等。
```
```
	方法：keyevent(keycode, metastate=None):
	方法：press_keycode(keycode, metastate=None):
	参数：
		keycode：发送给设备的关键代码
		metastate：关于被发送的关键代码的元信息，一般为默认值
```
```
	业务场景:
		1.打开设置
		2.按多次音量增加键
```
```
	代码实现：
		for i in range(3):
        	driver.keyevent(24)
```
![音量增加键](./移动端测试_image/音量增加键.gif)
### 操作手机通知栏

```
	打开手机的通知栏，可以获取通知栏的相关信息和元素操作
```
```
	方法：open_notifications()
```
```
	业务场景: 
		1.启动设置
		2.打开通知栏
```
```
	代码实现：
		driver.open_notifications()
```
![通知栏](./移动端测试_image/通知栏.gif)
### 获取手机当前网络

​	获取手机当前连接的网络

```
	方法：network_connection
```
​	业务场景:
​		获取手机当前网络模式

```
	代码实现：
		print(driver.network_connection)
	执行结果：
		6
```
![网络模式](./移动端测试_image/网络模式.png)
### 设置手机网络

```
	更改手机的网络模式，模拟特殊网络情况下的测试用例
```
```
	方法：set_network_connection(connectionType)
	参数：
		connectionType：需要被设置成为的网络类型
```
```
	业务场景：
		1.启动设置
		2.设置手机网络为飞行模式
```
```
	代码实现：
		driver.set_network_connection(1)
```
![飞行模式](./移动端测试_image/飞行模式.gif)
### 手机截图

手机截图,根据截的图的结果来分析,比如操作500条数据,不需要盯着模拟器看结果.只需看500张图片.另一方面,有时上传bug,界面会有对应的反应,这时可以给开发截图放到报告上,

```
	截取手机当前屏幕，保存指定格式图片到设定位置
```
```
	方法：get_screenshot_as_file(filename)
	参数：
		filename：指定路径下，指定格式的图片.
```
```
	业务场景：
		1.打开设置页面
		2.截图当前页面保存到当前目录，命名为screen.png
```
```
	代码实现：
		import os
	    driver.get_screenshot_as_file(os.getcwd() + os.sep + './screen.png')
	执行结果：
		当前目录下会生成screen.png文件
```
## 14.Pytest安装和介绍

- 介绍

```
	pytest是python的一种单元测试框架，同自带的Unittest测试框架类似，相比于Unittest框架使用起来更简洁，效率更高。
```
- 特点:

```
	1.非常容易上手，入门简单，文档丰富，文档中有很多实例可以参考
	2.支持简单的单元测试和复杂的功能测试
	3.支持参数化
	4.执行测试过程中可以将某些测试跳过，或者对某些预期失败的Case标记成失败
	5.支持重复执行失败的Case
	6.支持运行由Nose , Unittest编写的测试Case
	7.具有很多第三方插件，并且可以自定义扩展
	8.方便的和持续集成工具集成
```
### Pytest安装

```
	1.mac／linux：sudo pip install -U pytest # -U:可以理解为--upgrade，表示已安装就升级为最新版本
	2.管理员方式运行cmd：pip install -U pytest
	3,windows直接输入pip install pytest   xiang
```
### Pytest安装成功校验

```
	1.进入命令行
	2.运行：pytest --version # 会展示当前已安装版本
```
## 15.Pytest运行方式

### Hello Pytest

```
	# file_name: test_abc.py
	import pytest # 引入pytest包
	def test_a(): # test开头的测试函数
	    print("------->test_a")
	    assert 1 # 断言成功
	def test_b():
	    print("------->test_b")
	    assert 0 # 断言失败
	if __name__ == '__main__':
	    # pytest.main("-s  test_abc.py") # 调用pytest的main函数执行测试
		pytest.main(["-s", "login.py"])
```
```
	执行结果：
		test_abc.py 
		------->test_a
		. # .(代表成功)
		------->test_b
		F # F(代表失败)
```
### Pytest运行方式

* 1.测试类主函数模式

```
	pytest.main(["-s", "test_abc.py"])
```
* 2.命令行模式

```
	pytest 文件路径／测试文件名
	例如：
		pytest -s test_abc.py
```

pytest运行有2种方式:a,代码 pytest.main("-s xxx.py")  b,在终端cmd命令行中,pytest  -s  xxx.py 

快速打开终端并且进入当前项目目录:控制台下方,有一个termial:看文件是否在当前的父文件夹里,在的话,pytest  -s  xxx.py ,如果是爷爷级,先cd 父文件夹,回车,然后,pytest  -s  xxx.py 

  xiang

## 16.setup和teardown函数

* 概述
```
	1.setup和teardown主要分为：函数级、类级、模块级、功能级。
	2.存在于测试类内部
```
### 函数级别

```
	运行于测试方法的始末，即:运行一次测试函数会运行一次setup和teardown
```
```
	代码示例：
		import pytest
		class TestABC:
			# 函数级开始
		    def setup(self):
		        print("------->setup_method")
		    # 函数级结束
		    def teardown(self):
		        print("------->teardown_method")
		    def test_a(self):
		        print("------->test_a")
		        assert 1
		    def test_b(self):
		        print("------->test_b")
		if __name__ == '__main__':
		    pytest.main("-s  test_abc.py")
```
```
	执行结果：
		test_abc.py 
		------->setup_method # 第一次 setup()
		------->test_a
		.
		------->teardown_method # 第一次 teardown()
		------->setup_method # 第二次 setup()
		------->test_b
		.
		------->teardown_method # 第二次 teardown()
```
### 类级别

```
	运行于测试类的始末，即:在一个测试内只运行一次setup_class和teardown_class，不关心测试类内有多少个测试函数。
```
```
	代码示例：
		import pytest
		class TestABC:
			# 测试类级开始
		    def setup_class(self):
		        print("------->setup_class")
		    # 测试类级结束
		    def teardown_class(self):
		        print("------->teardown_class")
		    def test_a(self):
		        print("------->test_a")
		        assert 1
		    def test_b(self):
		        print("------->test_b")
		if __name__ == '__main__':
		    pytest.main("-s  test_abc.py")
```
```
	执行结果：
		test_abc.py 
		------->setup_class # 第一次 setup_class()
		------->test_a
		.
		------->test_b
		F 
		------->teardown_class # 第一次 teardown_class()
```

setup,setup_class在测试脚本之前执行,但setup会放连接手机的代码,因为不用考虑返回,当前的操作是否影响下一个操作等,它是一个操作完成之后直接回到连接手机的那一步.setup_class基本不怎么用.

函数级别的setup,teardown不带classs,有几个函数,运行几个setup,teardown.类级别的setup_class,teardown_class,不论中间有多少个函数,只在类的最前最后加一个setup_class函数和eardown_class函数.     xiang



## 17.Pytest配置文件

```
	pytest的配置文件通常放在测试目录下，名称为pytest.ini，命令行运行时会使用该配置文件中的配置.

```

### 配置pytest命令行运行参数

```
	[pytest]
	addopts = -s ... # 空格分隔，可添加多个命令行参数 -所有参数均为插件包的参数

```

### 配置测试搜索的路径

```
	[pytest]
	testpaths = ./scripts  # 当前目录下的scripts文件夹 -可自定义

```

### 配置测试搜索的文件名

```
	[pytest]
	python_files = test_*.py  
	# 当前目录下的scripts文件夹下，以test_开头，以.py结尾的所有文件 -可自定义

```

### 配置测试搜索的测试类名

```
	[pytest]
	python_classes = Test*  
	# 当前目录下的scripts文件夹下，以test_开头，以.py结尾的所有文件中，以Test_开头的类 -可自定义

```

### 配置测试搜索的测试函数名

```
	[pytest]
	python_functions = test_*  
	# 当前目录下的scripts文件夹下，以test_开头，以.py结尾的所有文件中，以Test_开头的类内，以test_开头的方法 -可自定义

```

pytest.ini在windows中是不能出现中文的,在mac中可以.

测试脚本写在scripts目录,pytest.ini直接复制过来,它和scripts目录是兄弟关系.

有了pytest.ini文件,在terminal中直接敲pytest回车就行了.

## 18.Pytest常用插件

```
	插件列表网址：https://plugincompat.herokuapp.com
	包含很多插件包，大家可依据工作的需求选择使用。

```

```
	前置条件：
		1.文件路径：
			- Test_App
			- - test_abc.py
			- - pytest.ini
		2.pyetst.ini配置文件内容：
			[pytest]
			# 命令行参数
			addopts = -s
			# 搜索文件名
			python_files = test_*.py
			# 搜索的类名
			python_classes = Test*
			# 搜索的函数名
			python_functions = test_*

```

### Pytest测试报告

```
	通过命令行方式，生成xml/html格式的测试报告，存储于用户指定路径。

```

```
	插件名称：pytest-html
	安装方式：
		1.安装包方式 python setup.py install 
		2.命令行 pip install pytest-html
	使用方法：
		命令行格式：pytest --html=用户路径/report.html
    也可在pytest.ini文件中直接配置:addopts = -s --html=report/report.html这样在terminal中直接pytest就生成报告.xiang
```

```
	示例：
		import pytest
		class TestABC:
			def setup_class(self):
				print("------->setup_class")
			def teardown_class(self):
				print("------->teardown_class")
			def test_a(self):
				print("------->test_a")
				assert 1
			def test_b(self):
				print("------->test_b")
				assert 0 # 断言失败
	运行方式：
		1.修改Test_App/pytest.ini文件，添加报告参数，即：addopts = -s --html=./report.html 
			# -s:输出程序运行信息
			# --html=./report.html 在当前目录下生成report.html文件
			⚠️ 若要生成xml文件，可将--html=./report.html 改成 --html=./report.xml
		2.命令行进入Test_App目录
		3.执行命令： pytest
	执行结果：
		1.在当前目录会生成assets文件夹和report.html文件

```

![报告截图](/Users/Yoson/Desktop/MobileTestNote/%E7%AC%94%E8%AE%B0/%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%B5%8B%E8%AF%95_image/report.png)

拷文件时,如果出现__pycache___文件,把这个文件删了,因为它是一个编译文件,它会自动生成.所以每次运行时,它想自动生成却发现有了,所以会报错.xiang

### Pytest控制函数执行顺序

```
	函数修饰符的方式标记被测试函数执行的顺序.

```

```
	插件名称：pytest-ordering
	安装方式：
		1.安装包方式 python setup.py install 
		2.命令行 pip install pytest-ordering
		pip是通用的python包管理工具,提供了对python包的查找,下载,安装,卸载的功能.xiang
	使用方法：
		1.标记于被测试函数，@pytest.mark.run(order=x)
		2.根据order传入的参数来解决运行顺序
		3.order值全为正数或全为负数时，运行顺序：值越小，优先级越高
		4.正数和负数同时存在：正数优先级高
0>较小的正数>较大的正数>无标记>较小的负数>较大的负数 xiang
```

```
	默认情况下，pytest是根据测试方法名由小到大执行的,可以通过第三方插件包改变其运行顺序。

```

```
	默认执行方式
	示例：
		import pytest
		class TestABC:
		    def setup_class(self):
		        print("------->setup_class")
		    def teardown_class(self):
		        print("------->teardown_class")
		    def test_a(self):
		        print("------->test_a")
		        assert 1
		    def test_b(self):
		        print("------->test_b")
		        assert 0
		if __name__ == '__main__':
		    pytest.main("-s  test_abc.py")
	执行结果：
		test_abc.py 
		------->setup_class
		------->test_a # 默认第一个运行
		.
		------->test_b # 默认第二个运行
		F
		------->teardown_class

```

```
	示例：
		import pytest
		class TestABC:
			def setup_class(self):
				print("------->setup_class")

			def teardown_class(self):
				print("------->teardown_class")
			@pytest.mark.run(order=2)
			def test_a(self):
				print("------->test_a")
				assert 1

			@pytest.mark.run(order=1)
			def test_b(self):
				print("------->test_b")
				assert 0
		if __name__ == '__main__':
				pytest.main("-s  test_abc.py")
	执行结果：
		test_abc.py
		------->setup_class
		------->test_b # order=1 优先运行
		F
		------->test_a # order=2 晚于 order=1 运行
		.
		------->teardown_class


```

### Pytest失败重试

```
	通过命令行方式，控制失败函数的重试次数。

```

```
	插件名称：pytest-rerunfailures
	安装方式：
		1.安装包方式 python setup.py install 
		2.命令行 pip install pytest-rerunfailures
	使用方法：
		命令行格式：pytest --reruns n # n：为重试的次数

```

```
	示例：
	import pytest
	class Test_ABC:
		def setup_class(self):
			print("------->setup_class")
		def teardown_class(self):
			print("------->teardown_class")
		def test_a(self):
			print("------->test_a")
			assert 1
		def test_b(self):
			print("------->test_b")
			assert 0 # 断言失败
	运行方式：
		1.修改Test_App/pytest.ini文件，添加失败重试参数，即：addopts = -s  --reruns 2 --html=./report.html 
			# -s:输出程序运行信息
			# --reruns 2 ：失败测试函数重试两次
			# --html=./report.html 在当前目录下生成report.html文件
		2.命令行进入Test_App目录
		3.执行命令： pytest
	执行结果：
		1.在测试报告中可以看到两次重试记录

```

![失败重试](/Users/Yoson/Desktop/MobileTestNote/%E7%AC%94%E8%AE%B0/%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%B5%8B%E8%AF%95_image/%E9%87%8D%E8%AF%95.png)

```
class TestLogin():
    def test_login1(self):
        num = random.randint(1,5)
        print(num)
        if num == 1:
            print('成功')
            assert True
        else:
            print('失败')
            assert False
```

运行中,如果num==1,就不运行了.如果不是1,则rerun,在n次rerun中,如果num始终不等于 1,则rerun n次,如果在rerun的第m次(m<n),num值等于1,则跳出来,不再rerun.   xiang

## 19.Pytest高阶用法

### 跳过测试函数

```
	根据特定的条件，不执行标识的测试函数.

```

```python
	方法：
		skipif(condition, reason=None)
	参数：
		condition：跳过的条件，必传参数
		reason：标注原因，必传参数
	使用方法：
		@pytest.mark.skipif(condition, reason="xxx")

```

```python
	示例：
		import pytest
		class TestABC:
			def setup_class(self):
				print("------->setup_class")
			def teardown_class(self):
				print("------->teardown_class")
			def test_a(self):
				print("------->test_a")
				assert 1
			@pytest.mark.skipif(condition=2>1,reason = "跳过该函数") # 跳过测试函数test_b
			def test_b(self):
				print("------->test_b")
				assert 0
	执行结果：
		test_abc.py 
		------->setup_class
		------->test_a #只执行了函数test_a
		.
		------->teardown_class
		s # 跳过函数


```

```python
import pytest
class TestLogin:
    @pytest.mark.skipif(True, reason="done")
    def test_login1(self):
        print('被跳过了的')
        assert True
    def test_login2(self):
        print('222')
        assert True
```

输出结果scripts\test_skip.py s222
.



### 标记为预期失败函数

```
	标记测试函数为失败函数


```

```
	方法：
		xfail(condition=None, reason=None, raises=None, run=True, strict=False)
	常用参数：
		condition：预期失败的条件，必传参数
		reason：失败的原因，必传参数
	使用方法：
		@pytest.mark.xfail(condition, reason="xx")

```

```
	示例：
		import pytest
		class TestABC:
			def setup_class(self):
				print("------->setup_class")
			def teardown_class(self):
				print("------->teardown_class")
			def test_a(self):
				print("------->test_a")
				assert 1
			@pytest.mark.xfail(2 > 1, reason="标注为预期失败") # 标记为预期失败函数test_b
			def test_b(self):
				print("------->test_b")
				assert 0
	执行结果：
		test_abc.py 
		------->setup_class
		------->test_a
		.
		------->test_b
		------->teardown_class
		x  # 失败标记


```

### 函数数据参数化

```
	方便测试函数对测试属于的获取。


```

```
	方法：
		parametrize(argnames, argvalues, indirect=False, ids=None, scope=None)
	常用参数：
		argnames：参数名
		argvalues：参数对应值，类型必须为list
					当参数为一个时格式：[value]
					当参数个数大于一个时，格式为:[(param_value1,param_value2.....),(param_value1,param_value2.....)]
	使用方法:
		@pytest.mark.parametrize(argnames,argvalues)
		⚠️ 参数值为N个，测试方法就会运行N次


```

```
	单个参数示例：
		import pytest
		class TestABC:
			def setup_class(self):
				print("------->setup_class")
			def teardown_class(self):
				print("------->teardown_class")

			@pytest.mark.parametrize("a",[3,6]) # a参数被赋予两个值，函数会运行两遍
			def test_a(self,a): # 参数必须和parametrize里面的参数一致
				print("test data:a=%d"%a)
				assert a%3 == 0
	执行结果:
		test_abc.py 
		------->setup_class
		test data:a=3 # 运行第一次取值a=3
		.
		test data:a=6 # 运行第二次取值a=6
		. 
		------->teardown_class


```

```
	多个参数示例：
		import pytest
		class TestABC:
			def setup_class(self):
				print("------->setup_class")
			def teardown_class(self):
				print("------->teardown_class")

			@pytest.mark.parametrize("a,b",[(1,2),(0,3)]) # 参数a,b均被赋予两个值，函数会运行两遍
			def test_a(self,a,b): # 参数必须和parametrize里面的参数一致
				print("test data:a=%d,b=%d"%(a,b))
				assert a+b == 3
	执行结果：
		test_abc.py 
		------->setup_class
		test data:a=1,b=2 # 运行第一次取值 a=1,b=2
		.
		test data:a=0,b=3 # 运行第二次取值 a=0,b=3
		.
		------->teardown_class



```

```
	函数返回值类型示例：
		import pytest
		def return_test_data():
			return [(1,2),(0,3)]
		class TestABC:
			def setup_class(self):
				print("------->setup_class")
			def teardown_class(self):
				print("------->teardown_class")

			@pytest.mark.parametrize("a,b",return_test_data()) # 使用函数返回值的形式传入参数值
			def test_a(self,a,b):
				print("test data:a=%d,b=%d"%(a,b))
				assert a+b == 3
	执行结果：
		test_abc.py 
		------->setup_class
		test data:a=1,b=2 # 运行第一次取值 a=1,b=2
		.
		test data:a=0,b=3 # 运行第二次取值 a=0,b=3
		.
		------->teardown_class



```

```python
import pytest
#coding=utf-8
class TestA:
    @pytest.mark.parametrize(('a','b','c'),[('amy',10,'女'),('lili',2,'女'),('mike',10,'男')])
    #@pytest.mark.parametrize('a, b, c',[('amy',10,'女'),('lili',2,'女'),('mike',10,'男')])
    #参数可以用小括号包起来,每个参数单独用引号,也可以用一个引号把所有参数包起来,并且不用小括号
    def test_A(self,a,b,c):
        print(a,b,c)
        print('*********')
```

输出结果  scripts\test_args2.py amy 10 女

------

.lili 2 女

------

.mike 10 男

------

.

## 20.Pytest-fixture

```
	fixture修饰器来标记固定的工厂函数,在其他函数，模块，类或整个工程调用它时会被激活并优先执行,
		通常会被用于完成预置处理和重复操作。


```

```
	方法：fixture(scope="function", params=None, autouse=False, ids=None, name=None)
	常用参数:
		scope：被标记方法的作用域
			function" (default)：作用于每个测试方法，每个test都运行一次
			"class"：作用于整个类，每个class的所有test只运行一次
			"module"：作用于整个模块，每个module的所有test只运行一次
			"session：作用于整个session(慎用)，每个session只运行一次
		params：(list类型)提供参数数据，供调用标记方法的函数使用
		autouse：是否自动运行,默认为False不运行，设置为True自动运行


```

### fixture(通过参数引用)

```
	示例：
		import pytest
		class TestABC:
		    @pytest.fixture()
		    def before(self):
		        print("------->before")
		    def test_a(self,before): # ⚠️ test_a方法传入了被fixture标识的函数，已变量的形式
		        print("------->test_a")
		        assert 1
		if __name__ == '__main__':
		    pytest.main("-s  test_abc.py")


```

```
	执行结果：
		test_abc.py 
		------->before # 发现before会优先于测试函数运行
		------->test_a
		.  


```

### fixture(通过函数引用)

```
	示例：
		import pytest
		@pytest.fixture() # fixture标记的函数可以应用于测试类外部
		def before():
		    print("------->before")
		@pytest.mark.usefixtures("before")
		class TestABC:
		    def setup(self):
		        print("------->setup")
		    def test_a(self):
		        print("------->test_a")
		        assert 1
		if __name__ == '__main__':
		    pytest.main("-s  test_abc.py")


```

```
	执行结果：
		test_abc.py 
		------->before # 发现before会优先于测试类运行
		------->setup
		------->test_a
		.


```

### fixture(默认设置为运行)

```
	示例：
		import pytest
		@pytest.fixture(autouse=True) # 设置为默认运行
		def before():
		    print("------->before")
		class TestABC:
		    def setup(self):
		        print("------->setup")
		    def test_a(self):
		        print("------->test_a")
		        assert 1
		if __name__ == '__main__':
		    pytest.main("-s  test_abc.py")


```

```
	执行结果：
		test_abc.py 
		------->before # 发现before自动优先于测试类运行
		------->setup
		------->test_a
		.


```

### fixture(作用域为function)

```
	示例：
		import pytest
		@pytest.fixture(scope='function',autouse=True) # 作用域设置为function，自动运行
		def before():
		    print("------->before")
		class TestABC:
		    def setup(self):
		        print("------->setup")
		    def test_a(self):
		        print("------->test_a")
		        assert 1
		    def test_b(self):
		        print("------->test_b")
		        assert 1
		if __name__ == '__main__':
		    pytest.main("-s  test_abc.py")


```

```
	执行结果：
		test_abc.py
		------->before # 运行第一次
		------->setup
		------->test_a
		.------->before # 运行第二次
		------->setup
		------->test_b
		.


```

### fixture(作用域为class)

```
	示例：
		import pytest
		@pytest.fixture(scope='class',autouse=True) # 作用域设置为class，自动运行
		def before():
		    print("------->before")
		class TestABC:
		    def setup(self):
		        print("------->setup")
		    def test_a(self):
		        print("------->test_a")
		        assert 1
		    def test_b(self):
		        print("------->test_b")
		        assert 1
		if __name__ == '__main__':
		    pytest.main("-s  test_abc.py")


```

```
	执行结果：
		test_abc.py
		------->before # 发现只运行一次
		------->setup
		------->test_a
		.
		------->setup
		------->test_b
		.


```

### fixture(返回值)

```
	示例一:
		import pytest
		@pytest.fixture()
		def need_data():
		    return 2 # 返回数字2

		class TestABC:
		    def test_a(self,need_data):
		        print("------->test_a")
		        assert need_data != 3 # 拿到返回值做一次断言

		if __name__ == '__main__':
		    pytest.main("-s  test_abc.py")
	执行结果：
		test_abc.py 
		------->test_a
		.  


```

```
	示例二:
		import pytest
		@pytest.fixture(params=[1, 2, 3])
		def need_data(request): # 传入参数request 系统封装参数
		    return request.param # 取列表中单个值，默认的取值方式

		class TestABC:

		    def test_a(self,need_data):
		        print("------->test_a")
		        assert need_data != 3 # 断言need_data不等于3

		if __name__ == '__main__':
		    pytest.main("-s  test_abc.py")
	执行结果：
		# 可以发现结果运行了三次
		test_abc.py 
		1
		------->test_a
		.
		2
		------->test_a
		.
		3
		------->test_a
		F 


```

## 21.PO模式

### Page Object Model

```
	测试页面和测试脚本分离，即页面封装成类，供测试脚本进行调用。


```

### 优缺点

- 优点

```
	1.提高测试用例的可读性;
	2.减少了代码的重复;
	3.提高测试用例的可维护性，特别是针对UI频繁变动的项目;


```

- 缺点

```
	结构复杂: 基于流程做了模块化的拆分。


```

![po模式](/Users/Yoson/Desktop/MobileTestNote/%E7%AC%94%E8%AE%B0/%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%B5%8B%E8%AF%95_image/po&%E9%9D%9E.png)



## 22.项目准备

### 需求

- 更多-移动网络-首选网络类型-点击2G
- 更多-移动网络-首选网络类型-点击3G
- 显示-搜索按钮-输入hello-点击返回

### 文件目录

```
PO模式
- scripts
- - test_settting.py
- pytest.ini


```

### 代码

test_setting.py

```
import time
from appium import webdriver


class TestSetting:

    def setup(self):
        # server 启动参数
        desired_caps = {}
        # 设备信息
        desired_caps['platformName'] = 'Android'
        desired_caps['platformVersion'] = '5.1'
        desired_caps['deviceName'] = '192.168.56.101:5555'
        # app的信息
        desired_caps['appPackage'] = 'com.android.settings'
        desired_caps['appActivity'] = '.Settings'
        # 解决输入中文
        desired_caps['unicodeKeyboard'] = True
        desired_caps['resetKeyboard'] = True

        # 声明我们的driver对象
        self.driver = webdriver.Remote('http://127.0.0.1:4723/wd/hub', desired_caps)

    def test_mobile_network_2g(self):
        self.driver.find_element_by_xpath("//*[contains(@text,'更多')]").click()
        self.driver.find_element_by_xpath("//*[contains(@text,'移动网络')]").click()
        self.driver.find_element_by_xpath("//*[contains(@text,'首选网络类型')]").click()
        self.driver.find_element_by_xpath("//*[contains(@text,'2G')]").click()

    def test_mobile_network_3g(self):
        self.driver.find_element_by_xpath("//*[contains(@text,'更多')]").click()
        self.driver.find_element_by_xpath("//*[contains(@text,'移动网络')]").click()
        self.driver.find_element_by_xpath("//*[contains(@text,'首选网络类型')]").click()
        self.driver.find_element_by_xpath("//*[contains(@text,'3G')]").click()

    def test_mobile_display_input(self):
        self.driver.find_element_by_xpath("//*[contains(@text,'显示')]").click()
        self.driver.find_element_by_id("com.android.settings:id/search").click()
        self.driver.find_element_by_id("android:id/search_src_text").send_keys("hello")
        self.driver.find_element_by_class_name("android.widget.ImageButton").click()

    def teardown(self):
        self.driver.quit()


```

pytest.ini

```
[pytest]
# 添加行参数
addopts = -s --html=./report/report.html
# 文件搜索路径
testpaths = ./scripts
# 文件名称
python_files = test_*.py
# 类名称
python_classes = Test*
# 方法名称
python_functions = test_*


```

## 23.多文件区分测试用例

### 需求

- 使用多个文件来区分不同的测试页面

### 好处

- 修改不同的功能找对应的文件即可

### 步骤

1. 在scripts下新建test_network.py文件
2. 在scripts下新建test_dispaly.py文件
3. 移动不同的功能代码到对应的文件
4. 移除原有的test_setting.py文件

### 文件目录

```
PO模式
- scripts
- - test_network.py
- - test_dispaly.py
- pytest.ini


```

### 代码

test_network.py

```
from appium import webdriver


class TestNetwork:

    def setup(self):
        # server 启动参数
        desired_caps = {}
        # 设备信息
        desired_caps['platformName'] = 'Android'
        desired_caps['platformVersion'] = '5.1'
        desired_caps['deviceName'] = '192.168.56.101:5555'
        # app的信息
        desired_caps['appPackage'] = 'com.android.settings'
        desired_caps['appActivity'] = '.Settings'
        # 解决输入中文
        desired_caps['unicodeKeyboard'] = True
        desired_caps['resetKeyboard'] = True

        # 声明我们的driver对象
        self.driver = webdriver.Remote('http://127.0.0.1:4723/wd/hub', desired_caps)

    def test_mobile_network_2g(self):
        self.driver.find_element_by_xpath("//*[contains(@text,'更多')]").click()
        self.driver.find_element_by_xpath("//*[contains(@text,'移动网络')]").click()
        self.driver.find_element_by_xpath("//*[contains(@text,'首选网络类型')]").click()
        self.driver.find_element_by_xpath("//*[contains(@text,'2G')]").click()

    def test_mobile_network_3g(self):
        self.driver.find_element_by_xpath("//*[contains(@text,'更多')]").click()
        self.driver.find_element_by_xpath("//*[contains(@text,'移动网络')]").click()
        self.driver.find_element_by_xpath("//*[contains(@text,'首选网络类型')]").click()
        self.driver.find_element_by_xpath("//*[contains(@text,'3G')]").click()

    def teardown(self):
        self.driver.quit()


```

test_dispaly.py

```
from appium import webdriver


class TestDisplay:

    def setup(self):
        # server 启动参数
        desired_caps = {}
        # 设备信息
        desired_caps['platformName'] = 'Android'
        desired_caps['platformVersion'] = '5.1'
        desired_caps['deviceName'] = '192.168.56.101:5555'
        # app的信息
        desired_caps['appPackage'] = 'com.android.settings'
        desired_caps['appActivity'] = '.Settings'
        # 解决输入中文
        desired_caps['unicodeKeyboard'] = True
        desired_caps['resetKeyboard'] = True

        # 声明我们的driver对象
        self.driver = webdriver.Remote('http://127.0.0.1:4723/wd/hub', desired_caps)

    def test_mobile_display_input(self):
        self.driver.find_element_by_xpath("//*[contains(@text,'显示')]").click()
        self.driver.find_element_by_id("com.android.settings:id/search").click()
        self.driver.find_element_by_id("android:id/search_src_text").send_keys("hello")
        self.driver.find_element_by_class_name("android.widget.ImageButton").click()

    def teardown(self):
        self.driver.quit()


```

### 出现no module named "xx",解决方法:导包

### import os, sys

### sys.path.append(os.getcwd())

### 但我加进去依然不起作用!!!!xiang

## 23.封装前置代码

### 需求

- 将前置代码进行封装

### 好处

- 前置代码只需要写一份

### 步骤

1. 新建base文件夹
2. 新建base_driver.py文件
3. 新建函数init_driver
4. 写入前置代码并返回
5. 修改测试文件中的代码

### 文件目录

```
PO模式
- base
- - base_driver.py
- scripts
- - test_network.py
- - test_dispaly.py
- pytest.ini


```

### 代码

base_driver.py

```
from appium import webdriver

def init_driver():
    # server 启动参数
    desired_caps = {}
    # 设备信息
    desired_caps['platformName'] = 'Android'
    desired_caps['platformVersion'] = '5.1'
    desired_caps['deviceName'] = '192.168.56.101:5555'
    # app的信息
    desired_caps['appPackage'] = 'com.android.settings'
    desired_caps['appActivity'] = '.Settings'
    # 解决输入中文
    desired_caps['unicodeKeyboard'] = True
    desired_caps['resetKeyboard'] = True

    # 声明我们的driver对象
    return webdriver.Remote('http://127.0.0.1:4723/wd/hub', desired_caps)


```

test_network.py

```
from base.base_driver import init_driver


class TestNetwork:

    def setup(self):
        self.driver = init_driver()

    def test_mobile_network_2g(self):
        self.driver.find_element_by_xpath("//*[contains(@text,'更多')]").click()
        self.driver.find_element_by_xpath("//*[contains(@text,'移动网络')]").click()
        self.driver.find_element_by_xpath("//*[contains(@text,'首选网络类型')]").click()
        self.driver.find_element_by_xpath("//*[contains(@text,'2G')]").click()

    def test_mobile_network_3g(self):
        self.driver.find_element_by_xpath("//*[contains(@text,'更多')]").click()
        self.driver.find_element_by_xpath("//*[contains(@text,'移动网络')]").click()
        self.driver.find_element_by_xpath("//*[contains(@text,'首选网络类型')]").click()
        self.driver.find_element_by_xpath("//*[contains(@text,'3G')]").click()

    def teardown(self):
        self.driver.quit()


```

test_dispaly.py

```
from base.base_driver import init_driver


class TestDisplay:

    def setup(self):
        self.driver = init_driver()

    def test_mobile_display_input(self):
        self.driver.find_element_by_xpath("//*[contains(@text,'显示')]").click()
        self.driver.find_element_by_id("com.android.settings:id/search").click()
        self.driver.find_element_by_id("android:id/search_src_text").send_keys("hello")
        self.driver.find_element_by_class_name("android.widget.ImageButton").click()

    def teardown(self):
        self.driver.quit()



```

总结:新建一个base文件夹,创建一个base_driver.py文件,把前置代码写入一个函数.return  webdriver对象.以后只要调用这个函数,它就会自动连接appium服务器---连接手机----把前置代码的参数传给手机.

测试文件,导入base_driver.py的init_driver,即from base.base_driver import init_driver,

setup职责是调用init_driver()函数,即self.driver = init_driver()

剩下的是测试方法. xiang

## 24.分离测试脚本

### 需求

- 测试脚本只剩流程
- 其他的步骤放倒page中

### 好处

- 测试脚本只专注过程
- 过程改变只需要修改脚本

### 步骤

1. 新建page文件夹
2. 新建network_page.py文件
3. 新建display_page.py文件
4. init函数传入driver
5. init进入需要测试的页面
6. page中新建“小动作”函数
7. 移动代码
8. 修改测试文件中的代码

### 文件目录

```
PO模式
- base
- - base_driver.py
- page
- - network_page.py
- - display_page.py
- scripts
- - test_network.py
- - test_dispaly.py
- pytest.ini


```

### 代码

base_driver.py

```
from appium import webdriver

def init_driver():
    # server 启动参数
    desired_caps = {}
    # 设备信息
    desired_caps['platformName'] = 'Android'
    desired_caps['platformVersion'] = '5.1'
    desired_caps['deviceName'] = '192.168.56.101:5555'
    # app的信息
    desired_caps['appPackage'] = 'com.android.settings'
    desired_caps['appActivity'] = '.Settings'
    # 解决输入中文
    desired_caps['unicodeKeyboard'] = True
    desired_caps['resetKeyboard'] = True

    # 声明我们的driver对象
    return webdriver.Remote('http://127.0.0.1:4723/wd/hub', desired_caps)


```

network_page.py

```
class NetWorkPage:

    def __init__(self, driver):
        self.driver = driver
        self.driver.find_element_by_xpath("//*[contains(@text,'更多')]").click()
        self.driver.find_element_by_xpath("//*[contains(@text,'移动网络')]").click()

    def click_first_network(self):
        self.driver.find_element_by_xpath("//*[contains(@text,'首选网络类型')]").click()

    def click_2g(self):
        self.driver.find_element_by_xpath("//*[contains(@text,'2G')]").click()
        
    def click_3g(self):
        self.driver.find_element_by_xpath("//*[contains(@text,'3G')]").click()


```

display_page.py

```
class DisplayPage:

    def __init__(self, driver):
        self.driver = driver
        self.driver.find_element_by_xpath("//*[contains(@text,'显示')]").click()

    def click_search(self):
        self.driver.find_element_by_id("com.android.settings:id/search").click()

    def input_text(self, text):
        self.driver.find_element_by_id("android:id/search_src_text").send_keys(text)

    def click_back(self):
        self.driver.find_element_by_class_name("android.widget.ImageButton").click()


```

test_network.py

```
import sys, os
sys.path.append(os.getcwd())

from base.base_driver import init_driver
from page.network_page import NetWorkPage


class TestNetwork:

    def setup(self):
        self.driver = init_driver()
        self.network_page = NetWorkPage(self.driver)

    def test_mobile_network_2g(self):
        self.network_page.click_first_network()
        self.network_page.click_2g()

    def test_mobile_network_3g(self):
        self.network_page.click_first_network()
        self.network_page.click_3g()

    def teardown(self):
        self.driver.quit()


```

test_dispaly.py

```
import sys, os
sys.path.append(os.getcwd())


from base.base_driver import init_driver
from page.display_page import DisplayPage


class TestDisplay:

    def setup(self):
        self.driver = init_driver()
        self.display_page = DisplayPage(self.driver)

    def test_mobile_display_input(self):
        self.display_page.click_search()
        self.display_page.input_text("hello")
        self.display_page.click_back()

    def teardown(self):
        self.driver.quit()


```

总结:凡是涉及到被测页面的内容改了,找page.  操作步骤变了,找script.

script关注的是先干什么,再干什么,只关注的是流程.page关注的是每一步是怎么操作(怎么找元素等,)

页面的init里面可以写已经确定的这个模块所有的前置功能

## 25.抽取找元素的特征

### 需求

- 将元素的特城放在函数之上

### 好处

- 若特征改了，流程不变，可以直接在上面修改

### 步骤

1. 将find_element_by_xxx改为find_element
2. 将方式和具体特征向上移动

### 文件目录

```
PO模式
- base
- - base_driver.py
- page
- - network_page.py
- - display_page.py
- scripts
- - test_network.py
- - test_dispaly.py
- pytest.ini


```

### 代码

base_driver.py

```
from appium import webdriver

def init_driver():
    # server 启动参数
    desired_caps = {}
    # 设备信息
    desired_caps['platformName'] = 'Android'
    desired_caps['platformVersion'] = '5.1'
    desired_caps['deviceName'] = '192.168.56.101:5555'
    # app的信息
    desired_caps['appPackage'] = 'com.android.settings'
    desired_caps['appActivity'] = '.Settings'
    # 解决输入中文
    desired_caps['unicodeKeyboard'] = True
    desired_caps['resetKeyboard'] = True

    # 声明我们的driver对象
    return webdriver.Remote('http://127.0.0.1:4723/wd/hub', desired_caps)



```

network_page.py

```
from selenium.webdriver.common.by import By


class NetWorkPage:

    more_button = By.XPATH, "//*[contains(@text,'更多')]"
    mobile_network_button = By.XPATH, "//*[contains(@text,'移动网络')]"
    click_first_network_button = By.XPATH, "//*[contains(@text,'首选网络类型')]"
    network_2g_button = By.XPATH, "//*[contains(@text,'2G')]"
    network_3g_button = By.XPATH, "//*[contains(@text,'3G')]"

    def __init__(self, driver):
        self.driver = driver
        self.driver.find_element(self.more_button).click()
        self.driver.find_element(self.mobile_network_button).click()

    def click_first_network(self):
        self.driver.find_element(self.click_first_network_button).click()

    def click_2g(self):
        self.driver.find_element(self.network_2g_button).click()

    def click_3g(self):
        self.driver.find_element(self.network_3g_button).click()


```

display_page.py

```
from selenium.webdriver.common.by import By


class DisplayPage:

    display_button = By.XPATH, "//*[contains(@text,'显示')]"
    search_button = By.ID, "com.android.settings:id/search"
    search_edit_text = By.ID, "android:id/search_src_text"
    back_button = By.CLASS_NAME, "android.widget.ImageButton"

    def __init__(self, driver):
        self.driver = driver
        self.driver.find_element(self.display_button).click()

    def click_search(self):
        self.driver.find_element(self.search_button).click()

    def input_text(self, text):
        self.driver.find_element(self.search_edit_text).send_keys(text)

    def click_back(self):
        self.driver.find_element(self.back_button).click()


```

test_network.py

```
import sys, os
sys.path.append(os.getcwd())

from base.base_driver import init_driver
from page.network_page import NetWorkPage


class TestNetwork:

    def setup(self):
        self.driver = init_driver()
        self.network_page = NetWorkPage(self.driver)

    def test_mobile_network_2g(self):
        self.network_page.click_first_network()
        self.network_page.click_2g()

    def test_mobile_network_3g(self):
        self.network_page.click_first_network()
        self.network_page.click_3g()

    def teardown(self):
        self.driver.quit()


```

test_dispaly.py

```
import sys, os
sys.path.append(os.getcwd())


from base.base_driver import init_driver
from page.display_page import DisplayPage


class TestDisplay:

    def setup(self):
        self.driver = init_driver()
        self.display_page = DisplayPage(self.driver)

    def test_mobile_display_input(self):
        self.display_page.click_search()
        self.display_page.input_text("hello")
        self.display_page.click_back()

    def teardown(self):
        self.driver.quit()


```



## 26.抽取action

### 需求

- 将动作进行封装

### 步骤

1. 新建base_action.py文件
2. 将click、send_keys抽取到文件中

### 文件目录

```
PO模式
- base
- - base_driver.py
- - base_action.py
- page
- - network_page.py
- - display_page.py
- scripts
- - test_network.py
- - test_dispaly.py
- pytest.ini


```

### 代码

base_action.py

```
class BaseAction:

    def __init__(self, driver):
        self.driver = driver

    def click(self, loc):
        self.driver.find_element(loc[0], loc[1]).click()

    def input(self, loc, text):
        self.driver.find_element(loc[0], loc[1]).send_keys(text)


```

network_page.py

```
import sys, os
sys.path.append(os.getcwd())

from selenium.webdriver.common.by import By
from base.base_action import BaseAction


class NetWorkPage(BaseAction):

    more_button = By.XPATH, "//*[contains(@text,'更多')]"
    mobile_network_button = By.XPATH, "//*[contains(@text,'移动网络')]"
    click_first_network_button = By.XPATH, "//*[contains(@text,'首选网络类型')]"
    network_2g_button = By.XPATH, "//*[contains(@text,'2G')]"
    network_3g_button = By.XPATH, "//*[contains(@text,'3G')]"

    def __init__(self, driver):
        BaseAction.__init__(self, driver)
        self.click(self.more_button)
        self.click(self.mobile_network_button)

    def click_first_network(self):
        self.click(self.click_first_network_button)

    def click_2g(self):
        self.click(self.network_2g_button)

    def click_3g(self):
        self.click(self.network_3g_button)


```

display_page.py

```
import sys, os
sys.path.append(os.getcwd())

from selenium.webdriver.common.by import By
from base.base_action import BaseAction


class DisplayPage(BaseAction):

    display_button = By.XPATH, "//*[contains(@text,'显示')]"
    search_button = By.ID, "com.android.settings:id/search"
    search_edit_text = By.ID, "android:id/search_src_text"
    back_button = By.CLASS_NAME, "android.widget.ImageButton"

    def __init__(self, driver):
        BaseAction.__init__(self, driver)
        self.click(self.display_button)

    def click_search(self):
        self.click(self.search_button)

    def input_text(self, text):
        self.input(self.search_edit_text, text)

    def click_back(self):
        self.click(self.back_button)


```

test_network.py

```
import sys, os
sys.path.append(os.getcwd())

from base.base_driver import init_driver
from page.network_page import NetWorkPage


class TestNetwork:

    def setup(self):
        self.driver = init_driver()
        self.network_page = NetWorkPage(self.driver)

    def test_mobile_network_2g(self):
        self.network_page.click_first_network()
        self.network_page.click_2g()

    def test_mobile_network_3g(self):
        self.network_page.click_first_network()
        self.network_page.click_3g()

    def teardown(self):
        self.driver.quit()


```

test_dispaly.py

```
import sys, os

import time

sys.path.append(os.getcwd())

from base.base_driver import init_driver
from page.display_page import DisplayPage


class TestDisplay:

    def setup(self):
        self.driver = init_driver()
        self.display_page = DisplayPage(self.driver)

    def test_mobile_display_input(self):
        self.display_page.click_search()
        self.display_page.input_text("hello")
        self.display_page.click_back()
        pass

    def teardown(self):
        self.driver.quit()


```

## 27.增加WebDriverWait

### 需求

- 找控件使用WebDriverWait
- 所有的找控件,都应该增加WebDriverWait.  xiang

### 好处

- 防止出现cpu卡的时候找不到

### 步骤

1. 自己新建find方法
2. 在系统的基础上增加WebDriverWait

### 文件目录

```
PO模式
- base
- - base_driver.py
- - base_action.py
- page
- - network_page.py
- - display_page.py
- scripts
- - test_network.py
- - test_dispaly.py
- pytest.ini


```

### 代码

base_action.py

```
from selenium.webdriver.support.wait import WebDriverWait


class BaseAction:

    def __init__(self, driver):
        self.driver = driver

    def find_element(self, loc, time=10, poll=1):
        return WebDriverWait(self.driver, time, poll).until(lambda x: x.find_element(loc[0], loc[1]))
        # return self.driver.find_element(by, value)

    def find_elements(self, loc, time=10, poll=1):
        return WebDriverWait(self.driver, time, poll).until(lambda x: x.find_elements(loc[0], loc[1]))
        # return self.driver.find_elements(by, value)

    def click(self, loc):
        self.find_element(loc).click()

    def input(self, loc, text):
        self.find_element(loc).send_keys(text)



```

## 28.xpath特殊处理

### 需求

- //*[contains(@,'')]是相同的可以进行抽取

### 好处

- 少写代码

### 步骤

1. 获取loc后，进行拆分
2. 字符串拼接

### 文件目录

```
PO模式
- base
- - base_driver.py
- - base_action.py
- page
- - network_page.py
- - display_page.py
- scripts
- - test_network.py
- - test_dispaly.py
- pytest.ini


```

### 代码

base_action.py

```
from selenium.webdriver.common.by import By
from selenium.webdriver.support.wait import WebDriverWait


class BaseAction:

    def __init__(self, driver):
        self.driver = driver

    def find_element(self, loc, time=10, poll=0.5):
        loc_by, loc_value = loc
        if loc_by == By.XPATH:
            xpath_key, xpath_value = loc_value
            loc_value = "//*[contains(@%s, '%s')]" % (xpath_key, xpath_value)
        return WebDriverWait(self.driver, time, poll).until(lambda x: x.find_element(loc_by, loc_value))

    def find_elements(self, loc, time=10, poll=0.5):
        loc_by, loc_value = loc
        if loc_by == By.XPATH:
            xpath_key, xpath_value = loc_value
            loc_value = "//*[contains(@%s, '%s')]" % (xpath_key, xpath_value)
        return WebDriverWait(self.driver, time, poll).until(lambda x: x.find_elements(loc_by, loc_value))

    def click(self, loc):
        self.find_element(loc).click()

    def input(self, loc, text):
        self.find_element(loc).send_keys(text)



```



## 29.Yaml数据存储文件

```
	YAML 是一种所有编程语言可用的友好的数据序列化标准,语法和其他高阶语言类似，并且可以简单表达清单、散列表，标量等资料形态.


```

- 语法规则

```
	1.大小写敏感
	2.使用缩进表示层级关系
	3.缩进时不允许使用Tab键，只允许使用空格。(在pycharm中,tab键会自动转化成空格xiang)
	4.缩进的空格数目不重要，只要相同层级的元素左侧对齐即可



```

- 支持的数据结构

```
	1.对象：键值对的集合，又称为映射（mapping）/ 哈希（hashes） / 字典（dictionary）
	2.数组：一组按次序排列的值，又称为序列（sequence） / 列表（list）
	3.纯量（scalars）：单个的、不可再分的值


```

- 1.对象

  - 值为字符

  ```
  	data.yaml
  	 animal: pets

  	转换为python代码
  	 {'animal': 'pets'}
  ```


  ```

  - 值为字典

  ```
  	data.yaml
  	 animal: {"ke1":"pets","key2":"app"} # python字典

  	转换为python代码
  	 {animal: {"ke1":"pets","key2":"app"}} # 嵌套字典结构


  ```

- 2.数组

  - 方式一

  ```
  	data.yaml
  	 animal: 
  	   - data1
  	   - data2
  	转换为python代码
  	 {'animal': ['data1', 'data2']}



  ```

  - 方式二

  ```
  	data.yaml
  	 animal: ['data1', 'data2'] # python列表

  	转换为python代码
  	 {'animal': ['data1', 'data2']} # 字典嵌套列表


  ```

- 纯量

  ```
	包含：字符串，布尔值，整数，浮点数，Null，日期


```

```
	字符串
	data.yaml
	 value: "hello"
	
	转换为python代码
	 {"value":"hello"}


```

```
	布尔值
	data.yaml
	 value1: true
	 value2: false
	
	转换为python代码
	 {'value1': True, 'value2': False}


```

```
	整数，浮点数
	data.yaml
	 value1: 12
	 value2: 12.102
	
	转换为python代码
	 {'value1': 12, 'value2': 12.102}
	
	空(Null)
	data.yaml
	 value1: ~ # ~ 表示为空
	转换为python代码
	 {'value1': None}
	
	日期
	data.yaml
	 value1: 2017-10-11 15:12:12
	转换为python代码
	 {'languages': {'value1': datetime.datetime(2017, 10, 11, 15, 12, 12)}}



```
- 锚点&和引用*

```
	锚点：标注一个内容，锚点名称自定义
	引用：使用被标注的内容<<:
	
	data.yaml
	  data: &imp
	  value: 456
	name:
	  value1: 123
	  <<: *imp # "<<:" 合并到当前位置，"*imp" 引用锚点imp
	转换为python代码
	 {'data': {'value': 456}, 'name': {'value': 456, 'value1': 123}}

### 30.Python解析yaml文件

- PyYAML库安装

	PyYAML为python解析yaml的库
	安装：pip install -U PyYAML


- yaml文件内容

	Search_Data:
	  search_test_001:
	    value: 456
	    expect: [4,5,6]
	  search_test_002:
	    value: "你好"
	    expect: {"value":"你好"}


- 读取yaml文件

  - 方法

  	yaml.load(stream, Loader=Loader)
  	参数：
  		stream：待读取文件对象


```
示例：
  		import yaml
  		with open("../Data/search_page.yaml",'r') as f:
  		    data = yaml.load(f)
  		    print(type(data)) # 打印data类型
  		    print(data) # 打印data返回值

  	执行结果：
  		<class 'dict'>
  		{'Search_Data': {
  			'search_test_002': {'expect': {'value': '你好'}, 'value': '你好'}, 
  			'search_test_001': {'expect': [4, 5, 6], 'value': 456}}}


```


- 写入yaml文件内容

	{'Search_Data': {
				'search_test_002': {'expect': {'value': '你好'}, 'value': '你好'}, 
				'search_test_001': {'expect': [4, 5, 6], 'value': 456}}}


- 写yaml文件

  - 方法


```
yaml.dump(data,stream,**kwds)
  	常用参数：
  		data：写入数据类型为字典
  		stream：打开文件对象
  		encoding='utf-8' # 设置写入编码格式
  		allow_unicode=True # 是否允许unicode编码
```

```
	示例：不设置编码格式
  		import yaml
  		data = {'Search_Data': {
  						'search_test_002': {'expect': {'value': '你好'}, 'value': '你好'},
  						'search_test_001': {'expect': [4, 5, 6], 'value': 456}}
  		with open("./text.yaml","w") as f: # 在当前目录下生成text.yaml文件，若文件存在直接更新内容
  		    yaml.dump(data,f)
  	执行结果：
  		1.当前目录生成text.yaml文件
  		2.文件内容：
  			Search_Data:
  			  search_test_001:
  			    expect: [4, 5, 6]
  			    value: 456
  			  search_test_002:
  			    expect: {value: "\u4F60\u597D"} # 中文出现乱码
  			    value: "\u4F60\u597D" # 中文出现乱码


```

```
示例：设置编码格式
  		import yaml
  		data = {'Search_Data': {
  						'search_test_002': {'expect': {'value': '你好'}, 'value': '你好'},
  						'search_test_001': {'expect': [4, 5, 6], 'value': 456}}
  		with open("./text.yaml","w") as f: # 在当前目录下生成text.yaml文件，若文件存在直接更新内容
  		    yaml.dump(data,f, encoding='utf-8', allow_unicode=True)
  	执行结果：
  		1.当前目录生成text.yaml文件
  		2.文件内容：
  			Search_Data:
  			  search_test_001:
  			    expect: [4, 5, 6]
  			    value: 456
  			  search_test_002:
  			    expect: {value: 你好} # 中文未出现乱码
  			    value: 你好 # 中文未出现乱码
```




## 31.Yaml数据驱动应用

目标集成Pytest完成测试任务


- 测试项目

业务：
​	1.进入设置点击搜索按钮
​	2.输入搜索内容
​	3.点击返回


- 目录结构

		App_Project # 项目名称
		  - Basic # 存储基础设施类
		  	- __init__.py # 空文件
		  	- Init_Driver.py # 手机驱动对象初始化
		  	- Base.py # 方法的二次封装
		  	- read_data.py #数据解析读取方法
		  - Page # 存储封装页面文件
		  	- __init__.py # 存储页面元素
		  	- search_page.py # 封装页面元素的操作方法
		  - Data # 存储数据文件
		  	- search_data.yaml(也可以是其他文件比如txt，excel，json，数据库等)
		  - Test # 存储测试脚本目录
		  	- test_search.py # 测试搜索文件
		  - pytest.ini # pytest运行配置文件


- 前置条件

	1.手机驱动对象独立 # 见PO章节代码
	2.方法的二次封装 # 见PO章节代码
	3.完成页面的封装 # 见PO章节代码


- 待完成任务

	1.编写数据驱动文件search_data.yaml
	2.编写解析yaml文件类/方法
	3.编写测试脚本


- 编写search_data.yaml

	search_test_001: # 用例编号
	  input_text: "你好" # 测试输入数据
	search_test_002:
	  input_text: "1234"
	search_test_003:
	  input_text: "*&^%"


- 编写解析yaml方法

	read_data.py

	import yaml,os
	class Read_Data:
	    def __init__(self,file_name):
	        '''
	        	使用pytest运行在项目的根目录下运行，即App_Project目录
	        	期望路径为：项目所在目录/App_Project/Data/file_name
	        '''
	        self.file_path = os.getcwd() + os.sep + "Data" + os.sep + file_name 
	    def return_data(self):
	        with open(self.file_path,'r') as f:
	            data = yaml.load(f) # 读取文件内容
	            return data
	    
	    # data:{"search_test_001":{"input_text": "你好"},"search_test_002":{"input_text": "1234"},"search_test_003":{"input_text": "*&^%"}}




- 测试脚本编写

	test_search.py

	import sys,os
	# 因为需要在项目的根目录下运行，所以需要添加python包搜索路径
	# pytest命令运行路径：App_Project目录下
	# os.getcwd(): App_Project所在目录/App_Project
	sys.path.append(os.getcwd())
	
	# 导入封装好的页面类
	from Page.search_page import Search_Page
	# 导入独立的手机驱动对象
	from Basic.Init_Driver import init_driver
	from Basic.read_data import Read_Data
	import pytest
	def package_param_data():
	    list_data = [] # 存储参数值列表，格式[(用例编号1,输入内容2),(用例编号1,输入内容2)...]
	    yaml_data = Read_Data("search_data.yaml").return_data() # 返回yaml文件读取数据
	    for i in yaml_data.keys():
	        list_data.append((i,yaml_data.get(i).get('input_text'))) # list_data中添加参数值
	    return list_data
	
	class Test_Search:
		'''
			我们希望测试函数运行多次，不希望每运行一次做一次初始化和退出，
			所以使用setup_class，teardown_class，
			测试类内只运行一次初始化和结束动作.
		'''
		def setup_class(self):
		    self.driver = init_driver()
		
		@pytest.mark.parametrize('test_id,input_text',package_param_data()) # 参数传递三组参数，会运行三次
		def test_search(self,test_id,input_text):
		    # 示例化页面封装类
		    sp = Search_Page(self.driver)
		    # 调用操作类
		    print("test_id:",test_id)
		    sp.input_search_text(input_text)
		    # 退出driver对象
		
		def teardown_class(self):
		    self.driver.quit()


```python
demo.py

import yaml
def yaml_data_with_file(file_name):
    with open("./" + file_name + '.yml', 'r') as f:
        return yaml.load(f)
    
def data_with_key(key):
    return yaml_data_with_file('data')[key]
	case_data_list = list()
    for case_data in data.values():
        case_data_list.append(case_data)

class TestLogin:
def test_login2(self):
	#data = data_with_key('test_login2')
    data = yaml_data_with_file('data')['test_login2']
    
 在另一个存储数据的.yml文件中
test_login2:
   test_login2_001:
    	username: "maxx"
         password: 123
     test_login2_002:
    	username: " maxx"
         password: 123       
```



- pytest的配置文件

	pytest.ini

	[pytest]
	addopts = -s  --html=./report.html
	# 测试路径
	testpaths = ./Test
	# 测试文件名
	python_files = test_*.py
	# 测试类名
	python_classes = Test_*
	# 测试的方法名
	python_functions = test_*


- 项目运行

	1.启动appium 服务：地址 127.0.0.1 端口 4723
	2.启动模拟器
	3.进入项目根目录:App_Project
	4.命令行输入pytest运行测试


- 测试报告
  ![search报告](/Users/Yoson/Desktop/MobileTestNote/%E7%AC%94%E8%AE%B0/%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%B5%8B%E8%AF%95_image/search%E6%8A%A5%E5%91%8A.png)

## 32.Allure报告

### Allure介绍

	Allure是一个独立的报告插件，生成美观易读的报告，目前支持语言：Java, PHP, Ruby, Python, Scala, C#。



### Allure安装

1.安装pytest的插件包pytest-allure-adaptor: pip install pytest-allure-adaptor

上述老师安装的方法会报错,因为pytest-allure-adaptor库基本被python3放弃了，运行很不友好.解决方法:
先卸载：pip uninstall pytest-allure-adaptor
再安装：pip install allure-pytest




### Allure帮助文档

	https://docs.qameta.io/allure/#_about



### 生成Allure报告

命令行参数：pytest --alluredir report  # 在执行命令目录生成report文件夹，文件夹下包含xml文件




- 示例

	pytest.ini

	[pytest]
	;--html=./report.html
	;删除原生html，增加Allure
	addopts = -s --alluredir report
	# 测试路径
	testpaths = ./Test
	# 测试文件名
	python_files = test_*.py
	# 测试类名
	python_classes = Test_*
	# 测试的方法名
	python_functions = test_*


```

```
	test_all.py

	class Test_allure:
	    def setup(self):
	        pass
	    def teardown(self):
	        pass
	    def test_al(self):
	        assert 0


```

```
操作步骤：
​	1.命令行进入pytest.ini所在目录
​	2.输入命令：pytest
执行结果：
​	1.pytest.ini所在目录生成report文件夹，文件夹下生成一个xml文件


```

![allure_xml](/Users/Yoson/Desktop/MobileTestNote/%E7%AC%94%E8%AE%B0/%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%B5%8B%E8%AF%95_image/allure_xml.png)

### xml转html工具安装

#### mac版本

```
	1.：brew install allure
	2.进入report上级目录执行命令：allure generate report/ -o report/html
	3.report目录下会生成index.html文件，即为可视化报告


#### windows版本

	1.下载压缩包allure-2.6.0.zip
		地址：https://bintray.com/qameta/generic/allure2
	2.解压
	3.将压缩包内的bin目录配置到path系统环境变量
	4.进入report上级目录执行命令：allure generate report/ -o report/html --clean
	5.report目录下会生成index.html文件，即为可视化报告


![allure_html](/Users/Yoson/Desktop/MobileTestNote/%E7%AC%94%E8%AE%B0/%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%B5%8B%E8%AF%95_image/allure_html.png)

## 33.Allure之Pytest

### 添加测试步骤

	方法：@allure.step(title="测试步骤001")


```

```
	示例：
		test_all.py
		import allure, pytest
		class Test_allure:
		    def setup(self):
		        pass
		    def teardown(self):
		        pass
		    @allure.step('我是测试步骤001')
		    def test_al(self, a):
		        assert a != 2


```

![allure步骤](/Users/Yoson/Desktop/MobileTestNote/%E7%AC%94%E8%AE%B0/%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%B5%8B%E8%AF%95_image/allure%E6%AD%A5%E9%AA%A4.png)

### 添加测试描述

```
	方法：allure.attach('描述', '我是测试步骤001的描述～～～')


```

```
	示例：
		test_all.py
		import allure, pytest
		class Test_allure:
		    def setup(self):
		        pass
		    def teardown(self):
		        pass
		    @allure.step('我是测试步骤001')
		    def test_al(self, a):
		    	allure.attach('描述', '我是测试步骤001的描述～～～')
		        assert a != 2


![allure步骤描述](/Users/Yoson/Desktop/MobileTestNote/%E7%AC%94%E8%AE%B0/%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%B5%8B%E8%AF%95_image/allure%E6%AD%A5%E9%AA%A4%E6%8F%8F%E8%BF%B0.png)

### 添加严重级别

测试用例设置不同的严重级别，可以帮助测试和开发人员更直观的关注重要Case.



```

```
	方法：@pytest.allure.severity(Severity)
	参数：
		Severity：严重级别(BLOCKER,CRITICAL,NORMAL,MINOR,TRIVIAL)
	使用方式：
		@pytest.allure.severity(pytest.allure.severity_level.CRITICAL）


```

```
	示例：
		test_all.py
		import allure, pytest
		class Test_allure:
		    def setup(self):
		        pass
		    def teardown(self):
		        pass
		    @pytest.allure.severity(pytest.allure.severity_level.CRITICAL）
		    @allure.step('我是测试步骤001')
		    def test_al(self, a):
		    	allure.attach('描述', '我是测试步骤001的描述～～～')
		        assert a != 2


![allure严重级别](/Users/Yoson/Desktop/MobileTestNote/%E7%AC%94%E8%AE%B0/%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%B5%8B%E8%AF%95_image/allure%E4%B8%A5%E9%87%8D%E7%BA%A7%E5%88%AB.png)

## 34.Jenkins安装

Jenkins是一个开源软件项目，是基于Java开发的一种持续集成工具，用于监控持续重复的工作，
旨在提供一个开放易用的软件平台，使软件的持续集成变成可能。

一般情况下，公司内部Jenkins安装在服务端，不需要本地安装，都已配置完成，可直接操作使用.


- 依赖java环境

	jdk1.5以上



### 安装jenkins

1.下载jenkins.war
2.进入jenkins.war所在目录，执行：java -jar jenkins.war
3.浏览器进入：localhost:8080


### 安装所需插件

1.官网下载jenkins安装包

2.安装完成后，会自动打开页面(若没有可以手动打开浏览器输入：localhost:8080)

3.进入默认密码提示文件，输入系统默认密码




![jenkins安装启动页](/Users/Yoson/Desktop/MobileTestNote/%E7%AC%94%E8%AE%B0/%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%B5%8B%E8%AF%95_image/jenkins%E5%AE%89%E8%A3%85%E5%90%AF%E5%8A%A8%E9%A1%B5.png)
![jenkins初始密码](/Users/Yoson/Desktop/MobileTestNote/%E7%AC%94%E8%AE%B0/%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%B5%8B%E8%AF%95_image/jenkins%E5%88%9D%E5%A7%8B%E5%AF%86%E7%A0%81.png)

4.安装建议插件




![jenkins建议安装插件](/Users/Yoson/Desktop/MobileTestNote/%E7%AC%94%E8%AE%B0/%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%B5%8B%E8%AF%95_image/jenkins%E5%BB%BA%E8%AE%AE%E5%AE%89%E8%A3%85%E6%8F%92%E4%BB%B6.png)
![jenkins插件安装中](/Users/Yoson/Desktop/MobileTestNote/%E7%AC%94%E8%AE%B0/%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%B5%8B%E8%AF%95_image/jenkins%E6%8F%92%E4%BB%B6%E5%AE%89%E8%A3%85%E4%B8%AD.png)

5.设置用户初始化信息




![jenkins设置用户信息](/Users/Yoson/Desktop/MobileTestNote/%E7%AC%94%E8%AE%B0/%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%B5%8B%E8%AF%95_image/jenkins%E8%AE%BE%E7%BD%AE%E7%94%A8%E6%88%B7%E4%BF%A1%E6%81%AF.png)

6.jenkins启动




![jenkins启动](/Users/Yoson/Desktop/MobileTestNote/%E7%AC%94%E8%AE%B0/%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%B5%8B%E8%AF%95_image/jenkins%E5%90%AF%E5%8A%A8.png)

7.jenkins首页




![jenkins首页](/Users/Yoson/Desktop/MobileTestNote/%E7%AC%94%E8%AE%B0/%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%B5%8B%E8%AF%95_image/jenkins%E9%A6%96%E9%A1%B5.png)

## 35.Jenkins持续集成配置

### Jenkins安装Allure插件

1.进入jenkins系统管理 -> 管理插件
2.点击可选插件
3.搜索框输入Allure Jenkins Plugin
4.选中安装


### Jenkins安装Allure Commandline工具

1.进入jenkins系统管理 -> 全局工具配置(系统设置xiang)
2.找到Allure Commandline，点击Allure Commandline安装
3.输入一个别名
4.点击新增安装-选择解压*.ip/*.tar.gz
5.解压目录选择已下载好的allure2.5.0.zip包所在目录(⚠️ 版本要一致)
6.点击保存


![allure_commind](/Users/Yoson/Desktop/MobileTestNote/%E7%AC%94%E8%AE%B0/%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%B5%8B%E8%AF%95_image/allure_commind.png)

### Jenkins新建一个项目

1.选择新建一个自由风格的软件项目 -> 点击确定
2.输入一些项目描述

3.选择GitHub project 
4.输入Project url # 因我们只是举例，所以使用自己的一个github测试脚本




![J_General](/Users/Yoson/Desktop/MobileTestNote/%E7%AC%94%E8%AE%B0/%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%B5%8B%E8%AF%95_image/J_General.png)

jenkins配置一些东西,git只要一传东西,jenkins会自动帮我们构建,帮我们生成报告.

### 源码管理配置

5.勾选Git
6.Repository URL输入地址同第四步
7.点击Add添加github的用户名和密码


![J_源码](/Users/Yoson/Desktop/MobileTestNote/%E7%AC%94%E8%AE%B0/%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%B5%8B%E8%AF%95_image/J_%E6%BA%90%E7%A0%81.png)
![github用户名密码](/Users/Yoson/Desktop/MobileTestNote/%E7%AC%94%E8%AE%B0/%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%B5%8B%E8%AF%95_image/github%E7%94%A8%E6%88%B7%E5%90%8D%E5%AF%86%E7%A0%81.png)

### 构建触发器

8.勾选Poll SCM # 根据定时任务，查看github版本是否更新，如果更新会自动构建项目
9.输入crontab命令
​	举例：
​		*/1 * * * * # 每一分钟检查一次
10.点击增加构建步骤，选择Execute shell
11.Command输入
​	mac：
​	export PATH=$PATH:"pytest可执行文件的目录"
​	pytest
​	
​	windows：
​	PATH=$PATH;"pytest可执行文件的目录"     #(到scripts)
​	pytest


![J_构建](/Users/Yoson/Desktop/MobileTestNote/%E7%AC%94%E8%AE%B0/%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%B5%8B%E8%AF%95_image/J_%E6%9E%84%E5%BB%BA.png)

时程表的格式如下:
f1 f2 f3 f4 f5 program
其中 f1 是表示分钟，f2 表示小时，f3 表示一个月份中的第几日，f4 表示月份，f5 表示一个星期中的第几天。program 表示要执行的程式。


### 构建后操作

12.点击增加构建后操作步骤，选择Allure Report
13.Path路径输入：生成的报告文件夹名称
⚠️ 文件夹名称与pytest生成的报告文件夹名称一致


```

![J_构建后](/Users/Yoson/Desktop/MobileTestNote/%E7%AC%94%E8%AE%B0/%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%B5%8B%E8%AF%95_image/J_%E6%9E%84%E5%BB%BA%E5%90%8E.png)

## 36.jenkins触发项目构建方式

### 手动触发构建

- 点击立即构建

### 更新github代码

- 触发器在定时任务到达时，会出发项目构建

![手动构建](/Users/Yoson/Desktop/MobileTestNote/%E7%AC%94%E8%AE%B0/%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%B5%8B%E8%AF%95_image/%E6%89%8B%E5%8A%A8%E6%9E%84%E5%BB%BA.png)

## 37.Jenkins邮件配置

### 发件人配置

```
	配置邮件系统用户：
		系统管理-系统设置-Jenkins Location
		系统管理员邮件地址：用户名@163.com(发送邮件用户)
	配置系统邮件：
		系统管理-系统设置-邮件通知
		SMTP服务器：例 smtp.163.com
		用户默认邮件后缀：例如 @163.com
		高级-使用SMTP认证
		输入发送邮箱和密码 -可以使用测试邮件验证
	配置(发送附件)邮件：
		系统管理-系统设置-Extended E-mail Notification
		SMTP server：例 smtp.163.com
		Default user E-mail suffix：例如 @163.com
		高级-Use SMTP Authentication - 输入发送邮件的邮箱和密码
		Default Content Type: HTML(text/html)
		Default Content(报告模版,使用以下html代码即可):
		       <hr/>(本邮件是程序自动下发的，请勿回复！)<hr/>
				项目名称：$PROJECT_NAME<br/><hr/>
				构建编号：$BUILD_NUMBER<br/><hr/>
				git版本号：${GIT_REVISION}<br/><hr/>
				构建状态：$BUILD_STATUS<br/><hr/>
				触发原因：${CAUSE}<br/><hr/>
				目录：${ITEM_ROOTDIR}<br/><hr/>
				构建日志地址：<a href=" ">${BUILD_URL}console</a ><br/><hr/>
				构建地址：<a href="$BUILD_URL">$BUILD_URL</a ><br/><hr/>
				报告地址：<a href="${BUILD_URL}allure">${BUILD_URL}allure</a ><br/><hr/>
				失败数：${FAILED_TESTS}<br/><hr/>
				成功数：${FAILED_TESTS}<br/><hr/>
				变更集：${JELLY_SCRIPT,template="html"}<br/><hr/>


### 收件人配置

# 添加测试报告接收邮件列表

14.点击增加构建后操作步骤，选择Editable Email Notification 
15.点击Advanced Setting…
16.点击Triggers中的高级按钮
17.Recipient List输入邮件接收列表，多个邮件逗号分隔




![邮件列表](/Users/Yoson/Desktop/MobileTestNote/%E7%AC%94%E8%AE%B0/%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%B5%8B%E8%AF%95_image/%E9%82%AE%E4%BB%B6%E5%88%97%E8%A1%A8.png)



## 38.XPath精确查找

//*[@text='Android']


用于查找某个属性是否等于某个值，而非包含。

## 39.XPath多条件查找

//*[@text='Android' and @index='0']


用于通过多个条件进行查找

总结:

包含      //*[contains(@text, '设')]

精确查找   //*[@text='设']

满足多个条件查询   //*[@text='设' and contains(@text, '设')]

### 40.获取toast

下载 appium-uiautomator2-driver

方法  cnpm install appium-uiautomator2-driver

在前置代码中添加   desired_caps['automationName'] = 'Uiautomator2'

使用WebDriverWait的方式寻找

```python
def find_toast(driver, message, timeout=3):
    #message为预期要获取的toast的部分信息
    message = "//*[contains(@text, '" + message +"')]"
    element = WebDriverWait(driver, timeout, 0.1).until(lambda x:x.find_element(By.XPATH, message))
    return element.text
```

将登登录成功失败,改为toast

1,在base中,写一个find_toast的函数,返回,根据部分内容,找到全部内容

2,在base中,写一个is_toast_exist的函数,如果找到,则返回true,如果找不到,则报错并返回false

3,在前置代码中添加 desired_caps['automationName'] = 'Uiautomator2'

```python
base_action.py(此文件中添加如下代码)
    def find_toast(self, message, time=10, poll=0.5):
        message = "//*[contains(@text, ' " + message + " ')]"
        ele = (WebDriverWait(self.driver, 10, 0.5)
               .until(lambda x: x.find_element(By.XPATH, message)))
        return ele.text

    def is_login_with_toast(self, text):
        try:
            self.find_toast(By.XPATH, "text," + text)
            return True
        except Exception:
            return False

```



## 文件管理器

- 第一个
  - 打开文件管理器
  - 在sdcard新建一个zzz文件夹
  - 在sdcard新建一个aaa文件夹
  - 进入zzz文件夹
  - 在zzz中创建文件 1.txt-20.txt
  - 把zzz中的20个文件移动aaa中
  - 判断-aaa有20个文件目录

```
目录
- 项目名字
- pytest.ini
- scripts
- - test_file
- page
- - file_page
- base
- - xxxx


```

```
test_file.py - 自动化脚本
脚本中有11个函数

1. 第一个
2. 如果属性弹窗中名字内容和所在位置一致 那么通过
3-10. 出了属性之外的左下角菜单所有功能
11. test_fail
	assert 0
	
尽量写上allure的log
邮件模板，最上面加上自己的名字

邮箱：hitheima@163.com


```

## 小作业

### 元素定位和操作练习

- 点击搜索按钮
- 输入“无线”
- 获取当前有几条记录?

### 滑动和拖拽时间练习

- 想办法滑动到最后的“关于手机”
- 点击进去
- 看当前页面是不是有一个“5.1”的字符串

## 常用代码

### 前置代码

```
	from appium import webdriver
	# server 启动参数
	desired_caps = {}
	# 设备信息
	desired_caps['platformName'] = 'Android'
	desired_caps['platformVersion'] = '5.1'
	desired_caps['deviceName'] = '192.168.56.101:5555'
	# app的信息
	desired_caps['appPackage'] = 'com.android.settings'
	desired_caps['appActivity'] = '.Settings'
	# 解决输入中文
	desired_caps['unicodeKeyboard'] = True
	desired_caps['resetKeyboard'] = True

	# 声明我们的driver对象
	driver = webdriver.Remote('http://127.0.0.1:4723/wd/hub', desired_caps)


```

### 获取包名

```
1.Mac/Linux: 'adb shell dumpsys window windows | grep mFocusedApp’
2.在 Windows 终端运行 'adb shell dumpsys window windows’ 然后去看mFocusedApp这一行的内容。


```

### xPath

```
//*[contains(@,'')]


```

## capabilities启动参数列表

![通用](/Users/Yoson/Desktop/MobileTestNote/%E7%AC%94%E8%AE%B0/%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%B5%8B%E8%AF%95_image/cap01.png)
![android](/Users/Yoson/Desktop/MobileTestNote/%E7%AC%94%E8%AE%B0/%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%B5%8B%E8%AF%95_image/cap02.png)
![ios](/Users/Yoson/Desktop/MobileTestNote/%E7%AC%94%E8%AE%B0/%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%B5%8B%E8%AF%95_image/cap03.png)

## keyevent常用键列表

- 常用键展示

```
	KEYCODE_CALL 拨号键 5
	KEYCODE_ENDCALL 挂机键 6
	KEYCODE_HOME 按键Home 3
	KEYCODE_MENU 菜单键 82
	KEYCODE_BACK 返回键 4
	KEYCODE_SEARCH 搜索键 84
	KEYCODE_CAMERA 拍照键 27
	KEYCODE_FOCUS 拍照对焦键 80
	KEYCODE_POWER 电源键 26
	KEYCODE_NOTIFICATION 通知键 83
	KEYCODE_MUTE 话筒静音键 91
	KEYCODE_VOLUME_MUTE 扬声器静音键 164
	KEYCODE_VOLUME_UP 音量增加键 24
	KEYCODE_VOLUME_DOWN 音量减小键 25
	KEYCODE_ENTER 回车键 66
	KEYCODE_ESCAPE ESC键 111
	KEYCODE_DPAD_CENTER 导航键 确定键 23
	KEYCODE_DPAD_UP 导航键 向上 19
	KEYCODE_DPAD_DOWN 导航键 向下 20
	KEYCODE_DPAD_LEFT 导航键 向左 21
	KEYCODE_DPAD_RIGHT 导航键 向右 22
	KEYCODE_MOVE_HOME 光标移动到开始键 122
	KEYCODE_MOVE_END 光标移动到末尾键 123
	KEYCODE_PAGE_UP 向上翻页键 92
	KEYCODE_PAGE_DOWN 向下翻页键 93
	KEYCODE_DEL 退格键 67
	KEYCODE_FORWARD_DEL 删除键 112
	KEYCODE_INSERT 插入键 124
	KEYCODE_TAB Tab键 61
	KEYCODE_NUM_LOCK 小键盘锁 143
	KEYCODE_CAPS_LOCK 大写锁定键 115
	KEYCODE_BREAK Break/Pause键 121
	KEYCODE_SCROLL_LOCK 滚动锁定键 116
	KEYCODE_ZOOM_IN 放大键 168
	KEYCODE_ZOOM_OUT 缩小键 169
	KEYCODE_ALT_LEFT Alt+Left
	KEYCODE_ALT_RIGHT Alt+Right
	KEYCODE_CTRL_LEFT Control+Left
	KEYCODE_CTRL_RIGHT Control+Right
	KEYCODE_SHIFT_LEFT Shift+Left
	KEYCODE_SHIFT_RIGHT Shift+Right


```

- 官方keyevent文档

```
	地址: https://developer.android.com/reference/android/view/KeyEvent.html

```

### git 笔记

git:版本控制的工具

学习git的网站:   git.oschina.net/progit

##### 配置

$ git config --global user.name "rosexiang150"

$ git config --global user.email 22480111**@**.com

git config --list 此命令查看配置信息

##### 命令

1,初始化一个git项目(告诉git这个项目,让它管理)   git init

2,查看当前的文件的git的状态,    git status

​	如果提示 "not a git repository"意味着不是一个git项目,需要先使用git init进行初始化.

3,告诉git,管理(追踪)文件:

​	a,   git add 文件名.格式  (添加了一个文件,进行追踪)

​	b,    git add .    (添加所有的git文件)

4, git status

5,提交版本

git commit -m "注释,本次操作都干了什么"

##### sourcetree

在官网就可下载,但不知道用途,所以没安装.

### github

github 与码云(git)唯一区别:github创建私有仓库需要付费, git不需要.

commit是本地的一个提交, 提交都是提交到本地

push是一个上传,推送,是跟远程进行一个同步,比如把本地的项目推送到服务器上,

本地多次提交之后可以放到远端.

git常用命令:

git init 初始化项目

git add . 或者git add 文件名.格式       把文件交给git管理

git status   当前git的状态

git commit -m "注释"  表示提交

git remote add origin https://github.com/itheima/popo.git    建立远端连接

git push -u origin master 推送到远端

##### 如何下载github的项目

1,download zip 下载

​	进入项目主页,右侧有一个绿色的按钮,点击后,选择download即可

2,clone 克隆

​	a,从远端第一次放到本地的过程叫clone, clone with https

​	b,在github主页上,项目会有一个地址,通过sourcetree进行克隆

​	c, 在sourcetree点击新仓库,从url克隆

​	d,将"xxxxxxxx.git"的地址,赋值到sourcetree中的url

​	e,选择存放路径即可

##### github的fork

目标项目----点击fork----自己主页多一个项目-------选择clone or download----复制地址----在sourcetree粘贴----克隆到桌面上或其他地址,不要用download zip

别人的项目,点击fork,相当于复制,但是fork之后的源地址是不一样的.意思是原作者更新项目,我们fork的项目没有变化.我们也可以提交东西,但原作者是不会显示.

##### sourcetree中的pull

作用:已经本地和远端连接的情况下(已经clone过了),将远端的代码,同步到本地(让本地保持和远端一样).这个过程叫pull

操作: 在sourcetree中,使用拉取,点击确定.

##### sourcetree中的切换版本

切换版本,就是可以快速预览之前的版本的情况.

在sourcetree中,直接双击.

##### 多次commit之后push

如果本地项目进行修改之后,sourcetree会提示,修改文件的个数.

如果想使用sourcetree进行提交,需要先勾选"暂存的文件",需要提交什么,就勾选什么,允许部分提交.

提交之后,此时远端并不会发生什么变化,需要进行一次push(推送),让远端同步本地的代码,意思是让远端和本地保持一致.

sourcetree是git 命令的可视化图形界面.xiang

关于提交的时间.提交的时间,以每次commit为准,与push无关.

##### 公司项目已传git,新人的步骤:

找项目主管要账号,是用svn还是git,  要git 远端的地址 "xxxxxx.git"

在sourcetree中,仓库粘贴地址,---克隆,

远端有改变,我们也需要pull.保持我们也是最新的.

##### 冲突

同事更新了版本,你直接更新是不行的.需要在sourcetree中先把新版本pull下来,然后再修改,提交.我们每一次在提交之前,先pull一下.

冲突是什么时候产生的:

当我们想要commit, push的时候,我们先要保证我们的版本是和服务器一致,我们才能修改.

当我们pull的时候,是和服务器一致的,然后我们修改,这个时候同事改了同样的代码,并且提交了.这时我想提交的时候,会报错.

这时git会给提示.一堆红色的<<<<=====>>>>,其中HEAD的那部分是自己的,

自己做出选择,然后提交.

### TPshop项目自动化测试

1,手点基本流程, 大体操作这个要测试的功能

2,写测试用例(尽可能考虑各种可能性)

3,对着测试用例,进行功能测试

4,考虑自动化

##### 项目准备:

准备之前用的base和配置文件

##### 先写一个正确的测试脚本

1,创建2个文件在对应的文件夹,一个是login_page,一个是test_login

2,在test_login的setup中,连接手机(导入模块,使用init_driver函数)

3,在login_page下,写类,继承BaseAction

4,在test_login下,创建page对象

5,分析步骤,发现部分步骤是必须要有的,考虑写在page的init中

6,

##### app开发一些常识

关于toast,toast只在android中有,不是所有的2分钟消失的那个视图都叫toast

关于控件:

android:  按钮:Button    文本框,显示文字:TextView     输入框,用来输入:EditText

ios:  按钮:UIButton       文本框,显示文字:UILabel    输入框,用来输入:UITextFiled

在ios中UITextView是用来输入大段文本的.

在ios类名中有前缀,涉及到视图都是UI开头.



APP测试的流程

- 测试资源准备
  - 需求文档
  - 接口文档
  - 原型图/效果图
  - 主流机型的真机
    - android 主要的品牌
    - iOS不同版本
- 测试用例设计和评审
  - 尽可能考虑多种情况
  - 开会讨论
- UI
  - 和效果图是否一致，如果不一致最好以效果图为准。协助两边沟通。
- 功能
  - 从逻辑的角度上（需求文档）去对比
- 中断测试
  - 电话，短信，闹钟
  - 前后台
- 兼容性
  - 厂商
    - iOS
    - android
      - 华为，小米，三星xxx
  - 分辨率
    - <https://blog.csdn.net/a704755096/article/details/46342689>
  - 系统版本
    - 问开发，最低版本到多少，从最低到现在的版本即可。
    - iOS，一般适配最新的到前两个版本，比如现在是11，就是9 10 11。
    - 主版本号.次版本号.修订版本号
- 性能测试
  - 同类产品相似
    - 启动时间，电池消耗，流量。
  - 如果有硬性标准除外
- 压力测试
  - monkey
    - 搜索null（空）
    - 重视空指针异常
- 安全测试
  - 传输数据的时候是否是明文（是不是用到加密AES/DSC）
  - 密码的是不是MD5
- 测试报告
- 自动化
  - 条件
    - 万年不变的东西
    - 主线业务
  - 好处
    - 节约时间和人力成本
  - 适用情况
    - 公司产品迭代特别快的

### webview

##### 查看webview元素的方式

在浏览器中输入 chromr://inspect 地址(需要翻墙)

可以看到对应的手机设备,已经有的webview:方式1: 点击inspect查看元素信息

方式2:

通过自己电脑上的浏览器chrome打开对应的手机的webview页面(如m.baidu.com)

在页面点击右键,选择检查(不是查看源代码)

点击红色按钮,进入查看元素的模式

##### 实现webview自动化

前置代码,和之前相同(打开的包名和启动名是浏览器软件)

获取,driver的所有的上下文

​	得到一个原生的APP的字符串,还有其他各种webview的字符串

​	

```
contexts = driver.contexts
	for i in contexts:
		print(i)


```

### monkey

##### Monkey用来做什么:

Monkey主要用于android的压力测试,是一个自动的压力测试小工具.主要目的是为了测试APP是否会crash.

##### Monkey程序介绍:

monkey程序由android系统自带,使用java语言写成,在android文件系统中的存放路径: /system/framework/monkey.jar;

monkey.jar程序是由一个名为"monkey"的shell脚本来启动执行,shell脚本在android文件系统中的存放路径:   /system/bin/monkey;

monkey命令启动方式:\

​	可以通过PC机的cmd窗口执行: adb shell monkey {+命令参数}  进行monkey测试

​	在PC上adb shell进入 android系统,执行monkey  {+命令参数} 进行monkey测试

​	在android机或者模拟器上直接执行monkey命令,可以在android机上安装android终端模拟器(Terminal Emulator for Android).

##### monkey输出日志

adb shell monkey -p 程序的包名 动作次数 > 路径/log.txt

比如 adb shell monkey -p com.android.settings 100 > Desktop/log1.txt

##### monkey基本参数介绍

**参数 -p**介绍: -p 后面跟允许的包名列表.可以指定一个或多个包,指定包之后,monkey将只允许系统启动指定的app,

指定一个包  adb shell monkey -p com.android.settings 100

指定多个包   adb shell monkey -p com.android.settings -p cn.goapk.market 100

monkey 其他参数

**参数 -v介绍**  用于指定反馈信息的级别,信息级别就是日志的详细程度,总共分3级:

a)   adb shell monkey -p cn.goapk.market -v 100   仅提供启动提示,测试完成,最终结果等少量信息

b)  adb shell monkey -p cn.goapk.market -v -v 100   提供较为详细的日志,包括每个发送到activity的事件信息

c)    adb shell monkey -p cn.goapk.market -v -v -v 100  最详细的日志,包括了测试中选中/未选中的activity的事件信息

**参数 -s介绍**   随机数种子, 用于指定伪随机数生成器的seed值,如果seed相同,则两次monkey测试所产生的事件序列也相同.如:

monkey测试1:    adb shell monkey -p cn.goapk.market -s 10 100

monkey测试2:    adb shell monkey -p cn.goapk.market -s 10 100

上述2个测试结果是一样的.

随机:就算所有的条件都相同,得到的结果也不相同.

伪随机:所有的条件都一致,得到的结果也相同.种子是其中的条件.当所有的种子都一致,得到的结果也一致.



**参数 --throttle** 毫秒,用于指定用户操作(即事件)间的时延,单位是毫秒,如果指定这个参数,monkey会尽可能的生成和发送消息.如  adb shell monkey -p cn.goapk.market --throttle 3000 100

##### monkey日志分析

--pct-touch <percent>  调整触摸事件的百分比(触摸事件是一个down-up事件,它发生在屏幕上的某单一位置)

--pct-motion <percent>  调整动作事件的百分比(动作事件由屏幕上某处的一个down事件,一系列的伪随机事件和一个up事件组成)

--pct-trackball <percent>   调整轨迹事件的百分比(轨迹事件由一个或几个随机的移动组成,有时还伴随有点击)

--pct-nav <percent>  调整"基本"导航事件的百分比(导航事件由来自方向输入 设备的up/down/left/right组成)

--pct-majornav <percent>   调整"主要"导航事件的百分比(这些导航事件通常引发图形界面中的动作,如 回退按钮,菜单按键)

--pct-syskeys <percent> 调整"系统"按键事件的百分比(这些按键通常被保留,由系统使用,如home, back, start call , end call及音量控制键)

--pct-appswitch <percent>  调整启动activity的百分比,在随机间隔里,monkey将执行一个startActivity()调用,作为最大程度覆盖包中全部activity的一种方法.

--pct-anyevent <percent>  调整其他类型事件的百分比,它包罗了所有其他类型的事件,如 按键,其他不常用的设备按钮等

上述的事件也可以人为设置百分比,比如monkey只点点点,不要滑动等其他操作,  adb shell monkey -p com.android.settings -v -v --throttle 20 --pct-touch 100 100 > Desktop/log2.txt

正常情况:

如果monkey测试顺利执行完成,在log的最后,会打印出当前执行事件的次数和所花费的时间

异常情况:

monkey测试出现错误后,一般的分析步骤:

看monkey的日志(注意第一个switch以及异常信息等)

程序无响应的问题:在日志中搜索"ANR"

崩溃问题:   在日志中搜索"Exception"如果出现空指针,NullPointException,肯定有bug

monkey执行中断,在log最后也能看到当前执行次数.

##### 版本号

主版本号

##### appium的额外功能

appium查看元素---android   

windows系统:在appium的file菜单--->new session window

mac:  appium--->new session window

在弹出的新界面,desired capabilities中填写对应的前置代码的key,value,然后保存,再打开

此页面一个作用是代替了ui automator ,因为它有attribute及value,一个作用是左上部分有3个按钮,分别是选中,滑动,点击,用此按钮操作最左边的界面和手机模拟器的作用是一样的,一个作用是右上部有5个按钮,

在此页面上,左上部分有3个按钮,一个是select elements   一个是swipe by coordinates  一个是tap by coordinates































































