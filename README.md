# Dell Latitude 5300 — macOS Tahoe 26.6.1 EFI

[中文](#中文说明) · [English](#english)

> Community project for educational and testing purposes. This public package deliberately excludes private SMBIOS values and proprietary Apple binaries.

## 中文说明

### 项目状态

这套配置已在 Dell Latitude 5300 上完成实机测试：使用 `MacBookPro16,2` SMBIOS 后，可以启动并完成 macOS Tahoe 26.6.1（Build 25G76）安装。用户确认安装完成后所有已测试硬件均正常。

此前使用 `MacBookPro15,4` 时，即使加入 `-no_compat_check` 和 Board-ID 跳过补丁，Tahoe 图形安装器仍提示“不兼容”。改用完整一致的 `MacBookPro16,2` 身份后问题解决。

### 测试硬件

- Dell Latitude 5300
- Intel Core i7-8665U
- Intel UHD 620
- Intel I219-LM / IntelMausi
- Broadcom BCM94360NG Wi-Fi 与蓝牙
- Dell I2C HID 触控板
- Realtek ALC295
- 机器专用 USB 映射

### 使用方法

1. 不要直接使用模板内的 `CHANGEME` 身份。
2. 使用 OpenCore `macserial` 或 GenSMBIOS 为 `MacBookPro16,2` 生成你自己的 SystemSerialNumber 与 MLB。
3. 生成新的 SystemUUID，并设置你自己的 6 字节 ROM。
4. 将这些值写入 `PlatformInfo -> Generic`。
5. 根据文档恢复所需的开源 kext；Broadcom/OCLP 工作流需要的 Apple 专有组件必须由用户从合法来源自行取得，本仓库不提供。
6. 先从 FAT32 USB EFI 分区测试，执行一次 Reset NVRAM，再从同一 U 盘重新启动。
7. 安装到独立 APFS 测试卷，确认启动、显卡、触控板、USB、有线网络、Wi-Fi、蓝牙、音频和睡眠后，再考虑内部 EFI。

### 关键设置

- `SystemProductName = MacBookPro16,2`
- `SecureBootModel = Disabled`
- `Skip Board ID check = Disabled`
- 不使用 `-no_compat_check`
- 保留 `ipc_control_port_options=0`

### 安全提醒

- 始终保留可启动的救援 U 盘和原 EFI 备份。
- 不要复制他人的 Serial、MLB、UUID 或 ROM。
- 不要将本模板直接覆盖到正在工作的内部 EFI。
- macOS 更新或 root patch 可能改变兼容性，应先在 USB 和独立卷测试。

## English

### Project status

This configuration was tested on a Dell Latitude 5300. With a complete `MacBookPro16,2` SMBIOS, it boots the macOS Tahoe 26.6.1 (25G76) installer and completes installation. The user reported that all tested hardware worked normally afterward.

With `MacBookPro15,4`, the graphical installer continued to report an incompatible Mac even when `-no_compat_check` and a Board-ID bypass were present. A complete and internally consistent `MacBookPro16,2` identity resolved the installer gate.

### Tested hardware

- Dell Latitude 5300
- Intel Core i7-8665U
- Intel UHD 620
- Intel I219-LM with IntelMausi
- Broadcom BCM94360NG Wi-Fi and Bluetooth
- Dell I2C HID trackpad
- Realtek ALC295
- Machine-specific USB map

### Usage

1. Do not use the `CHANGEME` identity values in the template.
2. Use OpenCore `macserial` or GenSMBIOS to generate your own SystemSerialNumber and MLB for `MacBookPro16,2`.
3. Generate a fresh SystemUUID and choose your own six-byte ROM value.
4. Insert the four values under `PlatformInfo -> Generic`.
5. Restore the required open-source kexts according to the documentation. Apple-proprietary components needed by Broadcom/OCLP workflows must be obtained by the user from a lawful source and are not distributed here.
6. Test from a FAT32 USB EFI partition first. Reset NVRAM once, then boot again through the same USB.
7. Install to a separate APFS test volume. Verify boot, graphics, trackpad, USB, Ethernet, Wi-Fi, Bluetooth, audio and sleep before considering internal-EFI deployment.

### Key settings

- `SystemProductName = MacBookPro16,2`
- `SecureBootModel = Disabled`
- `Skip Board ID check = Disabled`
- No `-no_compat_check`
- `ipc_control_port_options=0` retained

### Safety

- Always keep a bootable rescue USB and the original EFI backup.
- Never copy another person's Serial, MLB, UUID or ROM.
- Never overwrite a working internal EFI directly with this template.
- macOS updates and root patches may change compatibility; test them from USB and on an isolated volume first.

## Validation

- Active private build: OpenCore 1.0.7 schema validation passed with zero errors.
- Public template: SMBIOS identity intentionally invalidated and must be regenerated before use.
- Real-machine result: installation completed; all user-tested functions reported normal.

## License and attribution

OpenCore and third-party kexts remain under their respective upstream licenses. macOS and Apple components are property of Apple Inc. This repository is not affiliated with Apple, Dell, Acidanthera or Dortania.
