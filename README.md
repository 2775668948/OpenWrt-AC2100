# Actions-OpenWrt-AC2100(R2100)

[![LICENSE](https://img.shields.io/github/license/loneshore/OpenWrt-AC2100?label=LICENSE&style=flat-square)](https://github.com/loneshore/OpenWrt-AC2100/blob/main/LICENSE)
![GitHub Stars](https://img.shields.io/github/stars/loneshore/OpenWrt-AC2100?label=Stars&logo=github&style=flat-square)
![GitHub Forks](https://img.shields.io/github/forks/loneshore/OpenWrt-AC2100?label=Forks&logo=github&style=flat-square)
![GitHub release (latest by date)](https://img.shields.io/github/v/release/loneshore/OpenWrt-AC2100?label=Release&logo=github&style=flat-square)

小米路由器AC2100 OpenWrt固件自动化构建

## 说明

- 感谢 [P3TERX](https://github.com/P3TERX/Actions-OpenWrt) 的自动化构建项目
- 基于 [Lean's OpenWrt](https://github.com/coolsnowwolf/lede) 项目进行构建
- 默认登录IP [192.168.1.1](http://192.168.1.1) 密码 password
- 集成 OpenWrt Argon 主题和 Argon主题配置插件
- 集成 EQoS、PassWall、UnblockNeteaseMusic 等常用插件

## 安装

- 开启路由器SSH支持
- 漏洞固件：[2.0.722](https://cdn.cnbj1.fds.api.mi-img.com/xiaoqiang/rom/r2100/miwifi_r2100_firmware_4b519_2.0.722.bin)、[2.0.743](https://cdn.cnbj1.fds.api.mi-img.com/xiaoqiang/rom/r2100/miwifi_r2100_all_7d7b2_2.0.743.bin)（其实无需降级，最新固件也是支持的）
- 在浏览器访问以下链接即可开启SSH支持（STOK请登录路由器后台获取替换）
```
http://miwifi.com/cgi-bin/luci/;stok=<STOK>/api/misystem/set_config_iotdev?bssid=Xiaomi&user_id=admin&ssid=-h%3B%20nvram%20set%20ssh_en%3D1%3B%20nvram%20commit%3B%20sed%20-i%20's%2Fchannel%3D.*%2Fchannel%3D%5C%22debug%5C%22%2Fg'%20%2Fetc%2Finit.d%2Fdropbear%3B%20%2Fetc%2Finit.d%2Fdropbear%20start%3B%20echo%20-e%20'admin%5Cnadmin'%20%7C%20passwd%20root%3B
```
- 登录SSH，将固件上传到 /tmp 目录，依次执行以下代码（固件名称自行替换）
```
nvram set uart_en=1&&nvram set bootdelay=5&&nvram set flag_try_sys1_failed=1&&nvram commit
　
mtd write /tmp/xxx-kernel1.bin kernel1
mtd -r write /tmp/xxx-rootfs0.bin rootfs0
　
reboot
```

## 注意

- 刷机有风险，操作需谨慎
