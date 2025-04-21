# SUSFS 更新系统

## 项目简介
SUSFS 更新系统是一个高效、稳定的设备固件更新解决方案，适用于设备管理和固件升级。本项目包含 SUSFS 更新系统的核心代码、配置文件详细的刷回官方固件教程，确保设备恢复到官方状态。

## 特性
- **高效更新**：支持全量包刷写，快速恢复官方固件。
- **安全可靠**：内置校验机制，确保刷机过程稳定。
- **简单操作**：提供清晰的刷机和格式化步骤，适合开发者与用户。

## 刷回官方固件教程

### 前置要求
- 设备处于开机状态并已启用 USB 调试。
- 安装好 ADB 和 Fastboot 工具（参考 [Android SDK Platform Tools](https://developer.android.com/studio/releases/platform-tools)）。
- 下载最新的 SUSFS 全量更新包（可在 [Releases](https://github.com/your-username/your-repo/releases) 页面找到）。
- 确保设备电量充足（建议 >50%）并连接到电脑。

### 刷机步骤
1. **进入 fastbootd 模式**：
   - 连接设备到电脑，打开终端（Windows CMD、PowerShell 或 Linux/macOS 终端）。
   - 输入以下命令进入 fastbootd 模式：
     ```bash
     adb reboot fastboot
     ```
   - 设备将重启并进入 fastbootd 模式。

2. **擦除分区**：
   - 在终端输入以下命令，擦除用户数据和缓存分区：
     ```bash
     fastboot -w
     ```
   - **注意**：此操作会清除设备所有数据，请提前备份！

3. **线刷全量包**：
   - 在终端中，导航到全量包所在目录，或指定全量包路径。
   - 执行以下命令刷写全量包：
     ```bash
     fastboot flash <partition> <filename>.zip
     ```
     （替换 `<partition>` 为目标分区，如 `system`、`boot` 等，`<filename>.zip` 为全量包文件名，具体分区信息请参考全量包附带的说明文档）。
   - 等待刷写完成，终端会显示成功信息。

4. **格式化分区**：
   - 刷写完成后，执行格式化分区操作以确保系统干净：
     ```bash
     fastboot format <partition>
     ```
     （替换 `<partition>` 为需要格式化的分区，如 `userdata` 或 `cache`，具体分区参考全量包文档）。
   - 格式化完成后，输入以下命令重启设备：
     ```bash
     fastboot reboot
     ```

5. **验证与开机**：
   - 设备将自动重启并进入官方固件系统。
   - 按照屏幕提示完成初始设置（如语言、网络等）。
   - 检查系统状态，确保 SUSFS 更新系统或官方固件正常运行。

### 注意事项
- **全量包要求**：必须使用官方提供的全量包，刷写前确认包的完整性（可通过 MD5/SHA256 校验）。
- **格式化必要性**：刷机后格式化分区是必需步骤，跳过可能导致系统不稳定或无法开机。
- **数据备份**：执行 `fastboot -w` 和格式化会清除所有数据，请提前备份重要文件。
- **命令准确性**：确保输入正确的分区名称和文件名，错误操作可能导致设备变砖。

## 贡献
欢迎为 SUSFS 更新系统贡献代码或优化教程！请遵循以下步骤：
1. Fork 本仓库。
2. 创建你的功能分支（`git checkout -b feature/AmazingFeature`）。
3. 提交更改（`git commit -m 'Add some AmazingFeature'`）。
4. 推送到分支（`git push origin feature/AmazingFeature`）。
5. 提交 Pull Request。

## 许可证
本项目采用 [MIT 许可证](LICENSE)，详情请查看 LICENSE 文件。

## 联系方式
- 项目维护者：[Kevin-Y-Du](https://github.com/Kevin-Y-Du)
- 问题反馈：请在 [Issues](https://github.com/your-username/your-repo/issues) 页面提交问题。

感谢使用 SUSFS 更新系统！🚀
