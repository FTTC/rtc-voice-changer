<p align="center">
  <a href="https://intl.cloud.tencent.com/products/trtc">
    <img width="200" src="https://web.sdk.qcloud.com/trtc/webrtc/assets/trtc-logo.png">
  </a>
</p>

<h1 align="center">rtc-voice-changer</h1>

<div align="center">

RTCVoiceChanger 插件可以用来改变使用 [TRTC Web SDK](https://www.npmjs.com/package/trtc-js-sdk) 通话中的声音。

[![NPM version](https://img.shields.io/npm/v/rtc-voice-changer)](https://www.npmjs.com/package/rtc-voice-changer) [![NPM downloads](https://img.shields.io/npm/dw/rtc-voice-changer)](https://www.npmjs.com/package/rtc-voice-changer)  [![Documents](https://img.shields.io/badge/-Documents-blue)](https://github.com/FTTC/rtc-voice-changer)

</div>

简体中文 | [English](https://github.com/FTTC/rtc-voice-changer/blob/master/README.md)

## 简介
rtc-voice-changer 用来对 TRTC 进行的音视频通话进行变声。

## 前提条件

使用变声功能需开通 TRTC [包月套餐](https://cloud.tencent.com/document/product/647/85386) 尊享版及更高版本。

支持的浏览器：Chrome 66+, Edge 79+, Safari 14.1+, Firefox 76+。

为了更好的使用变声，建议您使用最新版本的 Chrome 浏览器。

## 安装
```shell
npm install rtc-voice-changer
```

## 实现流程
### Step 1. 初始化 RTCVoiceChanger
```javascript
import RTCVoiceChanger from 'rtc-voice-changer';
const voiceChanger = new RTCVoiceChanger();
```

### Step 2. 创建 processor 实例来处理音视频流

一个 processor 只能处理一条 stream

```javascript
let localStream = TRTC.createStream({ audio: true, video: true });
await localStream.initialize();
const processor = voiceChanger.createProcessor({ userId, sdkAppId, userSig });

// 1-熊孩子 2-萝莉 3-大叔 4-重金属 5-感冒 6-外语腔 7-困兽 8-肥宅 9-强电流 10-重机械 11-空灵
await processor.process(localStream, 1);

// 中途切换效果
processor.setEffect(3);
```

### Step 3. 结束通话销毁资源
```javascript
await client.leave();
processor.destroy();
```

## API
### RTCVoiceChanger
创建插件实例

```javascript
const rtcVoiceChanger = new RTCVoiceChanger();
```

#### createProcessor(params)

创建 Processor 实例

```javascript
const voiceChangerProcessor = await rtcVoiceChanger.createProcessor({
  sdkAppId,
  userId,
  userSig
});
```
**Params:**

| Name     | Type     | Description                                                  |
| -------- | -------- | ------------------------------------------------------------ |
| sdkAppId | `number` | sdkAppId <br/>在 [实时音视频控制台](https://console.cloud.tencent.com/trtc) 单击 **应用管理** > **创建应用** 创建新应用之后，即可在 **应用信息** 中获取 sdkAppId 信息。 |
| userId   | `string` | 用户ID<br/>建议限制长度为32字节，只允许包含大小写英文字母(a-zA-Z)、数字(0-9)及下划线和连词符。 |
| userSig  | `string` | userSig 签名<br/>计算 userSig 的方式请参考 [UserSig 相关](https://cloud.tencent.com/document/product/647/17275)。 |

#### destroy()

销毁实例，并释放资源

```javascript
voiceChangerProcessor.destroy();
```

### Processor

#### process(localStream, voiceType)
给本地流的音频增加降噪效果。
**Params:**

| Name        | Type          | Description                                                    |
|-------------|---------------|----------------------------------------------------------------|
| localStream | `LocalStream` | 本地流                                                            |
| voiceType   | `number`      | 1-熊孩子 2-萝莉 3-大叔 4-重金属 5-感冒 6-外语腔 7-困兽 8-肥宅 9-强电流 10-重机械 11-空灵。 |


```javascript
await voiceChangerProcessor.process(localStream, 1);
```

#### setEffect(type)
切换效果

| Name        | Type          | Description                                                    |
|-------------|---------------|----------------------------------------------------------------|
| voiceType   | `number`      | 1-熊孩子 2-萝莉 3-大叔 4-重金属 5-感冒 6-外语腔 7-困兽 8-肥宅 9-强电流 10-重机械 11-空灵。 |

```javascript
await voiceChangerProcessor.setEffect(2);
```
#### close()
关闭变声效果

```javascript
voiceChangerProcessor.close();
```

#### destroy()
销毁 processor 释放资源，结束 processor 生命周期。

## Changelog

### Version 1.0.0 @2023.06.20
- 正式发布 1.0.0 版本

