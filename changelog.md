# TEEManager 更新日志

## v1.2.6 (2026-08-26)

### 新增
- **Zygisk BL Hook（原生层拦截）**
  - 新增 `zygisk/arm64-v8a.so` 和 `zygisk/armeabi-v7a.so`
  - Hook `__system_property_get`：拦截 Native 层属性读取，BL 相关属性返回伪装值
  - Hook `open` / `fopen`：拦截 `/proc/cmdline` 读取，自动替换 `orange→green`、`unlocked→locked`
  - 伪装 30+ BL 相关属性（含厂商特有属性）
  - 仅对第三方应用生效（uid >= 10000），不影响系统进程
  - 需开启 Zygisk（Magisk 内置 / KernelSU 需装 Zygisk Next/ReZygisk）

### 修复
- 修复中国移动、中国农业银行等应用通过 Native 层直接读取属性和 `/proc/cmdline` 检测 BL 的问题
- 修复仅用 `resetprop` 改属性无法绕过 Native 层检测的问题

---

## v1.2.4 (2026-08-25)

### 优化
- 内部稳定性优化
- 兼容性改进

---

## v1.2.2 (2026-08-25)

### 新增
- **三阶段 BL 属性修正**
  - 第一阶段：post-fs-data 早期修正（系统服务启动前）
  - 第二阶段：service 首次修正（开机完成后）
  - 第三阶段：后台循环持续修正（每30秒检查一次，防止属性被系统服务恢复）
  - 新增 yosteebl `module.prop`，规范模块标识
- **自动重启 keystore2**
  - 首次属性修正完成后自动重启 keystore2 进程
  - 修复"重启设备后不生效，需手动执行 action.sh 才生效"的问题
- **更多属性修正**
  - 新增 27 个 BL 相关属性修正
  - 新增小米/红米特有属性：`ro.secureboot`、`ro.boot.securebootlock`、`persist.sys.oem.unlock`
  - 新增三星特有属性：`ro.boot.emmc.checksum`
  - 新增厂商通用属性：`ro.boot.secureboot`、`ro.boot.warranty_bit`、`sys.oem_unlock_allowed`、`ro.oem_unlock_supported`
- **在线更新支持**
  - `module.prop` 新增 `updateJson` 字段
  - 新增 `TEEManager.json` 在线更新配置文件
  - `script3.sh` 密钥下载地址改为从 GitHub 仓库获取
- **机型适配优化**
  - 动态检测 keystore UID（优先 `id -u keystore`，备选目录所有者推断）
  - 自动修复 SELinux 上下文（`restorecon -R`）
  - 支持机型列表扩展：新增三星/索尼/华硕/摩托罗拉
- **应用拦截扩展**
  - `injector.toml` 默认 scoop 从 5 个扩展到 70+ 应用
  - 新增密钥认证工具、Root 检测工具、Google 服务、银行/支付、游戏反作弊、厂商安全中心等
  - `action.sh` 自动将全部第三方应用加入拦截列表

### 修复
- 修复"开机5分钟后BL被检测"的问题（属性被系统服务恢复，后台循环持续修正）
- 修复部分机型 keystore UID 不匹配导致权限错误的问题
- 修复部分机型 SELinux 上下文不正确的问题

---

## v1.2.0 (2026-08-23)

### 初始版本
- 基于 Oh My Keymint 二次开发
- 自定义密钥伪装（KeyMint AIDL 接口完整实现）
- BL 属性修正（yosteebl 模块）
- keystore2 注入拦截
- WebUI 单页管理界面（一键更新3绿密钥）
- 支持 Root 管理器：Magisk / Alpha / KernelSU / KernelSU Next / SukiSU-Ultra / ApkeSU
- 支持系统：Android 9-17
- 支持架构：arm64-v8a
- 支持机型：一加/真我/OPPO/vivo/IQOO/小米/红米/红魔/联想/魅族