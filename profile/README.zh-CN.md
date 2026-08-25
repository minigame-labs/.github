## Minigame Labs

[English](README.md) | [中文](README.zh-CN.md)

我们做 **Migo** —— 面向 Canvas / WebGL 小游戏的嵌入式原生运行时。

把它嵌进你的 App，HTML5 与小游戏内容即可原生运行：引擎版本由你自己钉死，而不是随 OEM
与系统更新漂移的系统 WebView。它是**游戏容器，不是浏览器**——没有 DOM、没有 CSS、
没有布局引擎，需要这些的内容不是它的目标。

### 我们发布什么

| | |
|---|---|
| **[migo](https://github.com/minigame-labs/migo)** | 运行时本体。Rust 核心、V8、Skia。Android · Linux · Windows · OpenHarmony，x86_64 与 arm64，全部由 CI 构建并附 attestation。 |
| **[migo-bench](https://github.com/minigame-labs/migo-bench)** | Migo 对比系统 WebView：同一游戏、同一设备、同一场次。原始行与测量方法都在仓库里。 |
| **[migo-examples](https://github.com/minigame-labs/migo-examples)** | 宿主集成示例。 |
| **[migo-web-adapter](https://github.com/minigame-labs/migo-web-adapter)** | 为假定浏览器环境的引擎（Cocos、Egret、Laya、Pixi）提供浏览器式 BOM/DOM 表面。 |
| **[migo-wx-adapter](https://github.com/minigame-labs/migo-wx-adapter)** | 发布小游戏形状的全局对象，别名到运行时自己的能力上。 |

引擎只安装一个能力表面 `migo.*`，本身不含任何 adapter 代码。内容期待的其余一切都是独立、
可组合的包——按需选零个、一个或两个。

### 数字，连同它们不成立的地方

Android 上对比系统 WebView，三款真实游戏，同一场次，交错测量、逐格温控：

- **内存：少 49–62%。** WebView 按公平口径计算，含它独立的渲染进程。
- **CPU：低 2.4–3.0×。**
- **帧率：打平。** 两侧中位数都是 60 fps。两边都跑 V8，所以我们不声称 JavaScript 更快，
  以后也不会。
- **启动：六项里五项更快**，而这五项中有一项落在装置的噪声本底之内——benchmark 把这句话
  明写出来，而不是把它四舍五入掉。

以上每一个数字都是 Android。OpenHarmony NEXT 上的性能是另一个问题、另一个答案，
它被写下来了，而不是靠暗示。

### 核你自己的内容

别信我们，也别把包发给我们。**[PRESCREEN.md](https://github.com/minigame-labs/migo/blob/master/PRESCREEN.md)**
就是我们会跑的那个工具，交给你自己跑：它报告一个包需要哪些 API、对照某个构建实际发布了
什么，以及它在真机上是否出画面。你的内容不离开你的机器。

---

BSL 1.1，源码可得——可阅读、可自行构建、可审计。
