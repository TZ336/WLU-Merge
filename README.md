# University Merge / 合成西湖大学

Open PLAY.html in Safari, Chrome, Edge, or Firefox. Everything is bundled; no internet or installation is needed. Use 中文 / English at the top to switch languages.

打开 PLAY.html 即可游玩，无需安装或联网。点击顶部 中文 / English 切换语言。

Drag sideways and release (or tap) to drop. Use ← → to aim and Space/Enter to drop. P pauses. Matching logos merge into the next university. Keep the stack below the dotted line; reach Westlake to win, then continue playing if you wish. Best scores and language preferences are saved in the browser where supported.

左右拖动，松手投放；也可直接点击投放。方向键瞄准，空格/回车投放，P 暂停。两枚相同校徽合成下一所大学。堆叠持续超过警戒线则结束；合成西湖大学获胜，可继续挑战。浏览器支持时会保存最高分和语言偏好。

Exact size order / 从小到大：
WHU → SUSTech → SYSU → Tongji → HKUST → NJU → SJTU → FDU → HKU → ZJU → THU → PKU → USTC → UCAS → Westlake University

Edit core.js for levels and physics, game.js for interaction and translations, and style.css for layout, and logo-renderer.js for logo fitting and clipping. index.html is the editable multi-file entry point. PLAY.html bundles the same app into one portable file. Changing source files requires regenerating PLAY.html with the supplied build_offline.py (Python 3).

大学顺序仅为用户指定的游戏设定，不代表排名。University order is the requested game progression, not a ranking.

## Asset credits

WHU, SYSU, Tongji, NJU, SJTU, FDU, ZJU, THU, and PKU logo assets: https://xanderxuan123-collab.github.io/sysu-game/ (the supplied reference game).
SUSTech: https://www.sustech.edu.cn/ and https://www.urongda.com/logos/4144014325
HKUST: https://hkust.edu.hk/sites/default/files/2024-03/HKUST_logo_1.svg
HKU: its university article logo image on English Wikipedia.
USTC: path-only vector seal from https://jbyang1987.github.io/ustclogo/ (校徽/ustc校徽 科大蓝.svg).
UCAS: vector emblem extracted from the official standard-logo AI/PDF at https://onestop.ucas.ac.cn/Content/Upload/2020/9/1.zip (resource page https://onestop.ucas.ac.cn/Home/Info/6b9e95dc-5785-4eee-b25f-1f884698cfc3). Neither USTC nor UCAS embeds a low-resolution raster image.
Westlake: https://en.westlake.edu.cn/about/VIS/

Logos belong to their respective institutions. This is an independent game and does not imply university endorsement. Some supplied horizontal logo assets are displayed through SVG viewports showing their emblem component.

Physics: Matter.js 0.20.0, MIT license (included in LICENSE-matter.txt).

Logo QA: SYSU uses a circular SVG clip matching its emblem edge, removing its opaque rectangular background and the artifacts outside the emblem. All game-piece logos are clipped to their disc; non-circular shields and Westlake are fitted fully inside the disc to preserve their entire shape.

Physics: exact circular contact geometry, uniform gravitational acceleration, rigid disks with mass = m₀ × 2^level (zero-based), where m₀ = 0.002 × π × r₀² and rotational inertia = mr²/2. Each level has 1.2 times the previous radius; WHU radius is approximately 15.26 and Westlake radius is 195.9066. An analytic disk contact solver replaces Matter's polygon collision approximation; Matter.js supplies body storage and utility/event APIs. Normal impulses use the selected restitution (default 0.4), and tangential impulses obey Coulomb friction (default 0.2). Infinite friction enforces no slip while contact can support a positive normal impulse. Normal forces cannot pull bodies together. Floor and walls are fixed external supports. There is no air drag, floor lock, artificial spin reset, sleeping, or unforced velocity damping. Gravity acts through each disk's center, so a disk dropped straight down remains upright naturally; sliding or oblique contacts can generate spin. Unsupported disks immediately fall.

Merges place the new disk at the parents' center of mass and preserve total mass, linear momentum, and angular momentum. Each disk has uniform areal density internally, but density increases between levels because mass doubles while area grows by 1.44. Directly dropped higher-level disks have the same mass as disks obtained by merging to that level. Every new disk uses I = mr²/2 and density = m/(πr²). Instantaneous merging is the one explicit gameplay idealization preserved at the user’s request: the prescribed shape change can require boundary correction or increase rotational kinetic energy. It is not represented as a fully physical coalescence process. Mass and linear/angular momentum are still conserved at the transformation. Merges are not clamped or teleported away from walls. Continuous impact-time detection solves disk–disk and disk–plane flight intersections (including acceleration); adaptive substeps are recomputed after each event without the old 128-step cap. Force-driven acceleration is included in step selection. Initially stationary supports do not receive artificial restitution bounces from gravity. Very near existing contacts use iterative contact impulses and small position corrections to approximate rigid nonpenetration without endless microscopic impact events. Simultaneous contacts use an energy-admissible combination of compression and restitution impulses if independent Newton restitution targets would create kinetic energy; the selected e remains exact for isolated impacts, while coupled impacts can have reduced effective restitution. Drops into an occupied spawn volume are refused without consuming a drop. This is a numerical simulation, not an exact continuous-time solution: dense simultaneous contacts and extremely high velocities retain finite-step error.

Dynamic drop limit (1-based ranks): when the highest logo currently on the board is rank 8 or below, NJU (rank 6) is the maximum drop. Above rank 8, the maximum drop rank is highest board rank minus 3. All ranks from WHU to the current limit are eligible; lower ranks are more common. The queued previews remain eligible when the limit rises.


Before every round, the bilingual settings screen lets players adjust two sliders. e ranges from 0 to 1. The μ slider displays only friction values: 0 at the left, 1 in the middle, and ∞ at the right. Its nonlinear mapping is μ=tan(πp/2), where p is normalized slider position. The rightmost endpoint selects μ=∞. This uses a no-slip tangential contact constraint instead of passing numerical infinity to the physics engine. Finite μ values use ordinary friction. Defaults remain e=0.4 and μ=0.2. Values apply to all logos and boundaries for that round. Cancelling new-round setup preserves the current round.
[Uploading README.md…]()
