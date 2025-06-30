# Raspberry-Pi-BootSeq-Generator

# Raspberry Pi `config.txt` Reference

## 📘 General Information
- `config.txt` controls hardware and boot settings.
- Located in the boot partition (`/boot`).
- Syntax: one directive per line.

---

## 🎯 Common Directives and Their Purpose

| Purpose | Directive | Explanation |
|---------|-----------|-------------|
| Enable I2C | `dtparam=i2c_arm=on` | Turns I2C bus on/off. |
| Enable SPI | `dtparam=spi=on` | Enables SPI hardware. |
| Enable I2S Audio | `dtparam=i2s=on` | Enables I2S sound output. |
| Enable analog audio | `dtparam=audio=on` | 3.5mm audio output. |
| Auto-detect camera | `camera_auto_detect=1` | CSI camera detection. |
| Auto-detect display | `display_auto_detect=1` | DSI display detection. |
| Enable KMS driver | `dtoverlay=vc4-kms-v3d` | Full KMS video driver. |
| Disable overscan | `disable_overscan=1` | Removes black border on screen. |
| Force HDMI hotplug | `hdmi_force_hotplug=1` | HDMI always active. |
| Enable 4K@60Hz | `hdmi_enable_4kp60=1` | 4K output (Pi4/Pi5/CM5). |
| Use 64-bit kernel | `arm_64bit=1` | 64-bit kernel mode. |
| CPU performance boost | `arm_boost=1` | Higher CPU frequencies. |
| GPU memory allocation | `gpu_mem=128` | Memory (in MB) reserved for GPU. |
| Always overclock | `force_turbo=1` | CPU always runs at turbo frequencies. |
| Overvoltage offset | `over_voltage=2` | Increase core voltage. |
| Thermal limit | `temp_limit=85` | Throttling threshold in °C. |
| Initial GPIO state | `gpio=12=op,dh` | Sets GPIO pin modes and state. |
| PCIe enable | `dtoverlay=pciex1` | Enable PCIe interface. |
| PCIe Gen3 mode | `dtparam=pciex1_gen=3` | Use PCIe Gen3 speeds. |
| Include additional config | `include other.txt` | Load extra config file. |

---

## 🧩 Model Compatibility Matrix (`config.txt`)

| Purpose | Directive | CM5 | Pi5 | Pi4/400/CM4 | Pi3/3B+/CM3 | Pi2 | Pi1/Zero |
|---------|-----------|:---:|:---:|:-----------:|:-----------:|:---:|:--------:|
| Enable I2C | `dtparam=i2c_arm=on` | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ |
| Enable SPI | `dtparam=spi=on` | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ |
| Enable I2S Audio | `dtparam=i2s=on` | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ |
| Enable analog audio | `dtparam=audio=on` | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ |
| Auto-detect camera | `camera_auto_detect=1` | ✔ | ✔ | ✔ | ✘ | ✘ | ✘ |
| Auto-detect display | `display_auto_detect=1` | ✔ | ✔ | ✔ | ✘ | ✘ | ✘ |
| Enable KMS driver | `dtoverlay=vc4-kms-v3d` | ✔ | ✔ | ✔ | ✘ | ✘ | ✘ |
| Disable overscan | `disable_overscan=1` | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ |
| Force HDMI hotplug | `hdmi_force_hotplug=1` | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ |
| Enable 4K@60Hz | `hdmi_enable_4kp60=1` | ✔ | ✔ | ✔ | ✘ | ✘ | ✘ |
| Use 64-bit kernel | `arm_64bit=1` | ✔ | ✔ | ✔ | ✔ | ✘ | ✘ |
| CPU performance boost | `arm_boost=1` | ✔ | ✔ | ✔ | ✘ | ✘ | ✘ |
| GPU memory allocation | `gpu_mem=128` | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ |
| Always overclock | `force_turbo=1` | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ |
| Overvoltage offset | `over_voltage=2` | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ |
| Thermal limit | `temp_limit=85` | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ |
| Initial GPIO state | `gpio=12=op,dh` | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ |
| PCIe enable | `dtoverlay=pciex1` | ✔ | ✔ | ✘ | ✘ | ✘ | ✘ |
| PCIe Gen3 mode | `dtparam=pciex1_gen=3` | ✔ | ✔ | ✘ | ✘ | ✘ | ✘ |

---

# Raspberry Pi `cmdline.txt` Reference

## 📘 General Information
- `cmdline.txt` holds **kernel boot parameters**.
- Must be **a single line**, space-separated.
- Controls filesystem, console, and kernel behavior.

---

## 🎯 Common Parameters and Their Purpose

| Purpose | Parameter | Explanation |
|---------|-----------|-------------|
| Root filesystem path | `root=/dev/mmcblk0p2` or `root=PARTUUID=xxxx` | Defines root partition. |
| Filesystem type | `rootfstype=ext4` | Filesystem format. |
| Wait for root device | `rootwait` | Ensures the device is ready. |
| Serial console output | `console=serial0,115200` | UART output. |
| HDMI console output | `console=tty1` | Display output. |
| Read-only root | `ro` | Mount root read-only. |
| Kernel log level | `loglevel=3` | Verbosity of boot messages. |
| Enable cgroups | `cgroup_enable=cpuset cgroup_enable=memory cgroup_memory=1` | For container workloads. |
| Swap behavior | `vm.swappiness=10` | Swapping aggressiveness. |
| USB gadget mode | `modules-load=dwc2,g_ether` | USB device emulation. |
| Disable fsck repair | `fsck.repair=no` | Prevents auto-repair. |
| Quiet boot | `quiet splash plymouth.ignore-serial-consoles` | Hides boot messages. |
| I/O scheduler | `elevator=deadline` | Disk scheduler. |
| Video mode | `video=HDMI-A-1:1920x1080@60` | Framebuffer resolution. |

---

## 🧩 Model Compatibility Matrix (`cmdline.txt`)

| Purpose | Parameter | CM5 | Pi5 | Pi4/400/CM4 | Pi3/3B+/CM3 | Pi2 | Pi1/Zero |
|---------|-----------|:---:|:---:|:-----------:|:-----------:|:---:|:--------:|
| Root filesystem path | `root=...` | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ |
| Filesystem type | `rootfstype=ext4` | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ |
| Wait for root | `rootwait` | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ |
| Serial console | `console=serial0,115200` | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ |
| HDMI console | `console=tty1` | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ |
| Read-only root | `ro` | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ |
| Kernel log level | `loglevel=3` | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ |
| Enable cgroups | `cgroup_enable=...` | ✔ | ✔ | ✔ | ✔ | ✘ | ✘ |
| Swap behavior | `vm.swappiness=10` | ✔ | ✔ | ✔ | ✔ | ✘ | ✘ |
| USB gadget mode | `modules-load=dwc2,g_ether` | ✔ | ✔ | ✔ | ✘ | ✘ | ✘ |
| Disable fsck repair | `fsck.repair=no` | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ |
| Quiet boot | `quiet splash ...` | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ |
| I/O scheduler | `elevator=deadline` | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ |
| Video mode | `video=...` | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ |

---

## 📚 References
- [Raspberry Pi Documentation](https://www.raspberrypi.com/documentation/)
- [Kernel Parameters](https://docs.kernel.org/admin-guide/kernel-parameters.html)
- [Raspberry Pi Forums](https://forums.raspberrypi.com/)

---

