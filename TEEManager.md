- 首次安装后请重启设备生效
- 如 BL 状态仍被检测到，请确认 yosteebl 子模块已启用# TEEManager 更新日志

## v1.2.4-TEEManager (2026-08-26)

### 新增
- 模块在线更新支持（updateJson 指向 GitHub 仓库 TEEManager.json）
- 新增 TEEManager.json 在线更新配置文件
- yosteebl 双阶段属性修正（post-fs-data 早期修正 + service 兜底修正）
- TEEManager 自身 post-fs-data 阶段增加早期属性修正（三重保险）
- 小米/红米/三星特有属性隐藏（warranty_bit、secureboot、oem_unlock、frp.state）
- WebUI 精美界面重构（玻璃拟态 + 渐变光效 + SVG 盾牌钥匙图标 + 浮动光斑）
- 一键更新3绿密钥按钮加载状态 spinner 动画
- script3.sh 下载失败 3 次自动重试机制
- action.sh 生成配置后自动触发 injector 重启

### 优化
- BL 状态隐藏时机提前至系统服务启动前，解决小米设备属性缓存导致 BL 仍显示已解锁的问题
- 一键更新3绿密钥改为从 GitHub 仓库（Mocheng778/TEEManager）下载，下载后自动部署到生效路径并触发守护进程重启
- 动态 keystore UID 检测（优先 id 查询，备选目录所有者推断，fallback 1017），解决部分机型权限不正确导致模块不生效的问题
- 新增 restorecon 自动修复 SELinux 上下文，提升全机型兼容性
- injector.toml 默认拦截列表从 5 个扩展至 70+ 个应用，覆盖密钥认证工具、Root 检测工具、Google Play Integrity、银行支付、游戏反作弊、厂商安全中心
- action.sh 基础拦截列表同步扩展，执行后自动拦截全部第三方应用
- 支持机型列表扩展（新增三星 / 索尼 / 华硕 / 摩托罗拉）
- 安装时自动检测并显示设备品牌 / 型号 / 设备名
- 模块信息卡片布局优化，新增 stable 版本标签

### 修复
- yosteebl 属性修正执行过晚（wait_for_boot 等待开机完成）导致 keystore/keymint 已缓存旧属性，BL 状态仍显示已解锁的问题
- WebUI JS 模板字符串转义导致按钮无响应、界面卡住的问题
- 远程更新的 keybox 仅保存到备份路径、未部署到生效路径的问题
- keystore 目录所有者硬编码为 1017 导致部分机型权限不正确的问题

### 模块信息
- **模块 ID**: TEEManager
- **名称**: TEEManager
- **版本**: 1.2.2-TEEManager
- **版本号**: 222
- **作者**: 莫晨
- **架构**: arm64-v8a
- **支持系统**: Android 9-17
- **仓库**: https://github.com/Mocheng778/TEEManager

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
- 三星 / 索尼 / 华硕 / 摩托罗拉

### 功能说明
- 自定义密钥伪装安卓密钥状态
- 修正解锁 BL 后的异常系统属性（双阶段早期修正）
- 深度隐藏 Root 痕迹
- WebUI 一键更新3绿密钥（从 GitHub 仓库下载）
- yosteebl 子模块双阶段 BL 属性修正
- 自动拦截全部第三方应用的密钥操作
- 动态 keystore UID 检测 + SELinux 自动修复

### 升级注意事项
- 升级前请先卸载旧的 yosteebl 子模块，安装时会自动创建新的双阶段版本
- 升级后请重启设备使所有变更生效
- 如 BL 状态仍被检测到，请确认 yosteebl 子模块已启用，且 TEEManager 模块也已启用
- 公开 keybox 根证书可能已过期或被吊销，如需通过密钥认证请使用有效私有 keybox
