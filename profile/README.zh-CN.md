## Minigame Labs

[English](README.md) | [中文](README.zh-CN.md)

我们做 **Migo** —— 面向 Canvas / WebGL 小游戏的嵌入式原生运行时。

把它嵌进你的 App，HTML5 与小游戏内容即可原生运行：引擎版本由你自己钉死，而不是随 OEM
与系统更新漂移的系统 WebView。它是**游戏容器，不是浏览器**——没有 DOM、没有 CSS、
没有布局引擎，需要这些的内容不是它的目标。

### 我们发布什么

| | |
|---|---|
| **[migo-runtime](https://github.com/minigame-labs/migo-runtime)** | 运行时的发布仓库。Rust 核心、V8、Skia。Android · iOS · macOS · Linux · Windows · OpenHarmony 的 SDK 包，x86_64 与 arm64，由 CI 构建，附校验和与 SBOM 发布。 |
| **[migo-bench](https://github.com/minigame-labs/migo-bench)** | Migo 对比系统 WebView：同一游戏、同一设备、同一场次。原始行与测量方法都在仓库里。 |
| **[migo-examples](https://github.com/minigame-labs/migo-examples)** | 宿主集成示例。 |
| **[migo-web-adapter](https://github.com/minigame-labs/migo-web-adapter)** | 为假定浏览器环境的引擎（Cocos、Egret、Laya、Pixi）提供浏览器式 BOM/DOM 表面。 |
| **[migo-wx-adapter](https://github.com/minigame-labs/migo-wx-adapter)** | 发布小游戏形状的全局对象，别名到运行时自己的能力上。 |

引擎只安装一个能力表面 `migo.*`，本身不含任何 adapter 代码。内容期待的其余一切都是独立、
可组合的包——按需选零个、一个或两个。

### 数字，连同它们不成立的地方

Android 上对比系统 WebView，三款真实游戏，同一场次，交错测量、逐格温控：

- **内存：少 45–56%。** WebView 按公平口径计算，含它独立的渲染进程。
- **CPU：低 2.4–2.9×**，按核簇逐个计数的 CPU 周期少 3.5–4.7×。
- **帧率：打平。** 两侧中位数都是 60 fps。两边都跑 V8，所以我们不声称 JavaScript 更快，
  以后也不会。
- **启动：三款游戏首帧都明显更快，一款可玩明显更快。** 另外两项不引用——一项落在装置的噪声本底之内，
  另一项是这套装置历来读不出差异的量——benchmark 把这句话明写出来，而不是把它们四舍五入掉。

以上是 2026-11-19 的数字。此前公布的数字（内存少 47–58%）是在我们自己的 WebView 测试 App 给 WebView
加了一层硬件图层的情况下测的，普通 App 里没有这一层，它让 WebView 每款游戏多算约 24 MB。
benchmark 记录了这个发现和重测（[RESULTS §9.4](https://github.com/minigame-labs/migo-bench/blob/main/RESULTS.md)）。

以上每一个数字都是 Android。OpenHarmony NEXT 上的性能是另一个问题、另一个答案，
它被写下来了，而不是靠暗示。

### 试用

从[发布页](https://github.com/minigame-labs/migo-runtime/releases)取一个 SDK 包，用它的
`SHA256SUMS.txt` 校验，再从 [migo-examples](https://github.com/minigame-labs/migo-examples)
里的宿主示例起步。各平台的接入见[开发者文档](https://minigame-labs.com/docs/)。

---

以 [Migo Binary License 1.0](https://github.com/minigame-labs/migo-runtime/blob/master/LICENSE) 发布：
开发、测试与评估不限规模、免费；年收入不超过 100 万美元、月活不超过 300 万时，可免费嵌入
自己的 App 上线。v0.9.19 及更早的版本仍适用发布时的 BSL 1.1。
许可洽谈：[licensing@minigame-labs.com](mailto:licensing@minigame-labs.com)。
