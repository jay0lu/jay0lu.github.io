---
layout: default
title: Set bluetooth AptX connection on MacOS Mac上设置AptX连接
comments: true
---

## Enable AptX:
`sudo defaults write bluetoothaudiod "Enable AptX codec" -bool true`

## Enable AAC:
`sudo defaults write bluetoothaudiod "Enable AAC codec" -bool true`

Or go to apple developer page, Download `Additional Tools for Xcode`

Run Hardware/Bluetooth Explorer, then go to Tools>Audio Options. Select “Enable AAC”. If you have an aptX-only device you can enable that here as well. If your headset is already connected, disconnect and reconnect. You don’t need to re-pair the device.


***

下载 `Additional Tools for Xcode`，
打开， Hardware/Bluetooth， 状态栏/Tools>Audio Options， 勾选Enable AAC，aptx。
断开已连接的蓝牙设备，重连。
Done！