# CooPay 官方插件源

本仓库直接提供 CooPay 插件协议 v2 的 Lua ZIP 包，无需 GitHub Releases。

## 在 CooPay 中使用

新版 API 已预置此官方源。在「插件中心 → 插件源」刷新官方源，再到「市场」安装插件；新安装的插件需手动启用。已有部署请更新 API 后使用。

- 源 ID：`official`
- 类型：`github`
- 仓库：`LanQin996/CooPay-Plugins`
- 分支：`main`
- 子目录：留空
- 索引：[index.json](index.json)

不要求使用者提供公钥或私钥，不提供 `index.sig`。管理员信任插件源即授权执行其中的插件；客户端仍校验 HTTPS、文件大小、SHA-256、包结构及 manifest。渠道业务所需的支付宝/微信密钥与验签不受此规则影响。

## 当前插件

| 插件 | ID | 版本 |
| --- | --- | --- |
| 支付宝投诉 | `alipay_complaint` | 3.0.0 |
| 支付宝支付 | `alipay_payment` | 3.0.1 |
| 阿里云短信 | `aliyun_sms` | 3.0.0 |
| 实名本地调试 | `debug_realname` | 3.0.0 |
| 短信本地调试 | `debug_sms` | 3.0.0 |
| 易支付 | `easypay_payment` | 3.0.0 |
| 腾讯云实名认证 | `tencent_realname` | 3.0.0 |
| 微信投诉 | `wechat_complaint` | 3.0.0 |
| 微信支付（API v3） | `wechat_payment` | 3.0.0 |

所有包要求宿主插件协议 v2。微信支付插件使用微信 API v3；插件协议版本与渠道 API 版本不同。debug 插件仅供本地调试。ZIP 为跨平台 Lua 包，运行时由 API 启动隔离子进程。

## 发布维护

索引与所引用的 ZIP 必须在同一提交发布，目录序号递增。CooPay 下载会将 `main` 固定到提交 SHA，避免混用文件。包路径、大小和 SHA-256 以索引为准。更新只检查，不自动安装。

在 CooPay-Go 源码仓库运行 `go run ./cmd/plugin-market-publish -source-id official -out-dir <本仓库目录>`，测试与校验全部成功后检查差异并自行提交推送。发布工具不自动执行 Git 操作，不把渠道凭据或任何私钥提交到本仓库。
