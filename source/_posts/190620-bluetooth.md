---
title: 小米平板1-ubuntu系统_bluetooth篇
date: 2019-07-20 09:56:00
categories: linux
tags:
keywords:
description: OTG使用CSR8510蓝牙适配器
---

## CSR8510蓝牙适配器：驱动模块编译/开机自动加载
### 配置好./config文件后：
``` bash
root@tegra-ubuntu:/usr/src/kernel# make modules
  LD [M]  crypto/md4.ko
  LD [M]  crypto/sha256_generic.ko
  LD [M]  crypto/tcrypt.ko
  LD [M]  crypto/twofish_common.ko
  LD [M]  crypto/twofish_generic.ko
  LD [M]  drivers/bluetooth/bcm203x.ko
  LD [M]  drivers/bluetooth/bfusb.ko
  LD [M]  drivers/bluetooth/bpa10x.ko
  LD [M]  drivers/bluetooth/broadcom/bt_protocol_driver/brcm_bt_drv.ko
  LD [M]  drivers/bluetooth/broadcom/v4l2_fm_driver/fm_drv.ko
  LD [M]  drivers/bluetooth/broadcom/line_discipline_driver/brcm_hci_ldisc.ko
  LD [M]  drivers/bluetooth/btusb.ko
  LD [M]  drivers/bluetooth/hci_uart.ko
  LD [M]  drivers/input/joystick/xpad.ko
  LD [M]  drivers/input/joydev.ko
  LD [M]  drivers/media/platform/soc_camera/soc_camera_platform.ko
  LD [M]  drivers/media/usb/gspca/gspca_main.ko
  LD [M]  drivers/media/platform/soc_camera/tegra_camera/tegra_camera.ko
  LD [M]  drivers/media/v4l2-core/videobuf2-dma-contig.ko
  LD [M]  drivers/net/ppp/bsd_comp.ko
  LD [M]  drivers/net/ppp/ppp_async.ko
  LD [M]  drivers/net/ppp/ppp_deflate.ko
  LD [M]  drivers/net/ppp/ppp_generic.ko
  LD [M]  drivers/net/ppp/ppp_mppe.ko
  LD [M]  drivers/net/ppp/ppp_synctty.ko
  LD [M]  drivers/net/ppp/pppolac.ko
  LD [M]  drivers/net/ppp/pppopns.ko
  LD [M]  drivers/net/ppp/pppox.ko
  LD [M]  drivers/net/usb/raw_ip_net.ko
  LD [M]  drivers/net/slip/slhc.ko
  LD [M]  drivers/usb/class/cdc-acm.ko
  LD [M]  drivers/usb/class/cdc-wdm.ko
  LD [M]  drivers/usb/gadget/g_ether.ko
  LD [M]  drivers/usb/gadget/g_mass_storage.ko
  LD [M]  drivers/usb/gadget/libcomposite.ko
  LD [M]  drivers/usb/serial/baseband_usb_chr.ko
  LD [M]  drivers/video/tegra/host/vi/nvhost-vi.ko
  LD [M]  fs/cifs/cifs.ko
  LD [M]  net/bluetooth/bluetooth.ko
  LD [M]  fs/configfs/configfs.ko
  LD [M]  net/bluetooth/bnep/bnep.ko
  LD [M]  net/bluetooth/hidp/hidp.ko
  LD [M]  net/bluetooth/rfcomm/rfcomm.ko
  LD [M]  net/rfkill/rfkill-gpio.ko
root@tegra-ubuntu:/usr/src/kernel# 

root@tegra-ubuntu:/usr/src/kernel# make modules_install
  INSTALL crypto/md4.ko
  INSTALL crypto/sha256_generic.ko
  INSTALL crypto/tcrypt.ko
  INSTALL crypto/twofish_common.ko
  INSTALL crypto/twofish_generic.ko
#  INSTALL drivers/bluetooth/bcm203x.ko
#  INSTALL drivers/bluetooth/bfusb.ko
#  INSTALL drivers/bluetooth/bpa10x.ko
#  INSTALL drivers/bluetooth/broadcom/bt_protocol_driver/brcm_bt_drv.ko
#  INSTALL drivers/bluetooth/broadcom/line_discipline_driver/brcm_hci_ldisc.ko
#  INSTALL drivers/bluetooth/broadcom/v4l2_fm_driver/fm_drv.ko
#  INSTALL drivers/bluetooth/btusb.ko
#  INSTALL drivers/bluetooth/hci_uart.ko
  INSTALL drivers/input/joydev.ko
  INSTALL drivers/input/joystick/xpad.ko
  INSTALL drivers/media/platform/soc_camera/soc_camera_platform.ko
  INSTALL drivers/media/platform/soc_camera/tegra_camera/tegra_camera.ko
  INSTALL drivers/media/usb/gspca/gspca_main.ko
  INSTALL drivers/media/v4l2-core/videobuf2-dma-contig.ko
  INSTALL drivers/net/ppp/bsd_comp.ko
  INSTALL drivers/net/ppp/ppp_async.ko
  INSTALL drivers/net/ppp/ppp_deflate.ko
  INSTALL drivers/net/ppp/ppp_generic.ko
  INSTALL drivers/net/ppp/ppp_mppe.ko
  INSTALL drivers/net/ppp/ppp_synctty.ko
  INSTALL drivers/net/ppp/pppolac.ko
  INSTALL drivers/net/ppp/pppopns.ko
  INSTALL drivers/net/ppp/pppox.ko
  INSTALL drivers/net/slip/slhc.ko
  INSTALL drivers/net/usb/raw_ip_net.ko
  INSTALL drivers/usb/class/cdc-acm.ko
  INSTALL drivers/usb/class/cdc-wdm.ko
  INSTALL drivers/usb/gadget/g_ether.ko
  INSTALL drivers/usb/gadget/g_mass_storage.ko
  INSTALL drivers/usb/gadget/libcomposite.ko
  INSTALL drivers/usb/serial/baseband_usb_chr.ko
  INSTALL drivers/video/tegra/host/vi/nvhost-vi.ko
  INSTALL fs/cifs/cifs.ko
  INSTALL fs/configfs/configfs.ko
#  INSTALL net/bluetooth/bluetooth.ko
#  INSTALL net/bluetooth/bnep/bnep.ko
#  INSTALL net/bluetooth/hidp/hidp.ko
#  INSTALL net/bluetooth/rfcomm/rfcomm.ko
#?  INSTALL net/rfkill/rfkill-gpio.ko
  DEPMOD  3.10.40-gc5d0751
#         ^^^^^^^^^^^^^^^^
--------------------------------------------
# rc.local脚本:
# 加载顺序自下而上：
insmod '/usr/src/kernel/net/bluetooth/bluetooth.ko'
insmod '/usr/src/kernel/net/rfkill/rfkill-gpio.ko'
insmod '/usr/src/kernel/net/bluetooth/rfcomm/rfcomm.ko'
insmod '/lib/modules/3.10.40-gc5d0751/kernel/drivers/bluetooth/btusb.ko' 
insmod '/usr/src/kernel/drivers/bluetooth/hci_uart.ko' 
insmod '/usr/src/kernel/drivers/bluetooth/bcm203x.ko'
insmod '/usr/src/kernel/drivers/bluetooth/bfusb.ko'
insmod '/usr/src/kernel/drivers/bluetooth/bpa10x.ko'
insmod '/usr/src/kernel/net/bluetooth/bnep/bnep.ko' 
insmod '/usr/src/kernel/net/bluetooth/hidp/hidp.ko'
————————————————————————————————————————————————————
[只要这几个就够了,不安装smoke3.10.107内核里的BCM蓝牙驱动
root@tegra-ubuntu:/home/ubuntu# lsmod
Module                  Size  Used by
hidp                   14086  0 
bnep                   11864  0 
bpa10x                  4858  0 
bfusb                   8138  0 
bcm203x                 3277  0 
hci_uart               26740  0 
btusb                  16048  0 
rfcomm                 46451  0 
rfkill_gpio             2300  0 
bluetooth             279879  11 bnep,hidp,bfusb,btusb,bpa10x,hci_uart,rfcomm,brcm_hci_ldisc,bcm203x

--------------------------------------------------

-------------------------------------------------------
[BCM4356]
http://b8807053.pixnet.net/blog/post/347831957-bluez%E7%9B%B8%E9%97%9C%E7%9A%84%E5%90%84%E7%A8%AEtools%E7%9A%84%E4%BD%BF%E7%94%A8
Bluez相關的各種tools的使用

1. 安裝套件

sudo apt-get update
#sudo apt-get install bluetooth bluez bluez-hcidump

 
其中 bluetooth 套件包含了底層的 hci (host controller interface) 和 sdp (service discovery protocol) 工具。而 bluez 則是官方藍牙軟體協定 (Official Linux Bluetooth protocol stack)，屬於較上層。bluez 的網頁如下: http://www.bluez.org/

------------------------------------------------------
root@tegra-ubuntu:/home/ubuntu# proxychains apt-get install bluetooth bluez bluez-hcidump
ProxyChains-3.1 (http://proxychains.sf.net)
Reading package lists... Done
Building dependency tree       
Reading state information... Done
bluez is already the newest version.
bluez set to manually installed.
The following NEW packages will be installed:
  bluetooth bluez-gstreamer bluez-hcidump
...
Selecting previously unselected package bluetooth.
(Reading database ... 134589 files and directories currently installed.)
Preparing to unpack .../bluetooth_4.101-0ubuntu13_all.deb ...
Unpacking bluetooth (4.101-0ubuntu13) ...
Selecting previously unselected package bluez-gstreamer.
Preparing to unpack .../bluez-gstreamer_4.101-0ubuntu13_armhf.deb ...
Unpacking bluez-gstreamer (4.101-0ubuntu13) ...
Selecting previously unselected package bluez-hcidump.
Preparing to unpack .../bluez-hcidump_2.5-1_armhf.deb ...
Unpacking bluez-hcidump (2.5-1) ...
Processing triggers for man-db (2.6.7.1-1ubuntu1) ...
Setting up bluetooth (4.101-0ubuntu13) ...
Setting up bluez-gstreamer (4.101-0ubuntu13) ...
Setting up bluez-hcidump (2.5-1) ...
root@tegra-ubuntu:/home/ubuntu#
---------------------------------------------------
#不要安装
root@tegra-ubuntu:/home/ubuntu#  apt-get install bluez-utils [无效!!!],会使hciconfig无效,重启回复正常
**************************************************************
开机插上CSR8510模块等一会gnome 蓝牙设置窗口自动识别
配对B.O.W需要按住Fn+Delete初始化了再配对

------------------测试------------------------------------
--------------------------------------------------------------
root@tegra-ubuntu:/etc# dmesg | grep -i blue
[   23.330606] init: bluetooth main process (1080) terminated with status 1
[   23.330650] init: bluetooth main process ended, respawning
[   24.463328] Bluetooth: Core ver 2.16
[   24.463410] Bluetooth: HCI device and connection manager initialized
[   24.463447] Bluetooth: HCI socket layer initialized
[   24.463466] Bluetooth: L2CAP socket layer initialized
[   24.463498] Bluetooth: SCO socket layer initialized
[   24.490456] Bluetooth: RFCOMM TTY layer initialized
[   24.490497] Bluetooth: RFCOMM socket layer initialized
[   24.490506] Bluetooth: RFCOMM ver 1.11
[   24.529249] Bluetooth: HCI UART driver ver 2.2
[   24.529261] Bluetooth: HCI H4 protocol initialized
[   24.529268] Bluetooth: HCI BCSP protocol initialized
[   24.529275] Bluetooth: HCILL protocol initialized
[   24.529281] Bluetooth: HCIATH3K protocol initialized
[   24.529287] Bluetooth: HCI Three-wire UART (H5) protocol initialized
[   24.566516] Bluetooth: BNEP (Ethernet Emulation) ver 1.3
[   24.566533] Bluetooth: BNEP filters: protocol multicast
[   24.566570] Bluetooth: BNEP socket layer initialized
[   24.578784] Bluetooth: HIDP (Human Interface Emulation) ver 1.2
[   24.578827] Bluetooth: HIDP socket layer initialized
[   56.791738] input: B.O.W as /devices/platform/tegra-ehci.0/usb2/2-1/2-1:1.0/bluetooth/hci0/hci0:70/input2
[   56.792059] hid-generic 0005:05AC:023C.0001: input: BLUETOOTH HID v0.01 Keyboard [B.O.W] on 00:1a:7d:da:71:11
-------------------------------------------------------------
```
