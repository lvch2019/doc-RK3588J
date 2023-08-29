1. `ITX-3588J`出厂系统为`Android`,其他系统自行烧录到主板。
2. 升级方式: `USB线缆升级` 或`SD卡升级`固件
3. 启动模式
`ADB`  正常的启动过程
`Loader`	bootloader进入升级状态，等待主机命令，用于固件升级
`MaskRom` bootloader损坏系统修复

我们使用USB线缆升级固件(https://wiki.t-firefly.com/zh_CN/Core-3588J/upgrade_firmware.html)

升级流程:
1. 下载固件
2. 安装烧写工具(支持多操作系统的升级，目前对应的有linux，window，macos)
```
2.1 安装RK USB驱动
2.3 切换loader模式(方式1是使用recover键 方式2使用烧录工具"切换" 方式3是adb shell后输入reboot loader)
2.4 升级统一固件(后续如果自行修改内核, 
你需要先使用sdk 整体编译后，升级统一固件，再进行烧录boot.img ，你使用现成的固件进行烧录后，再烧录编译的boot.img ,版本异常异常到会导致系统跑不起来。)
```

建议: 
a. 如果只是熟悉官方的mpp和API,升级`统一固件`即可。
b. 后续如果需要做内核裁剪, 先下载SDK编译`统一固件`,然后针对需要`裁剪`的部分做单独编译镜像和升级镜像即可。
p.s 通过统一固件解包/打包工具，可以把统一固件解包为多个分区镜像，也可以将多个分区镜像合并为一个统一固件。

参考:
https://wiki.t-firefly.com/zh_CN/Core-3588J/upgrade_bootmode.html 
https://www.t-firefly.com/doc/download/160.html