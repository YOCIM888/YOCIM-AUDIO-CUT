# YOCIM Audio Cut

[English](README.md) | [简体中文](README.zh-CN.md)

一款在浏览器中运行的本地优先音频编辑器。音频文件在浏览器内解码和处理，不会上传到服务器。基于 Vue 3、TypeScript 与 Web Audio API 构建。

**[在线体验](https://audio.yocim.top/)**

## 功能特性

- **本地处理、隐私优先** — 点击导入或将文件拖到窗口即可使用，解码与 DSP 全部在本机浏览器内完成。
- **波形编辑** — 精确选区、缩放平移、过零吸附、剪切/复制/粘贴、淡变、增益与撤销重做。
- **多轨时间线** — 多轨片段、拖动排布、非破坏性边缘裁剪、拆分删除、轨道增益/声像，以及麦克风录音。
- **非破坏性效果链** — 多段 EQ、滤波器、动态处理等，支持实时 A/B 试听；导出时才渲染一次效果。
- **变速不变调** — 在 Web Worker 中使用 WSOLA 算法处理，范围 0.25x–4x，可仅作用于当前选区。
- **测量与修复** — LUFS / RMS / 真峰值电平、响度归一化、语谱图、降噪、去咔嗒、限制器与变调。
- **标记与导航** — Cue 列表、CSV 导入导出、可调吸附网格、键盘导航与静音分段检测。
- **视频提取音频** — 使用自托管的 ffmpeg.wasm 核心，离线从视频中提取音频。
- **批量处理** — 多文件排队串行处理，可逐个下载或打包为 ZIP。
- **灵活导出** — WAV（16/24/32-bit）、MP3、FLAC、M4A/AAC、OGG、WebM；可设置采样率、声道、码率、元数据与导出范围（全曲、选区或多轨混音）。
- **无损工程** — `.yac.zip` 工程包以 32-bit 浮点 WAV 保存 PCM，并在 IndexedDB 中自动恢复现场。

## 快速开始

建议使用 Node.js 22（与 CI 使用版本一致）。

```bash
npm install
npm run dev
```

打开 Vite 输出的地址即可使用。构建并预览生产版本：

```bash
npm run build
npm run preview
```

可直接部署的静态站点产物位于 `dist/`。

## 使用方式

1. 点击**导入音频**，或把音频文件拖入窗口。支持浏览器可解码的格式，例如 WAV、MP3、FLAC、OGG、M4A（具体取决于浏览器）。
2. 在编辑器顶部切换**波形编辑**和**多轨时间线**视图。
3. 使用右侧栏页签进行编辑、效果、测量、标记、修复、录音或导出。
4. 可从顶栏保存 `.yac.zip` 工程文件，之后再打开；同一浏览器中的未完成工作也会自动恢复。
5. 打开**导出**页签选择格式并下载结果。在支持 File System Access API 的浏览器中，WAV 还可以直接流式写入文件。

## 键盘快捷键

| 按键 | 功能 |
| --- | --- |
| `Space` | 播放 / 暂停 |
| `B` | 旁路 / 启用效果链 |
| `M` | 在播放头处添加标记 |
| `[` / `]` | 跳到上一个 / 下一个标记 |
| `←` / `→` | 微调选区或播放头（`Shift` 调右边界，`Ctrl` 调左边界，`Alt` 为 10 倍步进） |
| `Home` / `End` | 跳到开头 / 结尾 |
| `Ctrl+Z` / `Ctrl+Shift+Z` / `Ctrl+Y` | 撤销 / 重做 |
| `Ctrl+C` / `Ctrl+X` / `Ctrl+V` | 复制 / 剪切 / 粘贴 |
| `Delete` | 删除选中区域 |

## 项目结构

| 路径 | 说明 |
| --- | --- |
| `src/audio/` | DSP 核心：效果、响度、频谱处理、混音、多轨模型 |
| `src/workers/` | 音频处理、峰值计算与 MP3 编码 Worker |
| `src/composables/` | 导入、导出、录音、批量处理与工程持久化 |
| `src/components/` | 编辑器界面组件与右侧栏面板 |
| `src/stores/` | Pinia 编辑器状态与通知 |
| `public/` | 静态资源、favicon、`robots.txt`、`sitemap.xml` 与自托管 ffmpeg 核心 |
| `.github/workflows/deploy.yml` | GitHub Pages 部署工作流 |

## 部署

仓库内置 GitHub Pages 工作流：每次推送到 `main` 分支都会构建并发布 `dist/`。自定义域名为 `audio.yocim.top`（见 `public/CNAME`），Vite 的 `base` 已设为 `/`，适用于根路径部署。

## 许可证

[ISC 许可证](LICENSE) — Copyright (c) 2026 YOCIM。
