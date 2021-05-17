# Hackintosh-MSI-B460M-MORTAR-WIFI-i5-10500-iGPU-UHD630
微星B460M迫击炮wifi版主板黑苹果引导文件 

   
一、硬件配置

	CPU：I5-10500

	主板：迫击炮B460M MORTAR wifi版

	内存：金士顿2666 8G*2

	显卡：核显 UHD630

	wifi：主板内置 Intel AX200

	蓝牙：主板内置 Intel AX200

	BIOS版本：7C82v11

   	CPU支持:支持所有10代核显为UHD630的CPU,无核显带F的10代CPU，有以下免驱独显也可以（但无法使用核显加速）

   显卡支持：

   	支持仅有CPU核显的UHD630显卡
   	支持AMD独显 RX 470/480/570/570X/580/580X/590 系列显卡
   	支持AMD独显 RX 5500/5600/5700 系列显卡(需使用专用config.plist)

	PS: 使用独显的需在BIOS里强制打开CPU核显（高级 -> 内建显示配置 -> 集成显卡多显示器(IGD Multi-monitor) -> 允许），否则核显硬件解码失效，只使用核显的可以忽略

二、功能测试

		睡眠/唤醒------------正常

		所有USB端口----------正常

		核显硬件加速----------正常

		板载声卡-------------正常

		板载网卡-------------正常

		板载wifi AX200------正常

		板载蓝牙-------------正常
   
三、相关配置

（一）BIOS设置：

   USB设备从S3/S4/S5唤醒：允许
   PS/2鼠标从S3/S4/S5唤醒：允许
   USB键盘从S3/S4/S5唤醒：任意键
   集成显卡多显示器：允许（否则核显硬件解码失效，只使用核显的可以忽略）
   OC -> CPU 特征 -> Intel 虚拟化技术：允许
   OC -> CPU 特征 -> Intel VT-D 技术：禁止
   OC -> CPU 特征 -> CFG锁定：禁止

（二）OpenCore: 0.6.7

（三）EFI: <a href="https://github.com/QQ3233/Hackintosh-MSI-B460M-MORTAR-WIFI-i5-10500-iGPU-UHD630/releases/tag/1.0">下载地址</a>

   PS: 开机界面非图形界面直接选择 Reset NVRAM 选项，图形界面在选择启动盘时按空格，再选中 Reset NVRAM 选项，(回车键)重置NVRAM，重置后可能需要在BIOS中重新设置磁盘启动优先顺序

（四）系统macOS Big Sur 11.3 (注意: 安装系统时分区格式选择APFS, 而不是MacOS扩展日志式)

（五）系统安装:

   建议使用 【黑果小兵】macOS BigSur 11.1 安装镜像进行安装。若安装镜像卡加号或其它异常无法安装，可使用本EFI替换安装镜像的EFI进行尝试 (本EFI请使用config_install.plist配置文件，即删除原config.plist后重命名config_install.plist为config.plist即可)。系统安装成功后，替换为本EFI默认的config.plist文件即可

（六）若使用4K显示器，请将 "UIScale" 的值修改为 "Ag==" 以获得最佳ui体验

    <key>UIScale</key>
    <data>Ag==</data>

（七）板载网卡设置

    系统偏好设置 -> 网络 -> 以太网（高级） -> 硬件 -> 配置:手动, 速度:100baseTX(千兆网络环境可选择1000baseT), 双工:全双工, MTU:标准1500

四、常见故障处理

（一）睡眠的问题

   BIOS默认关闭了USB唤醒，睡眠后需按电源键唤醒
   需鼠标键盘唤醒的，在BIOS里设置USB唤醒为允许即可

    PS: 若睡眠有问题的可使用 Hackintool 工具，切换到电源选项，点击下面的螺丝刀图标修复

（二）Mac序列号的问题

    下载 OpenCore Configurator for Mac，打开 PlatformInfo -> Model Lookup | Check Coverage 右侧选择 iMac20,1 机型（生成你的唯一硬件UUID），然后 Save as (另存为) config.plist
    在config.plist文件中找到如下代码，记录MLB、SystemSerialNumber和SystemUUID的值并记住它，更新EFI时，用你记录的值替换 /OC/config.plist 下对应的值即可

    PS: 还可使用 Hackintool 工具（系统 -> 序列号生成器）来获取三码

<key>PlatformInfo</key>

<dict>
        
    <key>Generic</key>
    
    <dict>
        <key>AdviseWindows</key>
        <false/>
        <key>MLB</key>
        <string>C02047501CDPHCDAD</string>
        <key>ProcessorType</key>
        <integer>4105</integer>
        <key>ROM</key>
        <data>ESIzRFVm</data>
        <key>SpoofVendor</key>
        <true/>
        <key>SystemMemoryStatus</key>
        <string>Auto</string>
        <key>SystemProductName</key>
        <string>iMac20,1</string>
        <key>SystemSerialNumber</key>
        <string>C02DQSZFPN5T</string>
        <key>SystemUUID</key>
        <string>C567A1A9-9233-4D4D-B021-E1F38B112F33</string>
    </dict>

（三）Win+Mac双系统解决Win系统时间时差问题

    在Windows终端下使用管理员权限运行 Reg add HKLM\SYSTEM\CurrentControlSet\Control\TimeZoneInformation /v RealTimeIsUniversal /t REG_DWORD /d 1

（四）设置默认启动项

    多系统在启动选择界面，先使用键盘移动到要启动的项，然后按Ctrl + Enter (回车键) 进入系统，下次重启后默认就选中该项了
