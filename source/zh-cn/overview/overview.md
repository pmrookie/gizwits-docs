
title:  微信SDK
---
# 微信应用开发流程

## 概述

如果开发者有通过微信公众平台作为与最终消费者的交互界面的需求，您可以通过阅读本文档了解如何借助机智云以及微信公众号、微信硬件平台进行开发。由于基于微信公众号进行硬件设备的接入、控制需要与多个平台交互。所以，有必要对每个平台的作用有清晰的了解。

## 总体接入流程图



## 机智云

如图1在微信接入业务场景中，通过开发者中心（site.gizwits.com）的图形化界面定义设备功能，机智云自动生成设备MCU与通信模组之间的串口通信协议，开发者根据协议文档即可实现设备的联网能力。

如图2部分，设备接入机智云后，机智云提供了面向微信应用的API，提供传输设备数据到应用、应用向设备发起的控制信息的功能。

## 厂商服务器

厂商服务器是厂商为了满足自己的微信应用，独立部署的WEB系统。该系统通过机智云平台提供的API进行与设备的数据、控制的实时通讯，解决智能硬件接入的需求；通过访问微信公众号平台的API实现以微信为渠道服务厂商最终消费者的需求。

首先，开发者可以为自己的应用设计个性化的HTML交互界面与功能。（如图3、4部分）

## 微信服务器

微信服务器主要为设备与厂商服务器之间的通信提供了一系列的接口，主要包括微信用户账号与设备的绑定/解绑定、接受/发送设备消息等，具体接口及使用方法可查看微信官方文档，微信最近推出了微信硬件平台，在做微信接入前需要仔细了解微信公众号与微信硬件平台，提供的功能要在不断完善。

## 微信客户端

微信客户端提供了最终与用户交互的操作界面，可以理解为就是一个运行在手机的浏览器，只不过是运行在微信公众号这套体系下。开发者可通过自己申请的公众号管理后台配置自定义的菜单

# 了解微信

## 了解微信公众号平台

具体内容请参考[微信公众平台](http://mp.weixin.qq.com/wiki/home/index.html)


## 1.2. 机智云物联方案概况
![Alt text](/assets/test.png)
#### 1.3. 找到最合适的SDK
机智云目前提供3套SDK：iOS平台原生SDK、Android平台原生SDK、APICloud跨平台SDK。开发者可以根据项目需要自行选择，其中APICloud版本SDK可以用H5技术一次开发，同时适配iOS和Android两个平台，具体内容请参考：《APICloud SDK 集成指南》。
用于帮助企业和开发者将野狗快速接入应用的身份认证系统，一次身份认证打通野狗所有产品。还可以用于增强已有账户体系和简化新应用中账号系统的开发。
用于帮助企业和开发者将野狗快速接入应用的身份认证系统，一次身份认证打通野狗所有产品。还可以用于增强已有账户体系和简化新应用中账号系统的开发。
用于帮助企业和开发者将野狗快速接入应用的身份认证系统，一次身份认证打通野狗所有产品。还可以用于增强已有账户体系和简化新应用中账号系统的开发。
用于帮助企业和开发者将野狗快速接入应用的身份认证系统，一次身份认证打通野狗所有产品。还可以用于增强已有账户体系和简化新应用中账号系统的开发。
#### 1.4. 相关名词定义
##### 1.4.1. GAgent
全称Gizwits Agent，运行于Wi-Fi模块中，设备通过GAgent接入机智云服务器。 目前已兼容国内主流的Wi-Fi模块， 开发者也可以通过获取GAgent二次开发包实现自定义的模块接入机智云。
用于帮助企业和开发者将野狗快速接入应用的身份认证系统，一次身份认证打通野狗所有产品。还可以用于增强已有账户体系和简化新应用中账号系统的开发。
用于帮助企业和开发者将野狗快速接入应用的身份认证系统，一次身份认证打通野狗所有产品。还可以用于增强已有账户体系和简化新应用中账号系统的开发。
用于帮助企业和开发者将野狗快速接入应用的身份认证系统，一次身份认证打通野狗所有产品。还可以用于增强已有账户体系和简化新应用中账号系统的开发。
用于帮助企业和开发者将野狗快速接入应用的身份认证系统，一次身份认证打通野狗所有产品。还可以用于增强已有账户体系和简化新应用中账号系统的开发。
用于帮助企业和开发者将野狗快速接入应用的身份认证系统，一次身份认证打通野狗所有产品。还可以用于增强已有账户体系和简化新应用中账号系统的开发。


# 代码块
``` python
[GizWifiSDK shareInstance].delegate = self;
[GizWifiSDK startWithAppID:@"your_app_id"];
 
// 实现系统事件通知回调
- (void)wifiSDK:(GizWifiSDK *)wifiSDK didNotifyEvent:(GizEventType)eventType eventSource:(id)eventSource eventID:(GizWifiErrorCode)eventID eventMessage: (NSString *)eventMessage {
if(eventType == GizEventSDK)
{
     // SDK发生异常的通知
   NSLog(@"SDK event happened: [%@] = %@", @(eventID), eventMessage);
}
else if(eventType == GizEventDevice) 
{
    // 设备连接断开时可能产生的通知
    GizWifiDevice* mDevice = (GizWifiDevice*)eventSource;
    NSLog(@"device mac %@ disconnect caused by %@", mDevice.macAddress, eventMessage);
} 
else if(eventType == GizEventM2MService) 
{
     // M2M服务返回的异常通知
     NSLog(@"M2M domain %@ exception happened: [%@] = %@", (NSString*)eventSource, @(eventID), eventMessage);
} 
else if(eventType == GizEventToken)
{
    // token失效通知
    NSLog(@"token %@ expired: %@", (NSString*)eventSource, eventMessage);
}
```
