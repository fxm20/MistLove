| adb devices                                 | 查看连接的设备列表                 |
| ------------------------------------------- | ---------------------------------- |
| `adb shell`                                 | 进入 Android 设备的命令行模式      |
| `adb install <apk路径>`                     | 安装应用程序                       |
| `adb uninstall <包名>`                      | 卸载应用程序                       |
| `adb push <本地路径> <设备路径>`            | 将文件从本地传输到设备             |
| `adb pull <设备路径> <本地路径>`            | 将文件从设备传输到本地             |
| `adb reboot`                                | 重启设备                           |
| `adb reboot bootloader`                     | 重启设备进入 bootloader 模式       |
| `adb reboot recovery`                       | 重启设备进入恢复模式               |
| `adb logcat`                                | 显示系统日志                       |
| `adb logcat -d > <文件名>`                  | 保存日志到文件                     |
| `adb shell pm list packages`                | 查看已安装的应用包名列表           |
| `adb shell pm path <包名>`                  | 获取指定应用的 APK 路径            |
| `adb shell am start -n <组件名>`            | 启动指定的 Activity                |
| `adb shell am force-stop <包名>`            | 强制停止应用                       |
| `adb shell input tap <x> <y>`               | 模拟点击操作                       |
| `adb shell input swipe <x1> <y1> <x2> <y2>` | 模拟滑动操作                       |
| `adb shell screencap -p /sdcard/screen.png` | 截取屏幕截图                       |
| `adb pull /sdcard/screen.png`               | 将截图传输到本地                   |
| `adb shell screenrecord /sdcard/video.mp4`  | 录制屏幕                           |
| `adb forward <本地端口> <远程端口>`         | 设置端口转发                       |
| `adb shell dumpsys`                         | 获取系统服务的状态信息             |
| `adb shell getprop`                         | 查看设备的属性信息                 |
| `adb shell setprop <属性> <值>`             | 设置设备的属性信息                 |
| `adb bugreport > <文件名>`                  | 导出设备的 bugreport               |
| `adb root`                                  | 以 root 权限运行 adb               |
| `adb remount`                               | 重新挂载系统分区（需要 root 权限） |
| `adb sideload <文件名>`                     | 以 sideload 方式安装更新包         |