## Minigame Labs

[English](README.md) | [中文](README.zh-CN.md)

We build **Migo** — an embeddable native runtime for Canvas / WebGL mini-games.

Embed it in your app and HTML5 or mini-game content runs natively: one engine you
pin yourself, instead of a system WebView that drifts across OEMs and OS updates.
It is a **game container, not a browser** — there is no DOM, no CSS and no layout
engine, and content that needs those is not what it is for.

### What we publish

| | |
|---|---|
| **[migo-runtime](https://github.com/minigame-labs/migo-runtime)** | The runtime's releases. Rust core, V8, Skia. SDK packages for Android · iOS · macOS · Linux · Windows · OpenHarmony, x86_64 and arm64, built in CI and published with checksums and SBOMs. |
| **[migo-bench](https://github.com/minigame-labs/migo-bench)** | Migo vs the system WebView, same game, same device, same session. Raw rows and the method are in the repo. |
| **[migo-examples](https://github.com/minigame-labs/migo-examples)** | Host integration examples. |
| **[migo-web-adapter](https://github.com/minigame-labs/migo-web-adapter)** | A browser-style BOM/DOM surface for engines that assume one. Pixi, Phaser, three.js, Babylon.js, PlayCanvas and Egret run on it unmodified, and so do a Godot 4 web export -- WebAssembly, WebGL 2 and AudioWorklet -- and a Defold 1.14 HTML5 bundle. Cocos Creator's web build is not verified yet, so it is not claimed. |
| **[migo-wx-adapter](https://github.com/minigame-labs/migo-wx-adapter)** | Publishes a mini-game-shaped global, aliased onto the runtime's own capabilities. Cocos Creator's and LayaAir's mini-game builds run on it. |

The engine installs exactly one capability surface, `migo.*`, and carries no adapter
code. Everything else content expects is a separate, composable package — take zero,
one, or both.

`migo.*` follows the mini-game platform's API: every API its documentation lists has an
answer on Android, iOS and macOS, and Linux and Windows lack only a few hardware APIs
(OpenHarmony covers far fewer for now). Each API on each platform, and whether the
conformance suite verified it there, is in
[API platform support](https://minigame-labs.com/docs/en/capabilities/api-support/).

Not only test scenes: whole games, built unmodified by their own toolchains, reach their title screens
on Linux with no uncaught error. PixiJS's
[Bubbo Bubbo and Puzzling Potions](https://github.com/pixijs/open-games) through the web adapter, web fonts,
Spine animation and sound included; Godot's
[Dodge the Creeps](https://github.com/godotengine/godot-demo-projects/tree/master/2d/dodge_the_creeps), exported
by Godot 4.7 -- 40 MB of WebAssembly, WebGL 2, its audio through AudioWorklet -- through the web adapter too;
three.js's first-person example game (games_fps: a glTF level, octree collisions, shadows), through the web adapter; and
two levels written for the conformance suite in Cocos Creator 3.8 -- one with Box2D as WebAssembly, particles and
sound -- built by the editor to its mini-game target, through the mini-game adapter; a LayaAir 3.4.3 level built by
LayaAir's own build to its mini-game target (Box2D as WebAssembly, sound), through the mini-game adapter; and a Defold
1.14.1 level bundled for HTML5 by Defold's own build tool (Box2D, a GUI, sound), through the web adapter.

### What the numbers say, including where they don't

Measured on Android against the system WebView, three real games, one session,
interleaved and temperature-gated:

- **Memory: 45–56% lower.** WebView is counted fairly, including its separate
  renderer process.
- **CPU: 2.4–2.9× lower**, and 3.5–4.7× fewer CPU cycles counted core cluster by core cluster.
- **Frame rate: a tie.** 60 fps median on both sides. Both run V8, so we do not
  claim faster JavaScript and never will.
- **Startup: first frame clearly faster on all three games, game-ready on one.**
  The other two readings are not quoted — one is inside the harness's noise floor, the
  other is a measurement the harness has never resolved — and the benchmark says so out
  loud rather than rounding them up.

These are the 2026-11-19 figures. The ones published before them (47–58% less memory)
were measured with a hardware layer our own WebView test app put on the WebView, which an
ordinary app does not have; it cost the WebView about 24 MB per game. The benchmark
records the finding and the re-measurement ([RESULTS §9.4](https://github.com/minigame-labs/migo-bench/blob/main/RESULTS.en.md)).

Every figure above is Android. Performance on OpenHarmony NEXT is a separate
question with a separate answer, and it is written down rather than implied.

### Trying it

Take an SDK package from [the releases](https://github.com/minigame-labs/migo-runtime/releases),
verify it against its `SHA256SUMS.txt`, and start from a host in
[migo-examples](https://github.com/minigame-labs/migo-examples). The
[developer docs](https://minigame-labs.com/docs/en/) cover every platform.

---

Released under the [Migo Binary License 1.0](https://github.com/minigame-labs/migo-runtime/blob/master/LICENSE):
free to develop, test and evaluate at any scale, and free to ship in your own app
below USD 1 million in annual revenue and 3 million monthly active users.
v0.9.19 and earlier remain under BSL 1.1, the license they were released under.
Licensing: [licensing@minigame-labs.com](mailto:licensing@minigame-labs.com).
