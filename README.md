# 移动应用与开发赛项 · 资料库

面向全国职业院校技能大赛「移动应用与开发」赛项（ZZ039）的训练与交付资料。素材、离线打包工具链、十套赛题、交付模板与待测应用集中在一个仓库，克隆即用。

## 目录结构

| 目录 | 内容 |
| --- | --- |
| `A/` | 素材 —— 时代楷模文字及图片素材 |
| `B/` | 工具链与文档 —— 5+App 离线打包文档与 SDK、MUI / ECharts 离线文档、Git 使用手册、原生第三方插件、素材库、DigitalLife 初始框架、数字生活 API 接口文档 |
| `C/` | 交付与评测 —— 产品使用手册模板、测试报告模板、乡村民宿 APP 功能范围、待测 APK |
| `ZZ039 移动应用与开发赛项赛题/` | 第一套 ~ 第十套赛题文档 |

## 大文件（Release）

GitHub 单文件硬限制 100 MB，下列三个包不进入 Git 历史，改为在 [Releases](../../releases) 下载：

| 文件 | 大小 | 用途 |
| --- | --- | --- |
| `B-素材库.zip` | 63.2 MB | 通用素材包（图片、图标、字体、切图） |
| `B-原生第三方插件.zip` | 147.6 MB | 原生插件（相机、扫码、地图、推送等） |
| `B-离线打包SDK.zip` | 221.5 MB | Android 离线打包 SDK（Android Studio 工程与依赖） |

下载后放回 `B/` 目录，与 `B-5+App离线打包文档.doc` 同级即可。三个包已在 `.gitignore` 中排除，放回后不会误提交。

## 技术栈

- HBuilderX / uni-app / 5+App，Android 离线打包
- MUI 组件 + ECharts 图表
- 原生插件（Java / Android Studio）
- 输出 Android APK

## 典型工作流

1. 从 `ZZ039 移动应用与开发赛项赛题/` 取当前赛题
2. 用 `B/B-5+App离线打包文档.doc` 与 `B/B-离线打包SDK.zip` 搭建离线打包环境
3. 素材取自 `A/` 与 Release 中的 `B-素材库.zip`
4. 按 `C/乡村民宿APP功能范围.pdf` 实现，用 `C/待测乡村民宿.apk` 对照验证
5. 交付三件套：APK + 产品使用手册（模板 `C/C-产品使用手册模板.doc`）+ 测试报告（模板 `C/C-测试报告模板.doc`）

## 仓库约定

- 单个文件 ≤ 50 MB 入库；更大的资源走 Release 或 Git LFS
- `.gitignore` 已排除 `B/` 下三个超限包、Word 临时锁文件 `~$*`、`Thumbs.db` / `desktop.ini` / `.DS_Store`

## 提交

```powershell
git add .
git commit -m "说明"
git push
```

国内网络直连 GitHub 常见 `Connection was reset`，可临时走本地 socks5 代理：

```powershell
git -c http.proxy=socks5h://127.0.0.1:10808 push
```

## 版本

- `v1.0` —— 首次整理：十套赛题、工具链文档与 SDK、交付模板、待测 APK；三个超限资源包移至 Release。
