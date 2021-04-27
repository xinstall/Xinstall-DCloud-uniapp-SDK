# DCloud接入
## 一、概述
Xinstall 支持 DCloud 平台的 uni-app 插件接入，你可以在 [DCloud 插件市场](https://ext.dcloud.net.cn/#) 中找到 Xinstall 插件（直接搜索 xinstall 即可），让你的 uni-app 应用快速集成 Xinstall 插件。

本插件封装了 Xinstall 官方SDK，是集智能传参、快速安装、一键拉起、客户来源统计等功能，帮您提高拉新转化率、安装率和多元化精确统计渠道效果的产品。为用户提供点击、安装、注册、留存、活跃等等精准统计报表，并可实时排重，杜绝渠道流量猫腻，大大降低运营成本。 具体详细介绍可前往 [Xinstall 官网](https://xinstall.com/) 进行查看。

![本文结构](https://cdn.xinstall.com/DCloudUniapp%E7%B4%A0%E6%9D%90/v1.0.0/step0.png)



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

#### 3.2、配置 scheme

在工程左边目录里找到 **mainfest.json** 文件，并点击该文件，在 **App常用其它配置** 中的 **Android设置 -> UrlSchemes** 框内填写 Xinstall 分配给应用的 scheme：

![配置scheme](https://cdn.xinstall.com/DCloudUniapp%E7%B4%A0%E6%9D%90/v1.0.0/step8.png)

**字段介绍：**

* UrlSchemes：如需使用一键拉起功能则必须配置。urlScheme 值详细获取位置：Xinstall 应用控制台-> Android集成-> 功能集成 中获取



#### 3.3、Universal links 相关配置（针对 iOS）

HBuilderX 2.3.0 开始云端打包支持配置 XCode 中的 Capabilities [参考文档](https://ask.dcloud.net.cn/article/36393)

**开启 Associated Domains 服务**

对于 iOS，为确保能正常使用一键拉起功能，AppID 必须开启 Associated Domains 功能，请到苹果开发者网站，选择 “Certificate, Identifiers & Profiles”，选择 iOS 对应的 AppID，开启 Associated Domains：

![开启 Associated Domains 服务](https://cdn.xinstall.com/DCloudUniapp%E7%B4%A0%E6%9D%90/v1.0.0/step9.png)

> 注意：当 AppID 重新编辑过之后，需要更新相应的 mobileprovision 文件，更新后在 HBuilderX 中进行云打包时也需要替换该 mobileprovision 文件。

**配置 Universal links 关联域名**

关联域名（Associated Domains）的值请在 Xinstall 控制台获取（Xinstall 应用控制台 -> iOS集成 -> 功能集成）

在 HBuilderX 中的 **manifest.json** 中配置关联域名（在 HBuilderX 中点击查看源码视图，或者使用其他编辑器工具打开这个文件）：

* 节点路径："app-plus" -> "distribute" -> "ios" -> "capabilities" -> "entitlements"
* 在对应节点下添加 `com.apple.developer.associated-domains` 字段，字段值为字符串数组，每个字符串为要关联的域名

``` xml
    "capabilities": {  
        "entitlements": {  
            "com.apple.developer.associated-domains": [  
                "Xinstall 分配给应用的关联域名"  
            ]  
        }  
    }
```

**示例图片：**

![配置关联域名](https://cdn.xinstall.com/DCloudUniapp%E7%B4%A0%E6%9D%90/v1.0.0/step10.png)



### 4、导出包上传 Xinstall

代码集成完毕后，需要通过 [发行]-[原生App-云打包] 导出 iOS 和 Android 安装包，并上传 Xinstall 控制台里对应的 App：

**示例图片（iOS 端）：** ![img](https://cdn.xinstall.com/DCloudUniapp%E7%B4%A0%E6%9D%90/v1.0.0/step11.png)

**示例图片（Android 端）：** ![img](https://cdn.xinstall.com/DCloudUniapp%E7%B4%A0%E6%9D%90/v1.0.0/step12.png)

上传完包后，需要进入 「iOS应用适配」和「Android应用配置」中选择下载的包的版本

**示例图片（iOS 端）：** ![img](https://cdn.xinstall.com/DCloudUniapp%E7%B4%A0%E6%9D%90/v1.0.0/step13.png)

![img](https://cdn.xinstall.com/DCloudUniapp%E7%B4%A0%E6%9D%90/v1.0.0/step14.png)

**示例图片（Android 端）：** ![img](https://cdn.xinstall.com/DCloudUniapp%E7%B4%A0%E6%9D%90/v1.0.0/step15.png)

![img](https://cdn.xinstall.com/DCloudUniapp%E7%B4%A0%E6%9D%90/v1.0.0/step16.png)

> 注意：每次上传完新的 ipa 或者 apk 包后，均需要进入「iOS应用适配」和「Android应用配置」中重新选择下载的包的版本





## 三、如何使用



### 1、快速下载和一键拉起

如果只需要快速下载功能和一键拉起，无需其它功能（携带参数安装、渠道统计），完成初始化配置即可。其他影响因素如下图
![](https://xinstall-static-pro.oss-cn-hangzhou.aliyuncs.com/APICloud%E7%B4%A0%E6%9D%90/v1.1.0/xinstall_yjlqksaztj.png)


### 2、携带参数安装/唤起

> 注意：调用该功能对应接口时需要在 Xinstall 中为对应 App 开通专业版服务

在 APP 需要安装参数时（由 web 网页中传递过来的，如邀请码、游戏房间号等动态参数），调用此接口，在回调中获取web中传递过来的参数，参数在App被一键唤起（拉起），或在快速下载第一次打开应用时候，会传递过来，App端可以分别从`addWakeUpEventListener `和`addInstallEventListener`两个方法中进行获取

#### addWakeUpEventListener

添加唤醒应用事件监听者。添加`addWakeUpEventListener`监听,当从其他应用一键唤起（拉起）本App时候，监听回调函数里可保存唤醒数据供后续业务使用。

**示例代码**

`addWakeUpEventListener(callback)`

**入参说明**：callback 为事件回调数据

**回调说明**：传入监听回调 callback(result)

result：

类型：JSON对象

内部字段：

```json
{
    channelCode: '渠道编号', //渠道编号
    data: '唤醒携带的参数'   //有携带参数，则返回数据，没有则为空
}
```

**调用示例**

```js
const xinstall = uni.requireNativePlugin('xinstall-plugin');
xinstall.addWakeUpEventListener(function(result){
  // 回调函数将在合适的时机被调用，这里编写拿到渠道编号以及唤醒数据后的业务逻辑代码
    var channelCode = result.channelCode;
  	var data = result.data;
});
```

**补充说明**

此方法用于获取动态唤醒参数，通过动态参数，在拉起APP时，获取由web网页中传递过来的，如邀请码、游戏房间号等自定义参数，通过注册监听后，获取web端传过来的自定义参数。请严格遵循示例中的调用顺序，否则可能导致获取不到唤醒参数。

**可用性**

Android系统，iOS系统

可提供的 1.0.0 及更高版本


#### addInstallEventListener

添加携带参数安装事件监听者。快速安装完成后，在 App 启动时（一般为入口程序处）需要通过`addInstallEventListener `该方法添加监听者。监听回调函数里可保存安装参数供后续业务使用。

**示例代码**

`addInstallEventListener(callback)`

**入参说明**：callback 为事件回调数据

**回调说明**：传入监听回调 callback(result)

result：

类型：JSON对象

内部字段：

```json
{
    channelCode: '渠道编号', //渠道编号
    data: '个性化安装携带的参数'   //有携带参数，则返回数据，没有则为空
}
```

**调用示例**

```js
const xinstall = uni.requireNativePlugin('xinstall-plugin');
xinstall.addInstallEventListener(function(result){
    // 回调函数将在合适的时机被调用，这里编写拿到渠道编号以及携带参数后的业务逻辑代码
    var channelCode = result.channelCode;
    var data = result.data;
);
```

**补充说明**

此接口用于获取动态安装参数，测试时候建议卸载再安装正确获取参数，在APP需要个性化安装参数时（由web网页中传递过来的，如邀请码、游戏房间号等自定义参数），在回调中获取参数，可实现跳转指定页面、统计渠道数据等。**调用该函数的时机建议越早越好，尽量在程序启动时进行注册，以免错过回调时机。**

**可用性**

Android系统，iOS系统

可提供的 1.0.0 及更高版本



### 3、高级数据统计

> 注意：调用该功能对应接口时需要在 Xinstall 中为对应 App 开通专业版服务



#### 3.1、注册量统计

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

Xinstall 会自动完成安装量、留存率、活跃量、在线时长等渠道统计数据的上报工作，如需统计每个渠道的注册量（对评估渠道质量很重要），可根据自身的业务规则，在确保用户完成 app 注册的情况下，调用 reportRegister()上报注册量。 在 Xinstall 平台即可看到注册量。

**可用性**

Android系统，iOS系统

可提供的 1.0.0 及更高版本



#### 3.2、事件统计

事件统计，主要用来统计终端用户对于某些特殊业务的使用效果，如充值金额，分享次数，广告浏览次数等等。

调用接口前，需要先进入 Xinstall 管理后台**事件统计**然后点击新增事件。



#### reportEventPoint

**示例代码**

`reportEventPoint(eventId, eventValue)`

**入参说明**：需要主动传入2个参数

- eventId：类型：字符串；描述：效果点ID，与 Xinstall 后台创建的效果点 ID 对应
- eventValue：类型：数字类型；描述：效果点值

**回调说明**：无需传入回调函数

**调用示例**

``` js
const xinstall = uni.requireNativePlugin('xinstall-plugin');
xinstall.reportEventPoint('createOrder', 13);
```

**补充说明**

只有 Xinstall 后台创建事件统计，并且代码中传递的事件ID与后台创建的ID一致时，上报数据才会被统计。

**可用性**

Android系统，iOS系统

可提供的 1.0.0 及更高版本


## 三、导出apk/ipa包并上传

参考官网文档

[iOS集成-导出ipa包并上传](https://doc.xinstall.com/integrationGuide/iOSIntegrationGuide.html#%E5%9B%9B%E3%80%81%E5%AF%BC%E5%87%BAipa%E5%8C%85%E5%B9%B6%E4%B8%8A%E4%BC%A0)

[Android集成-导出apk包并上传](https://doc.xinstall.com/integrationGuide/AndroidIntegrationGuide.html#%E5%9B%9B%E3%80%81%E5%AF%BC%E5%87%BAapk%E5%8C%85%E5%B9%B6%E4%B8%8A%E4%BC%A0)

## 四、如何测试功能

参考官方文档 [测试集成效果](https://doc.xinstall.com/integrationGuide/comfirm.html)

## 五、更多 Xinstall 进阶功能
若您想要自定义下载页面，或者查看数据报表等进阶功能，请移步 [Xinstall 官网](https://xinstall.com/) 查看对应文档。

若您在集成过程中如有任何疑问或者困难，可以随时联系 [Xinstall 官方客服](https://xinstall.com/) 在线解决。
