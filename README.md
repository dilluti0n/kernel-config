[Gentoo Linux
Kernel](https://packages.gentoo.org/packages/sys-kernel/gentoo-sources)
configuration for my laptop(21MCCTO1WW ThinkPad T14 Gen 5)

- [config](./config) used to be follow stable (amd64) gentoo-sources,
  not maintained now.
- [config-nostable](./config-nostable) following unstable (~amd64)
  gentoo-sources.

It is minimal and fast-booting, built upon `make defconfig`. However,
I cannot guarantee that there are no unnecessary configs for this
hardware.

## Feature
- [dm_crypt](https://www.kernel.org/doc/html/latest/admin-guide/device-mapper/dm-crypt.html) works
- [tpm](https://www.kernel.org/doc/html/latest/security/tpm/index.html) works
- [btrfs](https://en.wikipedia.org/wiki/Btrfs)/[ext4](https://en.wikipedia.org/wiki/Ext4)/[nfs](https://en.wikipedia.org/wiki/Network_File_System) works
- [zram](https://docs.kernel.org/admin-guide/blockdev/zram.html) enabled
- Every PCI/I2C devices for this hardware works fine
- Every LEDs (power, keyboard, webcam ...) works fine
- Bluetooth/USB HID works fine
- [docker](https://www.docker.com/) and [overlayfs](https://en.wikipedia.org/wiki/OverlayFS) works fine
- [wireguard](https://www.wireguard.com/) works
- [nftables](https://nftables.org/)/[wireshark](https://www.wireshark.org/)
  works fine but most of xt_* filters are not enabled
- [KVM](https://linux-kvm.org/page/Main_Page) works but some features
  on [libvirt](https://libvirt.org/) might not work

I don’t know if anyone else will use this setup, but if any of these
doesn’t work on the same hardware, I’d appreciate it if you could let
me know in the Issues tab.

## Simple tutorial
``` bash
cp config-nostable /usr/src/linux/.config
cd /usr/src/linux
make -j$(nprocs)
```

This will prompt newconfigs if .config is older than source. You can
press ENTER without selecting one for each prompts if you want to use
default one. You should not use newer .config to older source.

If you want to use default one for all configs when updating, `make
olddefconfig` before build the source.


```
make modules_install
make install
```

For more information, see <https://wiki.gentoo.org/wiki/Kernel/Upgrade>.

## Links

- <https://wiki.gentoo.org/wiki/Kernel/Upgrade>
- <https://wiki.gentoo.org/wiki/Kernel/Gentoo_Kernel_Configuration_Guide>
- <https://www.kernel.org/doc/html/latest/kbuild/kconfig-language.html>
- <https://www.kernelconfig.io/index.html>

## Hardware
Result of `lspci`:
```
00:00.0 Host bridge: Advanced Micro Devices, Inc. [AMD] Phoenix Root Complex
00:00.2 IOMMU: Advanced Micro Devices, Inc. [AMD] Phoenix IOMMU
00:01.0 Host bridge: Advanced Micro Devices, Inc. [AMD] Phoenix Dummy Host Bridge
00:02.0 Host bridge: Advanced Micro Devices, Inc. [AMD] Phoenix Dummy Host Bridge
00:02.1 PCI bridge: Advanced Micro Devices, Inc. [AMD] Phoenix GPP Bridge
00:02.2 PCI bridge: Advanced Micro Devices, Inc. [AMD] Phoenix GPP Bridge
00:02.4 PCI bridge: Advanced Micro Devices, Inc. [AMD] Phoenix GPP Bridge
00:03.0 Host bridge: Advanced Micro Devices, Inc. [AMD] Phoenix Dummy Host Bridge
00:03.1 PCI bridge: Advanced Micro Devices, Inc. [AMD] Family 19h USB4/Thunderbolt PCIe tunnel
00:04.0 Host bridge: Advanced Micro Devices, Inc. [AMD] Phoenix Dummy Host Bridge
00:04.1 PCI bridge: Advanced Micro Devices, Inc. [AMD] Family 19h USB4/Thunderbolt PCIe tunnel
00:08.0 Host bridge: Advanced Micro Devices, Inc. [AMD] Phoenix Dummy Host Bridge
00:08.1 PCI bridge: Advanced Micro Devices, Inc. [AMD] Phoenix Internal GPP Bridge to Bus [C:A]
00:08.2 PCI bridge: Advanced Micro Devices, Inc. [AMD] Phoenix Internal GPP Bridge to Bus [C:A]
00:08.3 PCI bridge: Advanced Micro Devices, Inc. [AMD] Phoenix Internal GPP Bridge to Bus [C:A]
00:14.0 SMBus: Advanced Micro Devices, Inc. [AMD] FCH SMBus Controller (rev 71)
00:14.3 ISA bridge: Advanced Micro Devices, Inc. [AMD] FCH LPC Bridge (rev 51)
00:18.0 Host bridge: Advanced Micro Devices, Inc. [AMD] Phoenix Data Fabric; Function 0
00:18.1 Host bridge: Advanced Micro Devices, Inc. [AMD] Phoenix Data Fabric; Function 1
00:18.2 Host bridge: Advanced Micro Devices, Inc. [AMD] Phoenix Data Fabric; Function 2
00:18.3 Host bridge: Advanced Micro Devices, Inc. [AMD] Phoenix Data Fabric; Function 3
00:18.4 Host bridge: Advanced Micro Devices, Inc. [AMD] Phoenix Data Fabric; Function 4
00:18.5 Host bridge: Advanced Micro Devices, Inc. [AMD] Phoenix Data Fabric; Function 5
00:18.6 Host bridge: Advanced Micro Devices, Inc. [AMD] Phoenix Data Fabric; Function 6
00:18.7 Host bridge: Advanced Micro Devices, Inc. [AMD] Phoenix Data Fabric; Function 7
01:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8111/8168/8211/8411 PCI Express Gigabit Ethernet Controller (rev 0e)
02:00.0 Network controller: Qualcomm Technologies, Inc QCNFA765 Wireless Network Adapter (rev 01)
03:00.0 Non-Volatile memory controller: Sandisk Corp WD SN560/SN740/SN770/SN5000 NVMe SSD (rev 01)
c4:00.0 VGA compatible controller: Advanced Micro Devices, Inc. [AMD/ATI] HawkPoint1 (rev d0)
c4:00.1 Audio device: Advanced Micro Devices, Inc. [AMD/ATI] Radeon High Definition Audio Controller [Rembrandt/Strix]
c4:00.2 Encryption controller: Advanced Micro Devices, Inc. [AMD] Phoenix CCP/PSP 3.0 Device
c4:00.3 USB controller: Advanced Micro Devices, Inc. [AMD] Device 15b9
c4:00.4 USB controller: Advanced Micro Devices, Inc. [AMD] Device 15ba
c4:00.5 Multimedia controller: Advanced Micro Devices, Inc. [AMD] Audio Coprocessor (rev 63)
c4:00.6 Audio device: Advanced Micro Devices, Inc. [AMD] Family 17h/19h/1ah HD Audio Controller
c5:00.0 Non-Essential Instrumentation [1300]: Advanced Micro Devices, Inc. [AMD] Phoenix Dummy Function
c5:00.1 Signal processing controller: Advanced Micro Devices, Inc. [AMD] AMD IPU Device
c6:00.0 Non-Essential Instrumentation [1300]: Advanced Micro Devices, Inc. [AMD] Phoenix Dummy Function
c6:00.3 USB controller: Advanced Micro Devices, Inc. [AMD] Device 15c0
c6:00.4 USB controller: Advanced Micro Devices, Inc. [AMD] Device 15c1
c6:00.5 USB controller: Advanced Micro Devices, Inc. [AMD] Pink Sardine USB4/Thunderbolt NHI controller #1
c6:00.6 USB controller: Advanced Micro Devices, Inc. [AMD] Pink Sardine USB4/Thunderbolt NHI controller #2
```
