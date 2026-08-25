## Minigame Labs

We build **Migo** — an embeddable native runtime for Canvas / WebGL mini-games.

Embed it in your app and HTML5 or mini-game content runs natively: one engine you
pin yourself, instead of a system WebView that drifts across OEMs and OS updates.
It is a **game container, not a browser** — there is no DOM, no CSS and no layout
engine, and content that needs those is not what it is for.

我们做的是 **Migo** —— 面向 Canvas / WebGL 小游戏的嵌入式原生运行时。嵌进你的 App，
HTML5 与小游戏内容即可原生运行：版本由你自己钉死，而不是随 OEM 与系统更新漂移的系统
WebView。它是**游戏容器，不是浏览器**——没有 DOM、没有 CSS、没有布局引擎。

### What we publish

| | |
|---|---|
| **[migo](https://github.com/minigame-labs/migo)** | The runtime. Rust core, V8, Skia. Android · Linux · Windows · OpenHarmony, x86_64 and arm64, all built and attested in CI. |
| **[migo-bench](https://github.com/minigame-labs/migo-bench)** | Migo vs the system WebView, same game, same device, same session. Raw rows and the method are in the repo. |
| **[migo-examples](https://github.com/minigame-labs/migo-examples)** | Host integration examples. |
| **[migo-web-adapter](https://github.com/minigame-labs/migo-web-adapter)** | A browser-style BOM/DOM surface for engines that assume one (Cocos, Egret, Laya, Pixi). |
| **[migo-wx-adapter](https://github.com/minigame-labs/migo-wx-adapter)** | Publishes a mini-game-shaped global, aliased onto the runtime's own capabilities. |

The engine installs exactly one capability surface, `migo.*`, and carries no adapter
code. Everything else content expects is a separate, composable package — take zero,
one, or both.

### What the numbers say, including where they don't

Measured on Android against the system WebView, three real games, one session,
interleaved and temperature-gated:

- **Memory: 49–62% lower.** WebView is counted fairly, including its separate
  renderer process.
- **CPU: 2.4–3.0× lower.**
- **Frame rate: a tie.** 60 fps median on both sides. Both run V8, so we do not
  claim faster JavaScript and never will.
- **Startup: faster on five of six measures**, and one of those five is inside the
  harness noise floor — which the benchmark says out loud rather than rounding up.

Every figure above is Android. Performance on OpenHarmony NEXT is a separate
question with a separate answer, and it is written down rather than implied.

### Checking your own content

Don't take our word for it and don't send us anything. **[PRESCREEN.md](https://github.com/minigame-labs/migo/blob/master/PRESCREEN.md)**
is the tool we would run, for you to run yourself: it reports which APIs a bundle
needs against what a build actually publishes, and whether it paints on a real
device. Your content never leaves your machine.

---

Source-available under BSL 1.1 — read it, build it, audit it. 源码可得、可自行构建与审计。
