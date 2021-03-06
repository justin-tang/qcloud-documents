## 基础知识
**推流**（也叫发布）是指将音视频数据采集编码之后，推送到您指定的视频云平台上，这里涉及大量的音视频基础知识，而且需要长时间的打磨和优化才能达到符合预期的效果。

腾讯云 RTMP SDK 主要帮您解决在智能手机上的推流问题，它的接口非常简单易用，只需要一个推流URL就能驱动：
![demo](http://qzonestyle.gtimg.cn/qzone/vas/opensns/res/img/pusher_demo_introduction_2.jpg)

## 特别说明
- **<font color='red'>不限制云服务商</font>**
> RTMP SDK 不会限制您**向非腾讯云地址推流**，但如何才能推流到非腾讯云地址呢？
> 
> 为解决国内 DNS 映射不准确的问题，SDK 1.5.2 版本开始引入就近选路，即通过腾讯云就近选路服务器选择离主播最优的推流线路，这一改进对推流质量提升很大。但相应的，选路结果中只有腾讯云的服务器地址。而且，由于我们大量的客户采用专属推流域名，SDK 无法简单通过 URL 文本分析就辨别出是不是推到腾讯云。
> 
> 所以，如果您需要推流到其他云商的推流地址，可以通过客服联系我们，我们可以为您的账号关闭就近选路。该项配置通过云控实现，故您不需要发布新的客户端版本来解决这个问题。

- **x86 模拟器调试**
> 由于RTMP SDK大量使用iOS系统的高级特性，我们不能保证所有特性在x86环境的模拟器下都能正常运行，而且音视频是性能敏感的功能，模拟器下的表现跟真机会有很大的不同。所以，如果条件允许，推荐您尽量使用真机调试。

## 准备工作

- **获取开发包**
[下载](https://www.qcloud.com/document/product/454/7873) RTMP SDK 开发包，并按照[工程配置](https://www.qcloud.com/document/product/454/7876)指引将 RTMP SDK 嵌入您的 APP 开发工程。

- **获取测试URL**
[开通](https://console.qcloud.com/live)直播服务后，可以使用 [直播控制台>>直播码接入>>推流生成器](https://console.qcloud.com/live/livecodemanage) 生成推流地址，详细信息可以参考 [获得推流播放URL](https://www.qcloud.com/document/product/454/7915)。


## 代码对接
本篇攻略主要是面向**摄像头直播**的解决方案，该方案主要用于美女秀场直播、活动直播等场景。如果您需要实现游戏录屏推流，请参考进阶功能区的游戏推流文档。

### step 1: 创建Push对象
先创建一个 **LivePush** 对象，我们后面主要用它来完成推流工作。

不过在创建 LivePush 对象之前，还需要您指定一个**LivePushConfig**对象，该对象的用途是决定 LivePush 推流时各个环节的配置参数，比如推流用多大的分辨率、每秒钟要多少帧画面（FPS）以及Gop（表示多少秒一个I帧）等等。

LivePushConfig 在alloc之后便已经装配了一些我们反复调过的参数，如果您不需要自己定制这些配置，简单的alloc出来并塞给LivePush对象就可以了。如果您有相关领域的经验基础，需要对这些默认配置进行调整，可以阅读**进阶篇**中的内容。

```objectivec   
// 创建 LivePushConfig 对象，该对象默认初始化为基础配置
 TXLivePushConfig* _config = [[TXLivePushConfig alloc] init];    
 //在 _config中您可以对推流的参数（如：美白，硬件加速，前后置摄像头等）做一些初始化操作，需要注意 _config不能为nil  
 _txLivePush = [[TXLivePush alloc] initWithConfig: _config];
```

### step 2: 给画面“找块地”
接下来我们要给摄像头的影像画面找个地方来显示，iOS系统中使用view作为基本的界面渲染单位，所以您只需要准备一个view传给 LivePush 对象的 **startPreview** 接口函数就可以了。

- **推荐的布局！**
> 实际上，RTMP SDK 的内部并不是直接把画面渲染在您提供的view上，而是在这个view之上创建一个用于OpenGL渲染的子视图（subView），但是，这个渲染用的subView的大小会跟随您提供的view大小变化而自动调整。
>![](//mccdn.qcloud.com/static/img/75b41bd0e9d8a6c2ec8406dc706de503/image.png)
>
> 不过即如此，如果您想要在渲染画面之上实现弹幕、献花之类的UI控件，我们也推荐您”另起炉灶“（再创建一个平级的view），这样可以避免很多前后画面覆盖的问题。

- **如何做动画？**
> 针对view做动画是比较自由的，不过请注意此处动画所修改的目标属性应该是<font color='red'>transform</font>属性而不是frame属性。
>
```objectivec
  [UIView animateWithDuration:0.5 animations:^{
            _myView.transform = CGAffineTransformMakeScale(0.3, 0.3); //缩小1/3
        }];
```

### step 3: 启动推流
经过step1 和 step2 的准备之后，用下面这段代码就可以启动推流了： 

```objectivec 
NSString* rtmpUrl = @"rtmp://2157.livepush.myqcloud.com/live/xxxxxx";    
[_txLivePush startPreview:_myView];  //_myView 就是step2中需要您指定的view    
[_txLivePush startPush:rtmpUrl];
```

- **startPush** 的作用是告诉 RTMP SDK 音视频流要推到哪个推流URL上去。
- **startPreview** 的参数就是step2中需要您指定的view，startPreview 的作用就是将界面view控件和LivePush对象关联起来，从而能够将手机摄像头采集到的画面渲染到屏幕上。

### step 4: 美颜滤镜
对于摄像头直播的场景，美颜是必不可少的一个功能点，本SDK提供了一种简单版实现，包含磨皮（level 1 -> level 10）和美白 (level 1 -> level 3)两个功能。

您可以在您的APP得用户操作界面上使用滑竿等控件来让用户选择美颜效果，或者推荐您也可以先用Demo里的滑竿进行，达到您满意的效果后，将此时的数值固定到程序的设置参数里。

接口函数setBeautyFilterDepth可以动态调整美颜及美白级别:

```objectivec
[_txLivePush setBeautyFilterDepth:_beauty_level setWhiteningFilterDepth:_whitening_level];
```

### step 5: 控制摄像头
- **切换前置或后置摄像头** 
默认是使用**前置**摄像头（可以通过修改 LivePushConfig 的配置项 frontCamera 来修改这个默认值），调用一次switchCamera 切换一次，注意切换摄像头前必须保证 LivePushConfig 和 LivePush 对象都已经初始化。  
  
```objectivec
// 默认是前置摄像头，可以通过修改 LivePushConfig 的配置项 frontCamera 来修改这个默认值   
[_txLivePush switchCamera];
```

- **打开或关闭闪光灯** 
只有后置摄像头才可以打开闪光灯（您可以通过"TXLivePush.h"里面的frontCamera成员来确认当前摄像头是前置还是后置）

```objectivec
if(!frontCamera) {
	BOOL bEnable = YES;
	//bEnable为YES，打开闪光灯; bEnable为NO，关闭闪光灯
	BOOL result = [_txLivePush toggleTorch: bEnable];
	//result为YES，打开成功;result为NO，打开失败
}
```

- **自定义手动对焦**
RTMP SDK 的iOS版本内部有默认的手动对焦逻辑，虽然功能没什么问题，但是经常由于屏幕的触控事件被抢占而无法发挥作用。同时，界面排布的自由我们原则上绝不能干预。
我们在新版本的 TXLivePush 里增加了一个 setFocusPosition 函数接口，您可以自己根据手指触控位置进行手动对焦。

```objectivec
// 如果客户调用这个接口，SDK内部触发对焦的逻辑将会停止，避免重复触发对焦逻辑
- (void)setFocusPosition:(CGPoint)touchPoint;
```

### step 6: 设置Logo水印
最近相关政策规定，直播的视频必须要打上水印，所以这个之前看起来并不是特别起眼的功能现在要重点说一下：
腾讯视频云目前支持两种水印设置方式：一种是在推流SDK进行设置，原理是在SDK内部进行视频编码前就给画面打上水印。另一种方式是在云端打水印，也就是云端对视频进行解析并添加水印Logo。

这里我们特别建议您使用<font color='red'>SDK添加水印</font>，因为在云端打水印有三个明显的问题：
 （1）这是一种很耗云端机器的服务，而且不是免费的，会拉高您的费用成本；
 （2）在云端打水印对于推流期间切换分辨率等情况的兼容并不理想，会有很多花屏的问题发生。
 （3）在云端打水印会引入额外的3s以上的视频延迟，这是转码服务所引入的。

SDK所要求的水印图片格式为png，因为png这种图片格式有透明度信息，因而能够更好地处理锯齿等问题。（您可千万别把jpg图片在windows下改个后缀名就塞进去了，专业的png图标都是需要由专业的美工设计师处理的）

```objectivec
//设置视频水印
_config.watermark = [UIImage imageNamed:@"watermark.png"];
_config.watermarkPos = (CGPoint){10, 10};
```

### step 7: 硬件加速
通过 LivePushConfig 里的 **enableHWAcceleration** 接口可以开启硬件编码。
```objectivec
//停止推流 （开启过程推荐同时重启推流，否则可能导致播放端花屏绿屏等问题）
[_txLivePush stopPush]
//开启硬件编码
txLivePush.config.enableHWAcceleration = YES;
//重启推流
[_txLivePush startPush:rtmpUrl]
```

- **推荐开启硬编**
iOS平台的机型数量并不像Android那么浩瀚，而且硬件质量也都非常过关，所以硬件加速在iOS平台是非常推荐的，可以放心开启。

- **最新美颜效果**
不少客户对老版本SDK的美颜不满意，所以 SDK 1.6.2 开始我们换用了新的美颜方案，但是新美颜算法的计算量要略大于老版本的美颜算法。由于测试团队对性能标准要求非常严格和苛刻，所以我们最终确定：<font color='red'>只有开启硬件加速的情况下才会启用新的美颜效果</font>。
  
- **避免中途切换**
避免在推流过程中开关硬件加速，虽然大部分情况下没有问题，但有各种异常隐患。推荐的做法是一开始就开启，而不是中途再打开。

> RTMP SDK 内部有一种保护机制：如果硬件加速资源被其它App占用导致无法开启，会自动切换回软件编码。

### step 8: 后台推流
常规模式下，App一旦切到后台，摄像头的采集能力就会被 iOS 暂时停止掉，这就意味着 SDK 不能再继续采集并编码出音视频数据。如果我们什么都不做，那么故事将按照如下的剧本发展下去：
+ 阶段一（切后台开始 -> 之后的10秒内）- CDN因为没有数据所以无法向观众提供视频流，观众看到画面卡主。
+ 阶段二（10秒 -> 70秒内）- 观众端的播放器因为持续收不到直播流而直接推出，直播间已经人去楼空。
+ 阶段三（70秒以后）- 推流的 RTMP 链路被服务器直接断掉，主播需要重新开启直播才能继续。

主播可能只是短暂接个紧急电话而已，但上述的交互体验显然会让观众全部离开直播间，怎么优化呢？
从 **SDK 1.6.1** 开始，我们引入了一种解决方案，如下是从观众端的视角看去，该方案可以达到的效果： 
![](//mc.qcloudimg.com/static/img/6325a9f7918602bd8db15228e6ffe189/image.png)

- **8.1) 设置pauseImg**
在开始推流前，使用 LivePushConfig 的 pauseImg 接口设置一张等待图片，图片含义推荐为“主播暂时离开一下下，稍后回来”。

- **8.2) 设置App后台（短暂）运行**
App 如果切后台后就彻底被休眠掉，那么 RTMP SDK 再有本事也无济于事，所以我们使用下面的代码让App在切到后台后还可再跑几分钟，这段时间如果主播应付一下紧急电话，也就算是“功德圆满”。

```objectivec
//先注册后退消息通知
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(handleEnterBackground:) 
    name:UIApplicationDidEnterBackgroundNotification object:nil];

//收到通知后，调用beginBackgroundTaskWithExpirationHandler
-(void)handleEnterBackground:(NSNotification *)notification
{
    [[UIApplication sharedApplication] beginBackgroundTaskWithExpirationHandler:^{
    }];
}
```
- **8.3) 切后台处理**
推流中，如果App被切了后台，也就是在 8.2 中的 handleEnterBackground 里，调用 TXLivePush 的 pausePush 接口函数，之后，RTMP SDK 虽然采集不到摄像头的画面了，但可以用您刚才设置的 pauseImg 持续推流。

```
//切后台处理： 在 8.2 的基础上补一句
- (void)handleEnterBackground:(NSNotification *)notification
{
    [[UIApplication sharedApplication] beginBackgroundTaskWithExpirationHandler:^{
    }];
	[_txLivePush pausePush];
}
```

- **8.4) 切前台处理**
 等待App切回前台之后，调用TXLivePush 的 resumePush 接口函数，之后，RTMP SDK 会继续采集摄像头的画面进行推流。
 
```objectivec
//切前台处理
- (void)handleEnterForeground:(NSNotification *)notification
{
    [_txLivePush resumePush];
}
```

### step 9: 推荐的清晰度
影响画质的主要因素是三个：**分辨率**、**帧率**和**码率**。
- **分辨率**：摄像头直播有三种 9:16 的常规分辨率可供选择：360\*640，540\*960，720\*1280。
- **帧率**：FPS <=10 会明显感觉到卡顿，摄像头直播推荐设置 20 FPS。
- **码率**：编码器每秒编出的数据大小，单位是kbps，比如800kbps代表编码器每秒产生800kb（或100KB）的数据。

好的画质是分辨率、帧率和码率三者之间的平衡，如下是几种清晰度档位的推荐设置结果。其中，括号中标注的是 LivePushConfig 的对应设置项：

| 档位   | 分辨率（videoResolution） | FPS（videoFPS） | 码率（videoBitratePIN） |
|---------|---------|---------|---------|
| 标清 | VIDEO_RESOLUTION_TYPE_360_640 | 20 | 700kbps |
| 高清 | VIDEO_RESOLUTION_TYPE_540_960 | 20 | 1000kbps | 
| 超清 | VIDEO_RESOLUTION_TYPE_720_1280 | 20 | 1500kbps |

> 美女秀场领域，我们的客户一般是选择**高清**档位，因为它比较平衡：720p超清档拍人像比较浪费，360p的效果又不能在清晰度上跟竞品拉开差距。

### step 10: 提醒主播“网络不好”
step 13 中会介绍 RTMP SDK 的推流事件处理，其中 **PUSH_WARNING_NET_BUSY** 这个很有用，它的含义是：<font color='blue'>**当前主播的上行网络质量很差，观众端已经出现了卡顿。**</font>

当收到此WARNING时，您可以通过UI提醒主播换一下网络出口，或者离WiFi近一点，或者让他吼一嗓子：“领导，我在直播呢，别上淘宝了行不！什么？没上淘宝？那韩剧也是一样的啊。”

### step 11: 横屏推流
大多数情况下，用户习惯以“竖屏持握”进行直播拍摄，观看端看到的也是竖屏样式；有时候用户在直播的时候需要更广的视角，则拍摄的时候需要“横屏持握”，这个时候其实是期望观看端能看到横屏画面，就需要做横屏推流，下面两幅示意图分别描述了横竖屏持握进行横竖屏推流在观众端看到的效果。
![](//mc.qcloudimg.com/static/img/cae1940763d5fd372ad962ed0e066b91/image.png)
> <font color='red'>**注意：**</font> 横屏推流和竖屏推流，观众端看到的图像的宽高比是不同的，竖屏9:16，横屏16：9。

要实现横屏推流，需要在两处进行设置：
#### 调整观众端表现
通过对 LivePushConfig 中的 **homeOrientation** 设置项进行配置，它控制的是观众端看到的视频宽高比是 **16:9** 还是 **6:19**，调整后的结果可以用播放器查看以确认是否符合预期。

| 设置项 | 含义 |
|:---------|---------|
| VIDEO_ANGLE_HOME_RIGHT     | home键在右 |
| VIDEO_ANGLE_HOME_DOWN     | home键在下 |
| VIDEO_ANGLE_HOME_LEFT       | home键在左 |
| VIDEO_ANGLE_HOME_UP           | home键在上 |

#### 调整主播端表现
接下来就看主播本地渲染是否正常，这里可以通过 TXLivePush 中的 setRenderRotation 接口来设置主播看到的画面的旋转方向。此接口提供了** 0，90，180，270** 四个参数供设置旋转角度。

### step 12: 背景混音
RTMP SDK 1.6.1 开始支持背景混音，支持主播带耳机和不带耳机两种场景，您可以通过 TXLivePush 中的如下这组接口实现背景混音功能：

| 接口 | 说明 |
|---------|---------|
| playBGM | 通过path传入一首歌曲，[小直播Demo](https://www.qcloud.com/doc/api/258/6164)中我们是从iOS的本地媒体库中获取音乐文件 |
| stopBGM|停止播放背景音乐|
| pauseBGM|暂停播放背景音乐|
| resumeBGM|继续播放背景音乐|
| setMicVolume|设置混音时麦克风的音量大小，推荐在UI上实现相应的一个滑动条，由主播自己设置|
| setBGMVolume|设置混音时背景音乐的音量大小，推荐在UI上实现相应的一个滑动条，由主播自己设置|

### step 13: 结束推流
结束推流很简单，不过要做好清理工作，因为用于推流的 TXLivePush 对象同一时刻只能有一个在运行，所以清理工作不当会导致下次直播遭受不良的影响。
```objectivec
//结束推流，注意做好清理工作
- (void)stopRtmpPublish {
    [_txLivePush stopPreview];
    [_txLivePush stopPush];
    _txLivePush.delegate = nil;
}
```

## 事件处理
### 1. 事件监听
RTMP SDK 通过 TXLive<font color='red'>Push</font>Listener 代理来监听推流相关的事件，注意 TXLive<font color='red'>Push</font>Listener 只能监听得到 <font color='red'>PUSH_</font> 前缀的推流事件。

### 2. 常规事件 
一次成功的推流都会通知的事件，比如收到1003就意味着摄像头的画面会开始渲染了

| 事件ID                 |    数值  |  含义说明                    |   
| :-------------------  |:-------- |  :------------------------ | 
|PUSH_EVT_CONNECT_SUCC            |  1001| 已经成功连接到腾讯云推流服务器|
|PUSH_EVT_PUSH_BEGIN              |  1002| 与服务器握手完毕,一切正常，准备开始推流|
|PUSH_EVT_OPEN_CAMERA_SUCC	  | 1003	| 推流器已成功打开摄像头（Android部分手机这个过程需要1-2秒）| 

### 3. 错误通知 
SDK发现了一些严重问题，推流无法继续了，比如用户禁用了APP的Camera权限导致摄像头打不开。

| 事件ID                 |    数值  |  含义说明                    |   
| :-------------------  |:-------- |  :------------------------ | 
|PUSH_ERR_OPEN_CAMERA_FAIL        | -1301| 打开摄像头失败|
|PUSH_ERR_OPEN_MIC_FAIL           | -1302| 打开麦克风失败|
|PUSH_ERR_VIDEO_ENCODE_FAIL       | -1303| 视频编码失败|
|PUSH_ERR_AUDIO_ENCODE_FAIL       | -1304| 音频编码失败|
|PUSH_ERR_UNSUPPORTED_RESOLUTION  | -1305| 不支持的视频分辨率|
|PUSH_ERR_UNSUPPORTED_SAMPLERATE  | -1306| 不支持的音频采样率|
|PUSH_ERR_NET_DISCONNECT          | -1307| 网络断连,且经三次抢救无效,可以放弃治疗,更多重试请自行重启推流|

### 4. 警告事件 
SDK发现了一些问题，但这并不意味着无可救药，很多 WARNING 都会触发一些重试性的保护逻辑或者恢复逻辑，而且有很大概率能够恢复，所以，千万不要“小题大做”哦。

- **WARNING_NET_BUSY**
主播网络不给力，如果您需要UI提示，这个 warning 相对比较有用（step10）。

- <font color='red'>**WARNING_SERVER_DISCONNECT**</font>
推流请求被后台拒绝了，出现这个问题一般是由于推流地址里的 txSecret 计算错了，或者是推流地址被其他人占用了（一个推流URL同时只能有一个端推流）。

| 事件ID                 |    数值  |  含义说明                    |   
| :-------------------  |:-------- |  :------------------------ | 
|PUSH_WARNING_NET_BUSY            |  1101| 网络状况不佳：上行带宽太小，上传数据受阻|
|PUSH_WARNING_RECONNECT           |  1102| 网络断连, 已启动自动重连 (自动重连连续失败超过三次会放弃)|
|PUSH_WARNING_HW_ACCELERATION_FAIL|  1103| 硬编码启动失败，采用软编码|
|PUSH_WARNING_DNS_FAIL			  |  3001 |  RTMP -DNS解析失败（会触发重试流程）        |
|PUSH_WARNING_SEVER_CONN_FAIL     |  3002|  RTMP服务器连接失败（会触发重试流程）  |
|PUSH_WARNING_SHAKE_FAIL          |  3003|  RTMP服务器握手失败（会触发重试流程）  |
|PUSH_WARNING_SERVER_DISCONNECT      |  3004|  RTMP服务器主动断开连接（会触发重试流程）  |
