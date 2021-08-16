# DCloud接入
> 【重要说明】：从 v1.5.0 版本（含）开始，调用  Xinstall 插件的任意方法前，必须先调用一次初始化方法（init 或者 initWithAd），否则将导致其他方法无法正常调用。
>
> 从 v1.5.0 以下升级到 v1.5.0 以上版本后，需要自行修改代码调用初始化方法，Xinstall 插件无法在升级后自动兼容。

## 一、概述

Xinstall 支持 DCloud 平台的 uni-app 插件接入，你可以在 [DCloud 插件市场](https://ext.dcloud.net.cn/#) 中找到 Xinstall 插件（直接搜索 xinstall 即可），让你的 uni-app 应用快速集成 Xinstall 插件。

本插件封装了 Xinstall 官方 SDK，是集智能传参、快速安装、一键拉起、客户来源统计等功能，帮您提高拉新转化率、安装率和多元化精确统计渠道效果的产品。为用户提供点击、安装、注册、留存、活跃等等精准统计报表，并可实时排重，杜绝渠道流量猫腻，大大降低运营成本。 具体详细介绍可前往 [Xinstall 官网](https://xinstall.com/) 进行查看。

![本文结构](https://cdn.xinstall.com/DCloudUniapp%E7%B4%A0%E6%9D%90/v1.5.0/introduce.png)



## 二、如何接入

### 1、添加 Xinstall 插件

在 [DCloud 插件市场](https://ext.dcloud.net.cn/#) 中找到 Xinstall 插件，点击右侧购买：

![购买插件](https://cdn.xinstall.com/DCloudUniapp%E7%B4%A0%E6%9D%90/v1.0.0/step1.png)

在弹出的弹框中选择你的 uni-app 项目，并点击下一步：

![选择项目](https://cdn.xinstall.com/DCloudUniapp%E7%B4%A0%E6%9D%90/v1.0.0/step2.png)

输入 Android 和 iOS 对应的包名后，点击下一步：

![输入包名](https://cdn.xinstall.com/DCloudUniapp%E7%B4%A0%E6%9D%90/v1.0.0/step3.png)

根据后续提示完成插件购买。

完成插件购买后，在 HBuilderX 中进入对应项目，在左侧找到 **mainfest.json** 文件，点击后，找到 **App原生插件配置**，点击【选择云端插件】，勾选 **Xinstall-推广赋能专家** 后，点击【确认】按钮，完成插件集成：

![工程中添加插件](https://cdn.xinstall.com/DCloudUniapp%E7%B4%A0%E6%9D%90/v1.0.0/step6.png)

> 以上方法为云端集成插件，后续打包需使用 DCloud 官方 IDE：HBuilderX 进行云打包才能生效。

>   如您需要使用离线打包，则可点击【下载 for 离线打包】后，根据 [iOS 离线打包使用插件](https://nativesupport.dcloud.net.cn/NativePlugin/offline_package/ios?id=%e9%a2%84%e5%a4%87%e7%8e%af%e5%a2%83) 进行相应配置。配置过程中会涉及到部分重要参数，请在阅读完本章节后再进行离线打包配置。
>
>   若您使用离线打包，那么涉及 iOS 和 Android 两端的配置无法在 HBuilderX 中进行配置，如有需要，请联系 Xinstall 客户，我们会有专人进行配置指导。



### 2、创建 Xinstall 应用

进入 [Xinstall 官网](https://xinstall.com/) 注册账号，并在控制台中创建一个对应的应用，应用名字可以任意填写：

![创建应用](https://cdn.xinstall.com/DCloudUniapp%E7%B4%A0%E6%9D%90/v1.0.0/step4.png)

注意记录 Xinstall 中新创建应用的 appkey（后续配置需要用到）：

![记录appkey](https://cdn.xinstall.com/DCloudUniapp%E7%B4%A0%E6%9D%90/v1.0.0/step5.png)

接入过程中如有任何疑问或者困难，可以随时联系 [Xinstall 官方客服](https://xinstall.com/) 在线解决。



### 3、初始化配置

**进入 DCloud uni-app 应用的工程（使用 HBuilderX 打开），进行工程配置，配置完毕后，必须通过原生App-云打包生效，配置方法如下：**

#### 3.1、配置 appkey

在工程左边目录里找到 **mainfest.json** 文件，并点击该文件，在 **App原生插件配置** 中的 Xinstall 插件配置框内填写 Xinstall 分配给应用的 `AppKey`（填入 xinstall-uniapp-plugin 插件下的 APP_KEY 字段）：

![配置appkey](https://cdn.xinstall.com/DCloudUniapp%E7%B4%A0%E6%9D%90/v1.0.0/step7.png)

**字段介绍：**

* APP_KEY：插件接入前准备工作时，从 Xinstall 平台获取的 AppKey

> 【注意】：HBuilderX 3.1.1 ~ 3.1.2 版本存在 BUG，将导致 APP_KEY 输入框无法显示，从而无法输入。请将 HBuilderX 升级至 3.1.4 版本以上即可正常使用。

#### 3.2、配置 scheme

**配置 安卓 scheme**

在工程左边目录里找到 **mainfest.json** 文件，并点击该文件，在 **App常用其它配置** 中的 **Android设置 -> UrlSchemes** 框内填写 Xinstall 分配给应用的 scheme：

![配置scheme](https://cdn.xinstall.com/DCloudUniapp%E7%B4%A0%E6%9D%90/v1.0.0/step8.png)

**字段介绍：**

* UrlSchemes：如需使用一键拉起功能则必须配置。urlScheme 值详细获取位置：Xinstall 应用控制台 -> Android下载配置 中获取

**配置 iOS scheme**

在工程左边目录里找到 **mainfest.json** 文件，并点击该文件，在 **App常用其它配置** 中的 **iOS设置 -> UrlSchemes** 框内填写 Xinstall 分配给应用的 scheme：

![配置scheme](https://cdn.xinstall.com/DCloudUniapp%E7%B4%A0%E6%9D%90/v1.0.0/step19.png)

**字段介绍：**

* UrlSchemes：如需使用一键拉起功能则必须配置。urlScheme 值详细获取位置：Xinstall 应用控制台 -> iOS下载配置 中获取



#### 3.3、Universal links 相关配置（针对 iOS）

HBuilderX 2.3.0 开始云端打包支持配置 XCode 中的 Capabilities [参考文档](https://ask.dcloud.net.cn/article/36393)

**开启 Associated Domains 服务**

对于 iOS，为确保能正常使用一键拉起功能，AppID 必须开启 Associated Domains 功能，请到苹果开发者网站，选择 “Certificate, Identifiers & Profiles”，选择 iOS 对应的 AppID，开启 Associated Domains：

![开启 Associated Domains 服务](https://cdn.xinstall.com/DCloudUniapp%E7%B4%A0%E6%9D%90/v1.0.0/step9.png)

> 注意：当 AppID 重新编辑过之后，需要更新相应的 mobileprovision 描述文件并下载，下载后在 HBuilderX 中进行云打包时也需要替换该 mobileprovision 文件。
>
> 若对制作证书和描述文件的过程有疑问，可以参考 DCloud 的官方文章：[iOS证书(.p12)和描述文件(.mobileprovision)申请](https://ask.dcloud.net.cn/article/152)

**配置 Universal links 关联域名**

关联域名（Associated Domains）的值请在 Xinstall 控制台获取（Xinstall 应用控制台 -> iOS下载配置）

在 HBuilderX 中的 **manifest.json** 中配置关联域名（在 HBuilderX 中点击查看源码视图，或者使用其他编辑器工具打开这个文件）：

* 节点路径："app-plus" -> "distribute" -> "ios" -> "capabilities" -> "entitlements"
* 在对应节点下添加 `com.apple.developer.associated-domains` 字段，字段值为字符串数组，每个字符串为要关联的域名，一共需要添加两个：

``` xml
    "capabilities": {  
        "entitlements": {  
            "com.apple.developer.associated-domains": [  
                "Xinstall 分配给应用的关联域名1",
                "Xinstall 分配给应用的关联域名2"
            ]  
        }  
    }
```

> 若您的项目中已经有 `com.apple.developer.associated-domains` 字段，则直接在该数组中添加 Xinstall 分配给应用的关联域名 即可。

**示例图片：**

![配置关联域名](https://cdn.xinstall.com/DCloudUniapp%E7%B4%A0%E6%9D%90/v1.1.4/step10.png)



### 4、导出包上传 Xinstall

代码集成完毕后，需要通过 HBuilderX 菜单栏中的 [发行] - [原生App-云打包] 导出 iOS 和 Android 安装包，并上传 Xinstall 控制台里对应的 App：

**示例图片（iOS 端）：** ![img](https://cdn.xinstall.com/APICloud%E7%B4%A0%E6%9D%90/v1.1.0/step8.png)

**示例图片（Android 端）：** ![img](https://cdn.xinstall.com/APICloud%E7%B4%A0%E6%9D%90/v1.1.0/step9.png)

上传完包后，需要进入 「iOS下载配置」和「Android下载配置」中选择下载的包的版本

**示例图片（iOS 端）：** ![img](https://cdn.xinstall.com/APICloud%E7%B4%A0%E6%9D%90/v1.1.0/step10.png)

**示例图片（Android 端）：** ![img](https://cdn.xinstall.com/APICloud%E7%B4%A0%E6%9D%90/v1.1.0/step12.png)

> 注意：每次上传完新的 ipa 或者 apk 包后，均需要进入「iOS下载配置」和「Android下载配置」中重新选择下载的包的版本





## 三、如何使用



### 1、快速下载和一键拉起

如果只需要快速下载功能和一键拉起，无需其它功能（携带参数安装、渠道统计），完成初始化配置即可。其他影响因素如下图
![](https://xinstall-static-pro.oss-cn-hangzhou.aliyuncs.com/APICloud%E7%B4%A0%E6%9D%90/v1.1.0/xinstall_yjlqksaztj.png)



### 2、初始化 Xinstall 模块

> 注意：从 v1.5.0 版本开始，在调用 Xinstall 插件的任意方法之前，必须调用一次初始化方法，只需要调用一次即可，不需要反复调用。
>
> v1.5.0 之前的版本会在启动时自动初始化，无需调用，也无法调用。

#### init

初始化方法。在调用 Xinstall 插件其他方法之前必须调用一次该方法，否则其他方法均无法正常执行。

**示例代码**

`init()`

**入参说明**：无需主动传入参数

**回调说明**：无需传入回调函数

**调用示例**

```javascript
const xinstall = uni.requireNativePlugin('xinstall-plugin');
xinstall.init();
```

**可用性**

Android系统，iOS系统

可提供的 1.5.0 及更高版本



### 3、携带参数安装/唤起

> 注意：调用该功能对应接口时需要在 Xinstall 中为对应 App 开通专业版服务

在 APP 需要安装参数时（由 web 网页中传递过来的，如邀请码、游戏房间号等动态参数），调用此接口，在回调中获取web中传递过来的参数，参数在App被一键唤起（拉起），或在快速下载第一次打开应用时候，会传递过来，App端可以分别从 `addWakeUpEventListener ` 和 `addInstallEventListener` 两个方法中进行获取



#### addWakeUpEventListener

添加唤醒应用事件监听者。添加 `addWakeUpEventListener` 监听,当从其他应用一键唤起（拉起）本 App 时候，监听回调函数里可保存唤醒数据供后续业务使用。

**示例代码**

`addWakeUpEventListener(callback)`

**入参说明**：callback 为事件回调数据

**回调说明**：传入监听回调 callback(result)

result：

类型：JSON对象

内部字段：

```json
// 如果唤醒时没有携带任何参数，result 为一个空 json 对象：
{}

// 如果唤醒时有任意参数，result 为 json 对象，内部字段为：
{
    "channelCode":"渠道编号",  // 字符串类型。渠道编号，没有渠道编号时为 ""
    "data":{									// 对象类型。唤起时携带的参数。
        "co":{								// co 为唤醒页面中通过 Xinstall Web SDK 中的点击按钮传递的数据，key & value 均可自定义，key & value 数量不限制
            "自定义key1":"自定义value1", 
            "自定义key2":"自定义value2"
        },
        "uo":{   							// uo 为唤醒页面 URL 中 ? 后面携带的标准 GET 参数，key & value 均可自定义，key & value 数量不限制
            "自定义key1":"自定义value1",
            "自定义key2":"自定义value2"
        }
    }
}
```

**调用示例**

```js
const xinstall = uni.requireNativePlugin('xinstall-plugin');
xinstall.addWakeUpEventListener(function(result){
  // 回调函数将在合适的时机被调用，这里编写拿到渠道编号以及唤醒数据后的业务逻辑代码

  // 空对象时代表唤醒了，但是没有任何参数传递进来
  if (JSON.stringify(result) == '{}') {
    // 业务逻辑
  } else {
		var channelCode = result.channelCode;
    var data = result.data;
    var co = data.co;
    var uo = data.uo;
    // 根据获取到的数据做对应业务逻辑
  }
});
```

**补充说明**

此方法用于获取动态唤醒参数，通过动态参数，在拉起 APP 时，获取由 web 网页中传递过来的，如邀请码、游戏房间号等自定义参数，通过注册监听后，获取 web 端传过来的自定义参数。请严格遵循示例中的调用顺序，否则可能导致获取不到唤醒参数。

##### 【注意】Android 在开启应用宝功能后一键拉起配置

如果我们在 Xinstall 后台对应 App 的 [安卓下载配置] 中开启应用宝功能，现在只支持**离线打包**。具体操作如下

1. 在 App 的 **AndroidManifest.xml** 文件中将应用入口的 Activity io.dcloud.PandoraEntry 替换成 com.shubao.xinstallunisdk.XinstallPandoraEntry ，同时加入 android:launchMode="singleTask"

   具体样例如下：

   ```xml
   <!-- 应用入口 -->
   
           <activity
               android:name="com.shubao.xinstallunisdk.XinstallPandoraEntry"
               android:theme="@style/TranslucentTheme"
               android:configChanges="orientation|keyboardHidden|screenSize|mcc|mnc|fontScale"
               android:hardwareAccelerated="true"
               android:launchMode="singleTask"
               android:windowSoftInputMode="adjustResize">
               <intent-filter>
                   <data android:scheme="hbuilder"/>
                   <action android:name="android.intent.action.VIEW"/>
   
                   <category android:name="android.intent.category.DEFAULT"/>
                   <category android:name="android.intent.category.BROWSABLE"/>
               </intent-filter>
               <intent-filter>
                   <data android:mimeType="image/*"/>
                   <action android:name="android.intent.action.SEND"/>
                   <category android:name="android.intent.category.DEFAULT"/>
               </intent-filter>
               <intent-filter>
                   <action android:name="android.intent.action.MAIN"/>
                   <category android:name="android.intent.category.LAUNCHER"/>
               </intent-filter>
   
               <intent-filter>
                   <action android:name="android.intent.action.VIEW" />
   
                   <category android:name="android.intent.category.DEFAULT" />
                   <category android:name="android.intent.category.BROWSABLE" />
                   <data android:scheme="XINSTALL_SCHEME" />
               </intent-filter>
           </activity>
   ```


**可用性**

Android系统，iOS系统

可提供的 1.0.0 及更高版本



#### addInstallEventListener

添加携带参数安装事件监听者。快速安装完成后，在 App 启动时（一般为入口程序处）需要通过 `addInstallEventListener ` 方法添加监听者。监听回调函数里可保存安装参数供后续业务使用。

**示例代码**

`addInstallEventListener(callback)`

**入参说明**：callback 为事件回调数据

**回调说明**：传入监听回调 callback(result)

result：

类型：JSON对象

内部字段：

```json
// 如果没有获取到安装时携带的参数，result 为一个空 json 对象：
{}

// 获取到了安装时携带的参数，result 为 json 对象，内部字段为：
{
    "channelCode":"渠道编号",  // 字符串类型。渠道编号，没有渠道编号时为 ""
    "data":{									// 对象类型。安装时携带的参数。
        "co":{								// co 为唤醒页面中通过 Xinstall Web SDK 中的点击按钮传递的数据，key & value 均可自定义，key & value 数量不限制
            "自定义key1":"自定义value1", 
            "自定义key2":"自定义value2"
        },
        "uo":{   							// uo 为唤醒页面 URL 中 ? 后面携带的标准 GET 参数，key & value 均可自定义，key & value 数量不限制
            "自定义key1":"自定义value1",
            "自定义key2":"自定义value2"
        }
    },
  	timeSpan: 12, // 数字类型。代表下载页面上点击开始下载按钮与第一次打开App时的时间间隔，单位为秒
  	isFirstFetch: true // boolean类型。代表是否为第一次获取到安装参数，只有第一次获取到时为 true
}
```

**调用示例**

```js
const xinstall = uni.requireNativePlugin('xinstall-plugin');
xinstall.addInstallEventListener(function(result){
  // 回调函数将在合适的时机被调用，这里编写拿到渠道编号以及携带参数后的业务逻辑代码
  
  // 空对象时代表没有获取到安装参数
  if (JSON.stringify(result) == '{}') {
    // 业务逻辑
  } else {
    var channelCode = result.channelCode;
    var data = result.data;
    var co = data.co;
    var uo = data.uo;
    var timeSpan = result.timeSpan;
    var isFirstFetch = result.isFirstFetch;
    // 根据获取到的数据做对应业务逻辑
  }
});
```

**补充说明**

此接口用于获取动态安装参数，测试时候建议卸载再安装正确获取参数，在 APP 需要个性化安装参数时（由 web 网页中传递过来的，如邀请码、游戏房间号等自定义参数），在回调中获取参数，可实现跳转指定页面、统计渠道数据等。**调用该函数的时机建议越早越好，尽量在程序启动时进行注册，以免错过回调时机。**

**可用性**

Android系统，iOS系统

可提供的 1.0.0 及更高版本



### 4、渠道统计

> 注意：调用该功能对应接口时需要在 Xinstall 中为对应 App 开通专业版服务

#### 4.1、注册量统计

在业务中合适的时机（一般指用户注册）调用指定方法上报注册量



#### reportRegister

**示例代码**

`reportRegister()`

**入参说明**：无需主动传入参数

**回调说明**：无需传入回调函数

**调用示例**

``` js
const xinstall = uni.requireNativePlugin('xinstall-plugin');
xinstall.reportRegister();
```

**补充说明**

Xinstall 会自动完成安装量、留存率、活跃量、在线时长等渠道统计数据的上报工作，如需统计每个渠道的注册量（对评估渠道质量很重要），可根据自身的业务规则，在确保用户完成 App 注册的情况下，调用 `reportRegister()` 上报注册量。 在 Xinstall 平台即可看到注册量。

**可用性**

Android系统，iOS系统

可提供的 1.0.0 及更高版本



#### 4.2、事件统计

事件统计，主要用来统计终端用户对于某些特殊业务的使用效果，如充值金额，分享次数，广告浏览次数等等。

调用接口前，需要先进入 Xinstall 管理后台**事件统计**然后点击新增事件。



#### reportEventPoint

**示例代码**

`reportEventPoint(eventId, eventValue)`

**入参说明**：需要主动传入2个参数

- eventId：类型：字符串；描述：事件ID，与 Xinstall 后台创建的事件 ID 对应
- eventValue：类型：数字类型；描述：事件值

**回调说明**：无需传入回调函数

**调用示例**

``` js
const xinstall = uni.requireNativePlugin('xinstall-plugin');
xinstall.reportEventPoint('createOrder', 10);
```

**补充说明**

只有 Xinstall 后台创建事件统计，并且代码中传递的事件ID与后台创建的ID一致时，上报数据才会被统计。

**可用性**

Android系统，iOS系统

可提供的 1.0.0 及更高版本



### 5、广告平台渠道功能

>  如果您在 Xinstall 管理后台对应 App 中，**只使用「自建渠道」，而不使用「广告平台渠道」，则无需进行本小节中额外的集成工作**，也能正常使用 Xinstall 提供的其他功能。
>
>  注意：根据目前已有的各大主流广告平台的统计方式，目前 iOS 端和 Android 端均需要用户授权并获取一些设备关键值后才能正常进行 [ 广告平台渠道 ] 的统计，如 IDFA / OAID / GAID 等，对该行为敏感的 App 请慎重使用该功能。

#### 5.1、配置工作

**iOS 端：**

首先需要在 HBuilderX 中的 manifest.json 中的 [App常用其他设置]  中，**勾选 「使用广告标识（IDFA）」**：

![勾选使用广告标识](https://cdn.xinstall.com/DCloudUniapp%E7%B4%A0%E6%9D%90/v1.5.0/step_idfa_1.png)

从 iOS 14 开始，获取 IDFA 前将会提示用户获取权限，故**需要在 HBuilderX 中的 manifest.json 中的 [App权限配置] - [跟踪用户的活动] 中配置 IDFA 权限的说明文字**：

> 注意：在 DCloud 中，该配置项不填写时，HBuilderX 会在云打包时，默认填写该权限的说明文字：“ 请放心，开启权限不会获取您在其他站点的隐私信息，该权限仅用于标识设备并保障服务安全与提示浏览体验 ”

![填写获取 IDFA 权限的说明文字](https://cdn.xinstall.com/DCloudUniapp%E7%B4%A0%E6%9D%90/v1.5.0/step_idfa_2.png)



**Android 端：**

Android SDK有使用到IMEI,所以需要要授权，因此需要在`manifest.json`中声明权限，在 “App模块权限配置” 的 “Android打包权限配置” 勾选上`<uses-permission android:name="android.permission.READ_PHONE_STATE"/>`

![IMEI 权限配置](https://cdn.xinstall.com/DCloudUniapp%E7%B4%A0%E6%9D%90/v1.5.0/step_idfa_3.png)

在`manifest.json`中设置，关闭`uni-app`自动获取`android.permission.READ_PHONE_STATE`权限

```json
{
    "app-plus" : {
        "distribute" : {
            "android" : {
                "permissionPhoneState" : {
                    "request" : "none",
                    "prompt" : ""
                },
            }
        }
    }
}
```

#### 5.2、更换初始化方法

**使用新的 initWithAd 方法，替代原先的 init 方法来进行模块的初始化**

> 【重要说明】：接入广告平台渠道功能时，必须保证 HBuilderX 的版本 >= 3.1.4 ，否则将导致无法正常使用！同时由于目前 DCloud 官方给出的获取 IDFA 方案均存在缺陷，故 iOS 端的 vue 代码会比较复杂，接入时可直接复制代码到您的项目中。
>
> 

#### initWithAd

**示例代码**

`initWithAd(params)` 

**入参说明**：需要主动传入参数，JSON对象

入参内部字段：

* iOS 端：
  <table>
         <tr>
             <th>参数名</th>
             <th>参数类型</th>
             <th>描述 </th>
         </tr>
         <tr>
             <th>idfa</th>
             <th>字符串</th>
             <th>iOS 系统中的广告标识符</th>
         </tr>
     </table>


* Android 端：

  <table>
            <tr>
                <th>参数名</th>
                <th>参数类型</th>
                <th>描述 </th>
            </tr>
            <tr>
                <th>adEnabled</th>
                <th>boolean</th>
                <th>是否使用广告功能</th>
            </tr>
    				<tr>
                <th>oaid （可选）</th>
                <th>string</th>
                <th>OAID</th>
            </tr>
    				<tr>
                <th>gaid（可选）</th>
                <th>string</th>
                <th>GaID(google Ad ID)</th>
            </tr>
        </table>



**回调说明**：无需传入回调函数

**调用示例**

```javascript
const xinstall = uni.requireNativePlugin('xinstall-plugin');
// 由于 iOS 和 Android 两端需要传入的参数不同，故需要根据平台进行判断，传入不同的参数

if (uni.getSystemInfoSync().platform == 'ios') {
  let iOSVersion = uni.getSystemInfoSync().system.split(' ')[1];
  if (iOSVersion.indexOf("14.") == 0) {
    var ATTrackingManager = plus.ios.importClass("ATTrackingManager");
    var idfaStatus = ATTrackingManager.trackingAuthorizationStatus();
    if (idfaStatus == 0) {
      // 等待授权完成
      let waitIDFAAuth = setInterval(function() {
        idfaStatus = ATTrackingManager.trackingAuthorizationStatus();

        if (idfaStatus != 0) {
          clearInterval(waitIDFAAuth);

          var advertisingIdentifier = plus.ios.importClass("ASIdentifierManager").sharedManager().advertisingIdentifier();  
          var idfa = plus.ios.invoke(advertisingIdentifier,"UUIDString");  
          xinstall.initWithAd(idfa);
        }
      }, 1000)
    } else {
      var advertisingIdentifier = plus.ios.importClass("ASIdentifierManager").sharedManager().advertisingIdentifier();  
      var idfa = plus.ios.invoke(advertisingIdentifier,"UUIDString");  
      xinstall.initWithAd(idfa);
   }
  } else {
    var advertisingIdentifier = plus.ios.importClass("ASIdentifierManager").sharedManager().advertisingIdentifier();
    var idfa = plus.ios.invoke(advertisingIdentifier,"UUIDString");  
    xinstall.initWithAd(idfa);
  }
} else if (uni.getSystemInfoSync().platform == 'android') {
  plus.android.requestPermissions(["android.permission.READ_PHONE_STATE"], function(event) {
    if(event.granted){
      console.log(event.granted);
    }
    if(event.deniedPresent){
      console.log(event.deniedPresent);
    }
    if(event.deniedAlways){
      console.log(event.deniedAlways);
    }
    // 配置初始化，设置 OAID 和 GAID OAID SDK需要用户自行接入
    var params = {
      adEnable: true,
      oaid: "oaid测试",
      gaid: "gaid测试"
    };

    xinstall.initWithAd(params);

    // 如果想在初始化之后立即调用方法
    // 也可以使用
    // xinstall.initWithAd(params,function() {

    //});
  }, function(event) {
    // 权限申请错误
  });
}
```

**可用性**

Android系统，iOS系统

可提供的 1.5.0 及更高版本



#### 5.3、上架须知

**在使用了广告平台渠道后，若您的 App 需要上架，请认真阅读本段内容。**

##### 5.3.1 iOS 端：上架 App Store

1. 如果您的 App 没有接入苹果广告（即在 App 中显示苹果投放的广告），那么在提交审核时，在广告标识符中，请按照下图勾选：

![IDFA](https://cdn.xinstall.com/iOS_SDK%E7%B4%A0%E6%9D%90/IDFA_7.png)



1. 在 App Store Connect 对应 App —「App隐私」—「数据类型」选项中，需要选择：**“是，我们会从此 App 中收集数据”**：

![AppStore_IDFA_1](https://cdn.xinstall.com/iOS_SDK%E7%B4%A0%E6%9D%90/IDFA_1.png)

在下一步中，勾选「设备 ID」并点击【发布】按钮：

![AppStore_IDFA_2](https://cdn.xinstall.com/iOS_SDK%E7%B4%A0%E6%9D%90/IDFA_2.png)

点击【设置设备 ID】按钮后，在弹出的弹框中，根据实际情况进行勾选：

- 如果您仅仅是接入了 Xinstall 广告平台而使用了 IDFA，那么只需要勾选：**第三方广告**
- 如果您在接入 Xinstall 广告平台之外，还自行使用 IDFA 进行别的用途，那么在勾选 **第三方广告** 后，还需要您根据您的实际使用情况，进行其他选项的勾选

![AppStore_IDFA_3](https://cdn.xinstall.com/iOS_SDK%E7%B4%A0%E6%9D%90/IDFA_3.png)

![AppStore_IDFA_4](https://cdn.xinstall.com/iOS_SDK%E7%B4%A0%E6%9D%90/IDFA_4.png)

勾选完成后点击【下一步】按钮，在 **“从此 App 中收集的设备 ID 是否与用户身份关联？”** 选项中，请根据如下情况进行选择：

- 如果您仅仅是接入了 Xinstall 广告平台而使用了 IDFA，那么选择 **“否，从此 App 中收集的设备 ID 未与用户身份关联”**
- 如果您在接入 Xinstall 广告平台之外，还自行使用 IDFA 进行别的用途，那么请根据您的实际情况选择对应的选项

![AppStore_IDFA_5](https://cdn.xinstall.com/iOS_SDK%E7%B4%A0%E6%9D%90/IDFA_5.png)

最后，在弹出的弹框中，选择 **“是，我们会将设备 ID 用于追踪目的”**，并点击【发布】按钮：

![AppStore_IDFA_6](https://cdn.xinstall.com/iOS_SDK%E7%B4%A0%E6%9D%90/IDFA_6.png)





## 四、如何测试功能

参考官方文档 [测试集成效果](https://doc.xinstall.com/integrationGuide/comfirm.html)



## 五、更多 Xinstall 进阶功能

若您想要自定义下载页面，或者查看数据报表等进阶功能，请移步 [Xinstall 官网](https://xinstall.com/) 查看对应文档。

若您在集成过程中如有任何疑问或者困难，可以随时联系 [Xinstall 官方客服](https://xinstall.com/) 在线解决。
