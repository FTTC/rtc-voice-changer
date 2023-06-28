<p align="center">
  <a href="https://intl.cloud.tencent.com/products/trtc">
    <img width="200" src="https://web.sdk.qcloud.com/trtc/webrtc/assets/trtc-logo.png">
  </a>
</p>

<h1 align="center">rtc-voice-changer</h1>

<div align="center">

The RTCVoiceChanger plugin can be used in conjunction with the [TRTC Web SDK](https://www.npmjs.com/package/trtc-js-sdk) to change the voice on TRTC calls.

[![NPM version](https://img.shields.io/npm/v/rtc-voice-changer)](https://www.npmjs.com/package/rtc-voice-changer) [![NPM downloads](https://img.shields.io/npm/dw/rtc-voice-changer)](https://www.npmjs.com/package/rtc-voice-changer)  [![Documents](https://img.shields.io/badge/-Documents-blue)](https://github.com/FTTC/rtc-voice-changer)

</div>

English | [简体中文](https://github.com/FTTC/rtc-voice-changer/blob/master/README.zh-cn.md)
## Introduction
rtc-voice-changer is used to change the voice of TRTC's audio and video calls.

## Prerequisites
TRTC monthly subscription Premium and higher is required to use this plugin.

Supported browsers: Chrome 66+, Edge 79+, Safari 14.1+, Firefox 76+.

For better use of `rtc-voice-changer`, it is recommended that you use the latest version of Chrome.

## Installation
```shell
npm install rtc-voice-changer
```

## Feature Description
### Step 1. Initialize RTCVoiceChanger
```javascript
import RTCVoiceChanger from 'rtc-voice-changer';
const voiceChanger = new RTCVoiceChanger();
```

### Step 2. Create a processor instance to process audio and video streams

A processor can only process one stream.

```javascript
let localStream = TRTC.createStream({ audio: true, video: true });
await localStream.initialize();
const processor = voiceChanger.createProcessor({ userId, sdkAppId, userSig });

// 1-Brat 2-Loli 3-Uncle 4-Heavy Metal 5-Cold 6-Foreign Accent 7-Beast 8-Fat Otaku 9-Strong Current 10-Heavy Machinery 11-Ethereal
await processor.process(localStream, 1);

// Switch effects midway
processor.setEffect(3);
```

### Step 3. End the call and destroy resources
```javascript
await client.leave();
voiceChangerProcessor.destroy();
```

## API
### RTCVoiceChanger
Create a plugin instance

```javascript
const rtcVoiceChanger = new RTCVoiceChanger();
```

#### createProcessor(params)

Create a Processor instance

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
| sdkAppId | `number` | sdkAppId <br/>Get the sdkAppId information in **Application Information** after creating a new application by clicking **Application Management** > **Create Application** in the [Real-Time Audio and Video Console](https://console.tencentcloud.com/trtc/app/create). |
| userId   | `string` | User ID<br/>It is recommended to limit the length to 32 bytes, and only allow uppercase and lowercase English letters (a-zA-Z), numbers (0-9), underscores, and hyphens. |
| userSig  | `string` | UserSig signature<br/>Refer to [UserSig Related](https://www.tencentcloud.com/document/product/647/35166?lang=en) for how to calculate userSig. |


#### destroy()
Destroy the instance and release resources.

```javascript
voiceChangerProcessor.destroy();
```

### Processor

#### process(localStream, voiceType)

Add noise reduction effect to the audio of the local stream.

**Params:**

| Name        | Type          | Description                                                    |
|-------------|---------------|----------------------------------------------------------------|
| localStream | `LocalStream` | Local stream.                                                            |
| voiceType   | `number`      | 1-Brat 2-Loli 3-Uncle 4-Heavy Metal 5-Cold 6-Foreign Accent 7-Beast 8-Fat Otaku 9-Strong Current 10-Heavy Machinery 11-Ethereal. |


```javascript
await voiceChangerProcessor.process(localStream, 1);
```

#### setEffect(type)

Switch effects.

| Name        | Type          | Description                                                    |
|-------------|---------------|----------------------------------------------------------------|
| voiceType   | `number`      | 1-Brat 2-Loli 3-Uncle 4-Heavy Metal 5-Cold 6-Foreign Accent 7-Beast 8-Fat Otaku 9-Strong Current 10-Heavy Machinery 11-Ethereal. |

```javascript
await voiceChangerProcessor.setEffect(2);
```
#### close()

Turn off the voice changing effect.

```javascript
voiceChangerProcessor.close();
```

#### destroy()

Destroy the processor and release resources, ending the processor's lifecycle.

## Changelog

### Version 1.0.0 @2023.06.20
- Official Release 1.0.0

