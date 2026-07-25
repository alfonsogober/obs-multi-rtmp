# About this fork

This is a fork of [sorayuki/obs-multi-rtmp](https://github.com/sorayuki/obs-multi-rtmp) with crash, thread-safety, and memory-leak fixes on top of v0.7.4, made after a full audit of the plugin source:

- Fixed heap corruption in the output edit dialog (an `obs_data` reference over-release; crashed OBS when changing protocol, encoder, or shared-encoder settings).
- Fixed a use-after-free when a stream stopped while its widget was being destroyed (profile switch, OBS exit, or target deletion) — output signal callbacks are now bound to the widget's lifetime.
- Moved encoder/scene-view teardown off the OBS signal thread to eliminate a race with stream start.
- Fixed null-pointer crashes when an output type is unavailable or an encoder reports no codec (likely cause of the Linux "Add new target" crash).
- Fixed leaks: settings object leaked per stream start, audio encoders leaked on extra tracks (Twitch VOD track), message boxes leaked per dialog.
- Fixed float encoder/service settings being silently saved as integers.
- Registered `obs_module_unload` so the frontend event callback can't fire against a destroyed dock during shutdown.

Prebuilt binaries for Windows, macOS, and Ubuntu are on the [releases page](https://github.com/alfonsogober/obs-multi-rtmp/releases). All credit for the plugin itself goes to SoraYuki — original README follows.

---

# [Homepage / 主页](https://sorayuki.github.io/obs-multi-rtmp)

## 为什么首页是日语？ / Why is the homepage in Japanese?

因为最初是做给管人用的。

Because it's originally made for virtual Youtubers (VTubers).

# 声明 

近日发现百度贴吧有个叫 maggot 的用户在售卖此插件。咸鱼上也有，没得救了。 

本插件免费使用，作者不收取费用。 

举报之后百度贴吧找我要软件著作权证明，累不爱。 


# Announcement

This plugin is provided for free, without a fee. 

Recently a Baidu Tieba account 'maggot' is selling this plugin. Please, don't buy it.


# お知らせ

本プラグインは無償で提供されるものです。

最近、Baidu Tiebaに「maggot」というアカウント名のユーザーがこのプラグインを販売する行為をしています。

決して購入はしないでください。


# Donate

如果你觉得这个工具很有用想要捐赠，这里是链接。注意：这不是提需求的渠道。

このツールの開発に支援もとい投げ銭をしたいと思った方は以下のリンクからお願いします。(機能のリクエストは受け付けていません)

If you find this tool useful and want to doante, here is the link. (Please do not donate for feature requests.)

## [paypal / 贝宝](https://paypal.me/sorayuki0)

## alipay / 支付宝

![alipay](./docs/zhi.png) 

## wechat / 微信
![wechat](./docs/wechat.jpg)

## Build

This project uses obs-plugintemplate.   
Please refer to obs-plugintemplate to understand how it works.
