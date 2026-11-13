# Micalith Launcher 官网

Micalith Launcher 的官方网站，用 GitHub Pages 托管。

线上地址：<https://yuhaoya.github.io/micalith-launcher-web/>

主项目：[yuhaoya/micalith-launcher](https://github.com/yuhaoya/micalith-launcher)

## 技术栈

纯静态：原生 HTML + CSS + JavaScript。没有构建步骤、没有框架、没有 CDN、没有网络字体，克隆下来直接就是可部署状态。

```
.
├── index.html      页面结构与全部文案
├── styles.css      样式与主题变量
├── script.js       主题切换、滚动进场、截图灯箱
└── assets/
    ├── app.png     应用图标
    └── shots/      启动器界面截图
```

## 本地预览

```powershell
python -m http.server 8765 --bind 127.0.0.1
# 浏览器打开 http://127.0.0.1:8765/
```

直接双击 `index.html` 也能看，但用静态服务器更接近线上环境。

## URL 参数

方便截图、分享和排查问题：

| 参数 | 作用 |
| --- | --- |
| `?theme=light` / `?theme=dark` | 强制指定配色，覆盖系统偏好与本地记忆 |
| `?still=1` | 关闭滚动进场动画（截图、打印时用） |

正常访问时主题按「本地记忆 → 系统偏好」的顺序决定，右上角按钮可手动切换并记住选择。

## 修改内容

### 下载地址

两个下载按钮指向主仓库的 GitHub Releases：

```
https://github.com/yuhaoya/micalith-launcher/releases/download/beta/mcl-gui.exe
https://github.com/yuhaoya/micalith-launcher/releases/download/beta/mcl-gui-win7.exe
```

发布新版本时，把 `index.html` 里这两个 `href` 的 tag 从 `beta` 换成新 tag（也可以用 `latest/download/文件名`，这样不用每次改）。

同时更新卡片里的文件名、版本和大小，以及 `下载 → Windows 版` 下方 `.dl-hint` 处的 SHA256。

### 发新版时同步

- 页面上的版本号与安装包大小
- `assets/shots/` 里的截图（如果界面有变化）

### 换截图

截图在 `assets/shots/`，保持文件名直接覆盖即可。当前统一用浅色 + 绿色强调色。

建议截图规格：Windows 平台实际渲染，窗口 1280×820，导出 PNG。

## 部署

推送到 `main` 分支后 GitHub Pages 自动发布（仓库 Settings → Pages → Source 选 `main` / `/ (root)`）。

页面全部使用相对路径，所以即使站点挂在子路径（`/micalith-launcher-web/`）也能正常工作。

## 设计说明

- 配色沿用启动器本身：中性层叠背景 + 单一强调色。浅色 `#107C10`，深色自动提亮到 `#4BD44B`
- 间距、圆角、阴影幅度参照 Fluent Design 2，与客户端观感一致
- 进场动画用 CSS `animation`，而不是把元素初始设为 `opacity: 0`。这样即使 JS 不执行、或截图环境冻结动画，内容也始终可见
- 尊重 `prefers-reduced-motion`

## 许可

MIT，与主项目一致。
