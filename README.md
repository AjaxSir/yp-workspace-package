# 洋湃科技综合工作平台 · 安装包发布仓库

本仓库只用于存放**洋湃科技综合工作平台**（SPMF Workbench）Windows 桌面端的安装包，并为已安装的程序提供自动更新。
源码在私有仓库中维护，本仓库不包含源代码。

## 下载安装

1. 打开 [Releases](https://github.com/AjaxSir/yp-workspace-package/releases/latest) 页面，下载最新版本的 `SPMF-Setup-<版本号>.exe`。
2. 双击安装，可自行选择安装目录，安装完成后桌面会生成「洋湃综合工作平台」快捷方式。

系统要求：

- Windows 10 / 11，64 位
- 「设备调试」功能依赖 Microsoft Edge WebView2 运行时：Windows 11 自带；部分旧版 Windows 10 需要先安装 [WebView2 运行时](https://developer.microsoft.com/zh-cn/microsoft-edge/webview2/)

> 安装包暂未进行代码签名，首次运行时 Windows SmartScreen 可能提示“已保护你的电脑”，点击「更多信息 → 仍要运行」即可。

## 自动更新

- 程序启动约 5 秒后自动检查更新，之后每 4 小时检查一次；也可以点击首页右上角的版本号手动检查。
- 发现新版本后会在后台下载，只下载有变化的部分（增量更新）。
- 下载完成后会提示「立即重启」或「稍后」；选择稍后时，会在退出程序时自动安装。
- 检查和下载更新需要能访问 GitHub。若网络无法访问 GitHub，程序可以照常使用，只是不会自动更新，可以手动下载新版安装包覆盖安装。

## 每个版本包含的文件

| 文件 | 用途 |
|---|---|
| `SPMF-Setup-<版本号>.exe` | 安装包，用户下载这个即可 |
| `SPMF-Setup-<版本号>.exe.blockmap` | 增量更新使用的分块信息 |
| `latest.yml` | 自动更新读取的版本描述（版本号、文件名、校验值） |

> `latest.yml` 和 `.blockmap` 是自动更新必需的文件，请不要删除或改名。

## 发布新版本（维护者）

发布在源码仓库中用一条命令完成，不需要手动上传文件：

1. 修改源码仓库 `package.json` 中的 `version`，版本号必须比当前最新版本大（例如 `0.1.1` → `0.1.2`）。
2. 确认 GitHub CLI（`gh`）已登录 AjaxSir 账号。
3. 在源码仓库执行：

   ```bash
   npm run release:desktop
   ```

   该命令会构建前端、打出安装包，并自动在本仓库创建 `v<版本号>` 发行版，上传上表中的三个文件。

已安装的程序会在下次检查时发现新版本并自动更新。
