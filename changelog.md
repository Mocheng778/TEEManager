# TEEManager v1.2.6 更新日志
## ✨新增
1. 新增Zygisk BL Native Hook层
    - Hook `__system_property_get` 拦截Native层直接读取系统属性
    - Hook `open/fopen` 拦截应用读取 `/proc/cmdline`
    - 自动伪装bootloader解锁相关全部属性，修复中国移动、农业银行等通过native检测BL的风控
2. 三层BL隐藏防护：post‑fs-data早期修正 + yosteebl后台循环修正 + Zygisk原生Hook
3. Hook仅作用第三方应用，不干扰系统与root进程

## 🛠优化
1. 优化keystore2重启逻辑，开机密钥伪装稳定性提升
2. 拓展厂商boot属性列表，适配更多品牌机型
3. 优化SELinux补丁，降低权限异常概率
4. action.sh一键批量导入全部第三方应用拦截列表

## 📌说明
> 需要开启Zygisk / Zygisk‑Next才能使用新增BL Hook功能
> 模块仅负责TEE密钥伪装与BL属性伪装，不提供完整Root隐藏，建议搭配Shamiko使用
> 本模块不需要合法keybox即可运行
