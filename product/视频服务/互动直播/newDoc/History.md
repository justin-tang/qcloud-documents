## `常见问题更新    2017-01-18`

* [适应更多旋转裁剪场景](https://www.qcloud.com/document/product/268/7647)
* [直播时支持背景音乐](https://www.qcloud.com/document/product/268/8297)

## `随心播后台 2.0.0    2017-01-18`

* 独立账户模式的随心播后台终于来了，需要iLive SDK1.2.0配合使用。
* [QuickStart文档](https://www.qcloud.com/document/product/268/7603)
* 账号集成采用独立模式
* 支持录制文件的查询
* 支持旁路推流和录制回调
* 完善了和随心播的交互协议，可以作为业务流程设计的参考

## `iLive SDK PC 1.0.0    2017-01-18`

* 集成AVSDK 1.8.4版本和IMSDK 2.5.0，优化进房速度和屏幕分享速度
* 支持和Android ios的房间直播、消息互通
* 支持屏幕分享和摄像头切换
* 切换账号集成方式为独立模式，需要iLive SDK1.2.0配合使用。

## `iLive SDK Android ios 1.2.0    2017-01-18`

* 集成AVSDK 1.8.4版本和IMSDK 2.5.0，优化进房速度和屏幕分享速度
* 支持PC iLiveSDK的屏幕分享内容的直播
* 优化了横屏旋转的处理模式
* 支持拉取旁路直播列表
* 支持拉取录制列表和本地播放
* 支持封面上传到COS、点赞动画、消息动画
* 切换账号集成方式为独立模式，需要iLive SDK1.2.0配合使用。

## `截图鉴黄功能发布 2017-01-05`

大家都知道，直播行业里截图鉴黄是绕不过的功能。

腾讯视频云为客户提供了强大的截图和鉴黄功能。具体使用方法请参考[文档](https://www.qcloud.com/document/product/268/8109)。

## `AV_iOS_SDK1.8.4    2016-12-28`
* 直播场景进房速度优化
* 新增高音质连麦功能(android)
* 原http通道改为https(iOS)
* 优化流控策略，加快屏幕分享出帧速度，提升用户体验
* 增加控制播放指定用户音频流的接口
* 新增外部音频数据采集的能力(android/ iOS)
* 外部视频输入流采集接口新增是否使能本地渲染的选项(android/ iOS)
* 获取质量参数接口新增客户端IP

## `iLive SDK 1.0.0 2016-11-25`
* 封装了avsdk和imsdk在直播场景的主要操作，大幅度降低了接入难度
* 抽取了直播业务逻辑作为framework，便于用户引用和扩展

## `AV_iOS_SDK1.8.2    2016-08-12`
* 视频添加水印功能
* sdk节点上报
* 音视频包收发模块重构
* 音频场景可以在房间内切换
* 增加房间超时回调
* 房间摄像头采集设置变化通知
* 自动申请视频位，防止视频位丢失导致的无视频
* 摄像头采集参数设置通知
* 部分接口调整

## `AV_Android_SDK1.8.2    2016-08-12`
* 视频添加水印功能
* sdk节点上报
* 音视频包收发模块重构
* 音频场景可以在房间内切换
* 增加房间超时回调
* 房间摄像头采集设置变化通知
* 自动申请视频位，防止视频位丢失导致的无视频
* 摄像头采集参数设置通知
* 部分接口调整

## `AV_iOS_SDK1.8.1.1    2016-06-21`
* 修复部分crash问题
* 修复切后台再切回直播间的黑屏问题

## `AV_Android_SDK1.8.1.1    2016-06-21`
* create context 加主线程保护
* 修改流控参数和编码器状态不同步导致黑屏的问题 
* 修改change role导致的crash
* 修改因create与destroy不对应导致切换帐号进不了房间问题
* 修复收包时有可能的内存泄露
* 修复切后台再切回直播间的黑屏问题

## `AV_WIN_SDK1.8.1.1    2016-06-21`
* 修改收包逻辑可能引发大量内存泄漏的问题
* 解决进入房间后同时满足以下条件而可能发生crash的问题
* 解决Demo在进行"进入房间-开启屏幕分享-退出房间-再次进入房间-请求其他人的屏幕分享"操作后可能没有渲染屏幕分享画面的问题

## `AV_iOS_SDK1.8.1    2016-06-06`
**1. SDK新增功能 **

* 视频硬件编码
* 视频采集支持16:9宽高比
* 增加是否有能力支持美颜接口
* 进房间速度优化
* 视频质量优化，分辨率/帧率与web配置联动，视频（软）编码输出提升至720P
* 音频质量优化，开放64码率
* 增加主播场景下开播模式高品质通话接口
* 优化监听接口，降低延时
* 增加进房间不作请求，直接接收已有画面接口
* 增加不重入房间切换角色的接口
* 增加实时自定义音效接口，支持自定义采样率
* 增加音频引擎终端与恢复功能
* 增加外部查询进行是否支持美颜的接口
* 增加本地画面预处理视频回调接口
* 增加房间成员无某个通话能力权限却使用相关通话能力而导致的异常通知的接口
* 增加获取版本号接口
* 增加获取时间戳接口

**2. SDK修改bug**

* 主播模式下视频软件编码效果优化
* 修复视频画面花屏、绿屏、倒播的问题
* 修复视频观看方偶现唇音不同步的问题
* 修复个别机型视频画面被压缩/拉伸的问题
* 修复关闭视频时，音频也会被短暂关闭的问题
* 修复视频高码率场景，实际码率达不到云配置码率的问题
* 修复主播场景下，部分观众方听不到声音的问题
* 修复音频伴奏内存未释放问题
* 修复若干Crash问题
* 主播接电话后硬编切软编
* 退房间时的偶现crash
* 在房间内调用stopcontext的保护
* 退出房间后继续发包的crash
* 修复收包时有可能的内存泄露
*  修复发送屏幕分享时，同时也可以发送摄像头视频大画面
*  修复当权限设置为只有下行权限时，请求不到画面的问题
* 修复没有上行权限又修改为有上行权限后，打开摄像头远端看不到其视频态的问题
*  修复打开美颜时断网后高概率crash问题
*  修复iOS7.1.2系统打开麦克风说话，房间其他成员听不到声音的问题
*  修复ipod touch6无法开启美颜的问题
*  修复iOS端请求其他人的视频，手动结束SDK的进程
*  偶现蓝屏重启的问题

## `AV_Android_SDK1.8.1    2016-06-06`
**1. SDK新增功能 **

* 视频硬件编码
* 视频采集支持16:9宽高比
* 增加是否有能力支持美颜接口
* 进房间速度优化
* 视频质量优化，分辨率/帧率与web配置联动，视频（软）编码输出提升至720P
* 音频质量优化，开放64码率
* 增加进房间不作请求，直接接收已有画面接口
* 增加不重入房间切换角色的接口
*  增加实时自定义音效接口，支持自定义采样率
* 增加音频引擎终端与恢复功能
* 增加外部查询进行是否支持美颜的接口
* 增加获取版本号接口
*  增加获取时间戳接口

**2. SDK修改bug**

* 主播模式下视频软件编码效果优化
* 修复视频画面花屏、绿屏、倒播的问题
* 修复视频观看方偶现唇音不同步的问题
* 修复个别机型视频画面被压缩/拉伸的问题
* 修复关闭视频时，音频也会被短暂关闭的问题
* 修复视频高码率场景，实际码率达不到云配置码率的问题
* 修复若干Crash问题
* 修复发送屏幕分享时，同时也可以发送摄像头视频大画面
* 修复当权限设置为只有下行权限时，请求不到画面的问题
* 修复没有上行权限又修改为有上行权限后，打开摄像头远端看不到其视频态的问题
* 修复调用getqualityparas接口偶现crash问题
* 修复开启硬件编码后打印日志过多问题
*  修复LG NEXUS6 Android 6.0切换摄像头花屏问题
* 修复Android端主播模式视频内存GC频繁的问题

## `AV_Windows_SDK1.8.1    2016-06-06`
**1. SDK新增功能 **

* 视频采集支持16:9宽高比
* 进房间速度优化
* 视频质量优化，分辨率/帧率与web配置联动，视频（软）编码输出提升至720P
* 音频质量优化，开放64码率
* 增加主播场景下开播模式高品质通话接口
* 增加低延时监听接口
* 增加进房间不作请求，直接接收已有画面接口
* 增加不重入房间切换角色的接口
* 增加实时自定义音效接口，支持自定义采样率
* 增加获取版本号接口

**2. SDK修改bug**

* 修复发送屏幕分享时，同时也可以发送摄像头视频大画面
* 修复当权限设置为只有下行权限时，请求不到画面的问题
* 修复没有上行权限又修改为有上行权限后，打开摄像头远端看不到其视频态的问题
* 修复麦克风热插拔后开启屏幕分享导致的1301错误问题

## `AV_iOS_SDK1.7    2016-3-17`

**1. SDK新增功能 **

* 增加了美颜接口
* IMSDK拆分，减少安装包体积
* 增加获取房间状态参数的接口
* 增加明文修改权限的接口

**2. SDK修改bug**

* 解决进入后台硬编码导致蓝屏的问题
* 解决网络状态变化可能引起的crash
* 解决请求屏幕分享画面，有时画面出现的时间很慢问题。

## `AV_Android_SDK1.7   2016-3-17`

**1. SDK新增功能 **

* 增加美颜接口
* 增加本地采集预处理接口
* 增加获取房间状态参数的接口
* 增加明文修改权限的接口
* 增加暴露系统摄像头对象接口，使得App可以控制设备的闪光灯

**2. SDK修改bug**

* 解决StopContext 之后 调用 DestroyContext crash。
* 解决进入房间，打开前置摄像头，开启闪光灯，无响应问题。
* 解决requestviewlist导致crash的问题

## `AV_Windows C++SDK1.7   2016-3-17`

**1. SDK新增功能**

* 增加接受邀请进入房间的能力
* 增加获取房间状态参数的接口
* 增加明文修改权限的接口

**2. SDK修改bug**

* 解决禁用PC系统的默认扬声器，热插拔USB接口的扬声器，听不到声音。



## `AV_iOS_SDK1.6    2016-1-11`

**1. SDK新增功能 **

* 新增屏幕分享功能，可以进行接收PC端分享的屏幕视频。
* 新增音频数据输入和输出能力。可以实现录音功、伴奏、KTV监听、自定义音效等功能。
* 终端网络类型上报。
* 完善通话质量tips内容、显示格式和显示风格。

**2. SDK修改bug**

* 解决在"解码-渲染"流程中，处理同一个人的视频帧时，由于图像分辨率变化而可能导致的crash或者画面花屏。
* 解决执行外部捕获相关逻辑后去开启摄像头可能导致的crash。

## `AV_Android_SDK1.6    2016-1-11`

**1. SDK新增功能 **

* 新增屏幕分享功能，可以进行接收PC端分享的屏幕视频。
* 新增音频数据输入和输出能力。可以实现录音功、伴奏、KTV监听、自定义音效等功能。
* 新增终端网络类型上报。
* 完善通话质量tips内容、显示格式和显示风格。
* 缩减SDK体积，大约减少80KB。

**2. SDK修改bug**

* 解决在"解码-渲染"流程中，处理同一个人的视频帧时，由于图像分辨率变化而可能导致的crash或者画面花屏。
* 改成同步调节音量，解决快速去调节音量可能导致没有起作用的问题。
* 解决执行外部捕获相关逻辑后去开启摄像头可能导致的crash。
* 解决反复执行“进入房间-打开摄像头-退出房间”过程中的偶现crash。

## `AV_Windows C++_SDK1.6    2016-1-11`

**1. SDK新增功能**

* 新增屏幕分享功能，可以进行发送和接收屏幕视频。
* 新增音频数据输入和输出能力。可以实现录音功、伴奏、KTV监听、自定义音效等功能。
* 完善通话质量tips内容、显示格式和显示风格。
* 缩减SDK体积，大约减少200KB。

**2. SDK修改bug**

* 解决在"解码-渲染"流程中，处理同一个人的视频帧时，由于图像分辨率变化而可能导致的crash或者画面花屏。
* 改成同步调节音量，解决快速去调节音量可能导致没有起作用的问题。
* 解决执行外部捕获相关逻辑后去开启摄像头可能导致的crash。
