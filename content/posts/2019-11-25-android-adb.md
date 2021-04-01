---
title: "Android ADB 应用精简"
date: 2018-11-25T15:41:16+08:00
draft: false
tags: ["Android", "App"]
---

- [小米 MIUI 免 root 一键删除系统内置软件](https://t.me/zuanke8/6333)

    **温馨提示：因版本差异！所以请大家尽量卸载前备份重要数据！**

    本工具是基于 Android 9 所搭载的 MIUI 10 和 MIUI 11 修改！可向下兼容 MIUI 系统，Andriod 10 未测试！如果想恢复卸载掉的软件，双清系统（恢复出厂设置）即可

    1. 准备 小米手机、Windows 电脑、数据线
    2. 安装[小米官方手机驱动](http://bigota.d.miui.com/tools/MiFlash2018-5-28-0.zip)
    3. 进入开发者模式
    4. 连接手机与电脑用数据线将手机与电脑连接，选择 传文件 模式
    5. 使用本帖的工具进行卸载
    6. 工具 [下载地址](https://www.lanzous.com/iavr5tc)

- [华为 EMUI 免 root 一键删除系统内置软件](https://t.me/zuanke8/6337)

    温馨提示：为避免卡华为 LOGO！建议卸载前备份重要数据！

    此工具在 EMUI 9.1.0 测试无异常，可向下兼容 EMUI 系统，Andriod 10 未测试！

    如果想恢复卸载掉的软件，双清系统（恢复出厂设置）即可！

    1. 准备 华为手机、Windows电脑、数据线
    2. [安装华为官方手机驱动](https://consumer.huawei.com/cn/support/hisuite/)
    3. 进入开发者模式
    4. 连接手机与电脑
    5. 使用本帖的工具进行卸载
    6. 工具 [下载地址](https://www.lanzous.com/iawrxif)

## 精简步骤

1. 在手机上打开USB调试

    打开「设置-我的设备-全部参数」，连续点击 5 次 「MIUI 版本”」，打开「开发者选项」，然后返回并打开 「设置→更多设置→开发者选项」，打开「USB 调试」，打开「USB调试(安全设置)」。

2. 解压 adb.zip

     在ADB/ADB or Fastboot文件夹，打开 cmd.exe，输入 `adb devices` 查看手机是否连接电脑.查看手机是否要授权，点确认。电脑cmd窗口出现一段 「字母数字组合 device」。说明设备连接成功。

3. 说明

    ```
    adb shell pm uninstall --user 0 应用包名 
    删除 显示 Success，表示成功
    ```

    > 删除的app，据说只能通过恢复出厂设置来恢复，请谨慎删除。

    ```
    adb shell pm disable-user 应用包名  
    停用  显示 disabled-user，表示成功
    ```

    > 停用的app可以手机应用管理里启用。MIUI 中一些 app 无法停用，或者显示停用了，但还是运行中。

    ```
    adb shell pm enable 应用包名        启用
    ```

- MIUI10，设置，应用管理，应用，右上角「i」可以看到应用包名。
- 批量启用，可以修改bat文件，编辑→替换，把停用的命令替换成启用，达到一键启用的效果
- 批量停用。 在电脑新建一个文本文档。把自己要精简的命令放进去，然后改.txt为.bat，丢adb文件夹。双击bat文件，自动出现命令窗口，命令走完自动关闭。

## 精简项目

> 下面是我的小米手机用的是adb 精简列表。删除是我真的用不上的，停用是可能以后会用到。

- 省电确实是玄学。有时候精简完其实省电了。有时候好像又没什么区别。不知道是不是和系统版本有关，还是心理作用。
- 按我这个精简，可以开机，不会卡mi，相应和关联的功能可能不可用。精简完，可以系统更新里面增量包更新。更新完，删除的还是删除的，停用了的还是停用了。
- 实在用不到的选择删除，可能用得到的建议停用。但部分app无法停用，或者重启会启用。

 下面精简列表收集于网络结果。我只是收集整合，提取我认为可以用的。然后给大家参考而已。详细的还请自己测试。出任何问题，本人一概不负责。建议能停用的尽量停用。不能停用的才考虑删除。删除的同时需要考虑有没有影响到别的app。 

已知bug，精简小米云相关服务前，未开启手机查找时：精简完，不能开启手机查找，MI Pay 无法绑定银行卡；已测试，开启开启手机查找后，可精简小米云相关服务，对MI Pay 开卡无影响。

### 删除

> 一部分应用不能被停用。一部分应用停用后，重启就启用了，只能删除。有标注的是测试过的

```
adb shell pm uninstall --user 0 com.miui.virtualsim 全球上网（不能被停用）
adb shell pm uninstall --user 0 com.android.email 电子邮件
adb shell pm uninstall --user 0 com.miui.notes 便签
adb shell pm uninstall --user 0 com.miui.hybrid 快应用
adb shell pm uninstall --user 0 com.miui.hybrid.accessory 快应用服务
adb shell pm uninstall --user 0 com.miui.voiceassist 小爱同学
adb shell pm uninstall --user 0 com.miui.player 音乐
adb shell pm uninstall --user 0 com.miui.video 视频
adb shell pm uninstall --user 0 com.xiaomi.gamecenter 游戏
adb shell pm uninstall --user 0 com.xiaomi.gamecenter.sdk.service 游戏服务
```

### 停用

#### 已经测试过

```
adb shell pm disable-user com.android.quicksearchbox            搜索（建议在系统应用设置里面-搜索-关闭手势打开，再精简。可以停用。建议停用）
adb shell pm disable-user com.miui.userguide                    用户手册
adb shell pm disable-user com.miui.cloudservice                 小米服务（精简前，未开启手机查找的，精简后，不能开启手机查找，则MI pay无法绑定银行卡）
adb shell pm disable-user com.android.midrive                   小米云盘
adb shell pm disable-user com.miui.yellowpage                   生活黄页（建议停用。需要通话短信拦截的不建议精简。）
adb shell pm disable-user com.miui.screenrecorder               屏幕录制
adb shell pm disable-user com.android.browser                   浏览器
adb shell pm disable-user com.miui.contentextension             传送门
adb shell pm disable-user com.android.providers.userdictionary  用户字典
adb shell pm disable-user com.xiaomi.payment                    米币支付
adb shell pm disable-user com.xiaomi.drivemode                  驾车模式
adb shell pm disable-user com.android.stk                    USIM卡应用 (建议停用。停用了显示正在运行，重启就好)
adb shell pm disable-user com.miui.backup                       备份
adb shell pm disable-user com.miui.cloudbackup                  桌面备份
adb shell pm disable-user com.miui.bugreport                    用户反馈
adb shell pm disable-user com.miui.touchassistant               悬浮球
adb shell pm disable-user com.android.printspooler          打印处理服务
adb shell pm disable-user com.android.bips                  默认打印服务
adb shell pm disable-user com.xiaomi.simactivate.service    小米SIM卡激活服务
adb shell pm disable-user com.sohu.inputmethod.sogou.xiaomi  搜狗输入法
adb shell pm disable-user com.miui.personalassistant          智能助理（负1屏的智能助理，据说删了会进不了桌面的。停用未发现）
adb shell pm disable-user com.android.calllogbackup    小米云备份通话记录
adb shell pm disable-user com.miui.systemAdSolution          msa广告推送（据说小米广告服务三件套之一）
adb shell pm disable-user com.xiaomi.ab               mab小米广告推送服务（据说小米广告服务三件套之一）
adb shell pm disable-user com.miui.analytics           Analytics数据分析（据说小米广告服务三件套之一）
adb shell pm disable-user com.xiaomi.scanner                    扫一扫（删除的话，设置，小米账号里面的扫一扫也挂了。建议停用）
adb shell pm disable-user com.dsi.ant.server           ANT HAL Service 
adb shell pm disable-user com.svox.pico            Pico TTS 语音识别系统
adb shell pm disable-user com.android.thememanager             个性主题（不建议删除，否则壁纸和铃声都不能换。建议设置好壁纸和铃声，闹钟铃声再停用）
adb shell pm disable-user com.miui.compass                       指南针
adb shell pm disable-user com.miui.micloudsync             MiCloudSync
adb shell pm disable-user com.miui.securityinputmethod      小米安全键盘
adb shell pm disable-user com.qualcomm.wfd.service              Wfd服务
adb shell pm disable-user com.android.emergency                 急救信息
adb shell pm disable-user com.xiaomi.providers.appindex         设置搜索
adb shell pm disable-user com.milink.service                    联播服务
adb shell pm disable-user com.miui.cleanmaster                  垃圾清理
adb shell pm disable-user com.android.dreams.basic          基本互动屏保
adb shell pm disable-user com.android.dreams.phototable  照片屏幕保护程序
adb shell pm disable-user com.android.egg             安卓彩蛋【百度结果】
adb shell pm disable-user com.mi.dlabs.vr                        小米VR
adb shell pm disable-user com.android.wallpaper.livepicker      动态壁纸
adb shell pm disable-user com.android.vpndialogs                VPN相关
adb shell pm disable-user com.android.bookmarkprovider           收藏夹
adb shell pm disable-user com.xiaomi.joyose                     卓越智擎（负一屏计步用的【百度结果】，精简后设置-更多设置-系统安全-伪基站防护也挂了)
adb shell pm disable-user com.miui.vpnsdkmanager              游戏加速器
adb shell pm disable-user com.android.smspush                   短信推送（删除对短信接收无影响）
adb shell pm disable-user com.android.calendar                     日历
adb shell pm disable-user com.android.providers.calendar        日历储存
adb shell pm disable-user com.android.providers.downloads.ui    下载管理
adb shell pm disable-user com.miui.weather2                        天气
adb shell pm disable-user com.miui.providers.weather            天气储存
adb shell pm disable-user com.miui.daemon                   MiuiDaemon
adb shell pm disable-user com.xiaomi.mircs                  免费网络短信
adb shell pm disable-user com.miui.catcherpatch  内容抓取（传送门相关功能）
adb shell pm disable-user com.qti.confuridialer          会议电话拨号界面
adb shell pm disable-user com.android.htmlviewer            HTML 查看器
adb shell pm disable-user com.miui.miwallpaper                  小米壁纸
adb shell pm disable-user com.android.pacprocessor       代理自动配置相关
adb shell pm disable-user com.android.printservice.recommendation    Print Recommendation Service（语音打印服务,用不到的可删除）
adb shell pm disable-user com.google.android.marvin.talkback    屏幕阅读
adb shell pm disable-user com.miui.translationservice           翻译服务
adb shell pm disable-user com.miui.translation.kingsoft     金山词霸翻译
adb shell pm disable-user com.miui.translation.xmcloud           金蝶？
adb shell pm disable-user com.miui.translation.youdao           有道翻译
adb shell pm disable-user com.xiaomi.upnp                  UpnpService （有小米盒子等电器的不要删除）
adb shell pm disable-user com.miui.vsimcore             虚拟SIM卡核心组件
adb shell pm disable-user com.android.wallpaperbackup           壁纸备份
adb shell pm disable-user com.miui.cloudservice.sysbase    云备份同步相关
adb shell pm disable-user com.mi.webkit.core              MiWebView （小米全球上网组件）
adb shell pm disable-user com.android.proxyhandler       代理自动配置相关
adb shell pm disable-user com.android.sharedstoragebackup   共享存储备份
adb shell pm disable-user com.android.wallpapercropper        壁纸合作商
adb shell pm disable-user com.miui.audioeffect                                     AudioEffect
adb shell pm disable-user com.xiaomi.mircs      小米广告服务相关??无法停用
adb shell pm disable-user com.miui.daemon                MiuiDaemon （据说是负一屏，删除后负一屏不可用，暂未发现其他Bug）无法停用
```

#### 没有精简过

> 无法确定精简后是否卡米，未精简的部分app列表。慎重精简！

```
com.sohu.inputmethod.sogou.xiaomi     搜狗输入法小米版
com.android.managedprovisioning       工作资料设置
com.miui.calculator                   计算器
com.android.soundrecorder             录音机
com.android.calendar                  日历
com.android.providers.calendar        日历储存
com.android.inputdevices              输入设备
com.miui.weather2                     天气
com.android.externalstorage           外部储存设备
com.android.documentsui               文件
com.android.fileexplorer              文件管理 
com.xiaomi.pass                       小米卡包
com.mipay.wallet                      小米钱包
com.miui.nextpay                      小米支付
com.miui.tsmclient                    小米智能卡
com.miui.contentcatcher               应用程序扩展服务                 （据说和传送门功能有关。无法停用，停用了显示正在运行，重启也在运行）
com.qapp.secprotect                   安全防护
com.miui.antispam                     骚扰拦截                      （不建议删，删后安全中心的骚扰拦截功能无法使用【百度结果，未测试】）
com.miui.cit                          硬件检测                             （删除后工程模式不可用【百度结果，未测试】）
```

### 已知不可精简的app

> 网络结果，未测试

- com.miui.securitycenter

安全中心（精简后卡米） 

- com.xiaomi.finddevice

查找手机（精简后卡米） 

- com.android.updater

系统更新（精简后卡米）

- com.xiaomi.market

应用商店（精简后卡米）

- com.xiaomi.vipaccount

我的小米（登录了小米账号的，精简后卡开机输入小米账号的密码）

- com.miui.guardprovider

MIUI安全组件（安全中心病毒扫描功能(重启会启用)， 精简后程序不能安装，提示错误-22。启用后，就能安装了 ）

- com.android.certinstaller

证书安装程序（卸载了以后android手机会无法安装应用程序,无法自动 WIFI 等） 

- com.android.providers.downloads

下载管理程序（不能删除，不然会出现无法安装应用程序【关闭 miu i优化后，关闭前未知】）

### 一些技巧

```jsx
adb devices     //检查一下设备是否连接正常
pause //正常就按任意键继续
adb install %1 //安装拖进来的apk
pause //安装成功后按任意键退出
 
默认：adb shell wm size 1080x1920
默认：adb shell wm density 480 && adb reboot 480？
修改手机分辨率 ：adb shell wm size 900x1600
修改手机DPI：adb shell wm density 380 && adb reboot
修改手机分辨率 ：adb shell wm size 720x1280
修改手机DPI：adb shell wm density 300 && adb reboot
```
