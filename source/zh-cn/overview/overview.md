
title:  iOS SDK 2.0
---
## 1. 设备接入SDK概述
### 1.1. SDK目的与功能

机智云的设备接入SDK（以下简称SDK）封装了手机（包括PAD等设备）与机智云智能硬件的通讯过程，以及手机与云端的通讯过程。这些过程包括配置入网、发现、连接、控制、心跳、状态上报、报警通知等。使用SDK，可以使得开发者快速完成APP开发，开发者仅需关注APP的UI和UE设计即可，而相对复杂的协议与错误处理等事项可忽略。 
相比之下，SDK在新接口定义上做了进一步的简化，使用流程更加简单了。APP已经完全不需要了解设备连接方面的概念，可以更专注于APP用户体验的优化设计。

### 1.2. 机智云物联方案概况

### 1.3. 找到最合适的SDK
机智云目前提供3套SDK：iOS平台原生SDK、Android平台原生SDK、APICloud跨平台SDK。开发者可以根据项目需要自行选择，其中APICloud版本SDK可以用H5技术一次开发，同时适配iOS和Android两个平台，具体内容请参考：《APICloud SDK 集成指南》。
### 1.4. 相关名词定义
#### 1.4.1. GAgent
全称Gizwits Agent，运行于Wi-Fi模块中，设备通过GAgent接入机智云服务器。 目前已兼容国内主流的Wi-Fi模块， 开发者也可以通过获取GAgent二次开发包实现自定义的模块接入机智云。


### 代码块
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

# 1. 设备接入SDK概述

## 1.1. SDK目的与功能

Wilddog Auth** 机智云的设备接入SDK（以下简称SDK）封装了手机（包括PAD等设备）与机智云智能硬件的通讯过程，以及手机与云端的通讯过程。这些过程包括配置入网、发现、连接、控制、心跳、状态上报、报警通知等。使用SDK，可以使得开发者快速完成APP开发，开发者仅需关注APP的UI和UE设计即可，而相对复杂的协议与错误处理等事项可忽略。 
相比之下，SDK在新接口定义上做了进一步的简化，使用流程更加简单了。APP已经完全不需要了解设备连接方面的概念，可以更专注于APP用户体验的优化设计。

## Wilddog Auth 能做什么

### 一次身份认证，打通野狗全部产品
与野狗实时数据同步（Sync）、通知（Notification）、实时音频通话（Voice）、实时视频通话（Video）、IM 等产品无缝集成。

### 增强已有账户体系
为应用增加更丰富的身份认证提供商，例如微博、微信、OpenID connect 等。

### 简化新应用的账户系统开发
极大地简化新应用的帐户系统开发。提供丰富的身份认证方式，开发者可以快速开发新应用，节省成本。

## Wilddog Auth 带来的好处

### 避免从 0 开始
让新应用避开从 0 开始的账户系统开发，轻松搞定用户注册登录，用户信息存储。
```javascript
console.log('hello world')
alert('fuck me plz')
```

### 提高账户安全性
野狗采用行业标准的 JWT 格式对传输数据进行加密，有效提高账号系统的安全性，防止用户信息泄漏。
```javascript
console.log('hello world')
alert('fuck me plz')
console.log('hello world')
alert('fuck me plz')
console.log('hello world')
alert('fuck me plz')
console.log('hello world')
alert('fuck me plz')
```

更多细节，请参考身份认证的 [快速入门](/quickstart/auth/web.html)。

![Alt text](/assets/test.png)
![Alt text](/assets/1.png)
![Alt text](/assets/2.png)
