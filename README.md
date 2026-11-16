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

GitHub 单文件硬限制 100 MB，且大文件单次 POST 在国内线路上极易中断，下列资源不进入 Git 历史，改为在 [Releases](../../releases) 以 40 MB 分卷发布。

| Release 附件 | 大小 | 合并后的文件 | 用途 |
| --- | --- | --- | --- |
| `B-resource-library.zip` | 63.2 MB | `B-素材库.zip` | 通用素材包（图片、图标、字体、切图） |
| `B-native-plugins.zip.part01` ~ `part04` | 147.6 MB | `B-原生第三方插件.zip` | 原生插件（相机、扫码、地图、推送等） |
| `B-offline-packaging-SDK.zip.part01` ~ `part06` | 221.5 MB | `B-离线打包SDK.zip` | Android 离线打包 SDK（Android Studio 工程与依赖） |

### 分卷合并

把分卷下载到同一目录，按 part 序号拼接（顺序不能乱，缺一段就解压失败）：

```bat
copy /b B-native-plugins.zip.part01+B-native-plugins.zip.part02+B-native-plugins.zip.part03+B-native-plugins.zip.part04 "B-原生第三方插件.zip"
copy /b B-offline-packaging-SDK.zip.part01+B-offline-packaging-SDK.zip.part02+B-offline-packaging-SDK.zip.part03+B-offline-packaging-SDK.zip.part04+B-offline-packaging-SDK.zip.part05+B-offline-packaging-SDK.zip.part06 "B-离线打包SDK.zip"
```

或 PowerShell：

```powershell
function Merge-Parts($pattern, $out) {
  $fs = [IO.File]::Create($out)
  Get-ChildItem $pattern | Sort-Object Name | ForEach-Object {
    $in = [IO.File]::OpenRead($_.FullName); $in.CopyTo($fs); $in.Close()
  }
  $fs.Close()
}
Merge-Parts 'B-native-plugins.zip.part*'        'B-原生第三方插件.zip'
Merge-Parts 'B-offline-packaging-SDK.zip.part*' 'B-离线打包SDK.zip'
```

合并后放进仓库根目录的 `B/` 下（与 `B-5+App离线打包文档.doc` 同级）。

> Release 附件名被 GitHub 强制为 ASCII，中文名见上表「合并后的文件」列。原始中文名与这些 ASCII 名都已写进 `.gitignore`，放回 `B/` 后不会误提交。

### 下载提示

Release 附件由 `objects.githubusercontent.com` 提供，国内直连常见长时间 0 字节或 `Connection was reset`。除浏览器挂代理外，命令行可显式指定本地 socks5：

```powershell
curl.exe -L --proxy socks5h://127.0.0.1:10808 -O https://github.com/QifaEduTech/Mobile-development/releases/download/v1.0/B-offline-packaging-SDK.zip.part01
```

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
