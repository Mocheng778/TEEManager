# TEEManager 更新日志

## v1.2.0-TEEManager (2026-08-25)

### 新增
- 模块在线更新支持（updateJson）
- yosteebl 双阶段属性修正（post-fs-data + service）
- 小米/红米特有属性隐藏（warranty_bit、secureboot、oem_unlock）
- WebUI 精美界面重构（玻璃拟态 + 渐变光效 + SVG 图标）

### 优化
- BL 状态隐藏时机提前至系统服务启动前，解决小米设备属性缓存问题
- 一键更新3绿密钥按钮加载状态动画
- 模块信息卡片布局优化

### 修复
- yosteebl 属性修正执行过晚导致 BL 状态仍显示已解锁的问题
- WebUI JS 模板字符串转义导致按钮无响应的问题

### 模块信息
- **模块 ID**: TEEManager
- **版本**: 1.2.0-TEEManager
- **版本号**: 216
- **作者**: 莫晨
- **架构**: arm64-v8a
- **支持系统**: Android 9-17

### 支持 Root 管理器
- Magisk
- Magisk Alpha
- KernelSU
- KernelSU Next
- SukiSU-Ultra
- ApkeSU

### 支持机型
- 一加 / 真我 / OPPO
- vivo / IQOO
- 小米 / 红米 / 红魔
- 联想 / 魅族

### 功能说明
- 自定义密钥伪装安卓密钥状态
- 修正解锁 BL 后的异常系统属性
- 深度隐藏 Root 痕迹
- WebUI 一键更新3绿密钥
- yosteebl 子模块双阶段 BL 属性修正

### 注意事项
- 公开 keybox 根证书可能已过期或被吊销，如需通过密钥认证请使用有效私有 keybox
- 首次安装后请重启设备生效
- 如 BL 状态仍被检测到，请确认 yosteebl 子模块已启用