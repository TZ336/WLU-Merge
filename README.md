[README.md](https://github.com/user-attachments/files/33388911/README.md)
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
HKU and UCAS: their university articles' logo images on English Wikipedia.
USTC: https://www.ustc.edu.cn/images/zkdlogo.png
Westlake: https://en.westlake.edu.cn/about/VIS/

Logos belong to their respective institutions. This is an independent game and does not imply university endorsement. Some supplied horizontal logo assets are displayed through SVG viewports showing their emblem component.

Physics: Matter.js 0.20.0, MIT license (included in LICENSE-matter.txt).

Logo QA: SYSU uses a circular SVG clip matching its emblem edge, removing its opaque rectangular background and the artifacts outside the emblem. All game-piece logos are clipped to their disc; non-circular shields and Westlake are fitted fully inside the disc to preserve their entire shape.

Physics: each level has 1.2 times the previous radius (20% larger in radius and diameter, 44% larger in area). All logos are scaled down by 16.6% from the previous version: WHU radius is approximately 18.84 and Westlake radius is 241.86. Logos are dynamic rigid disks with finite rotational inertia. Friction is 0.2 for both logo–logo and logo–floor contact; Matter.js static-friction multiplier is 1. Contact restitution is 0.4. No floor position lock, linear-velocity reset, forced sleeping, or artificial air drag is applied. The engine continuously handles friction, rotation, and collision response. Automatic sleeping is disabled so a logo falls immediately when its support merges, moves, or disappears. All logos use density 0.002 in simulation units, including merged logos; mass is density × π × radius². Merges preserve linear/angular momentum, but use the new level radius and the same density rather than adding the old masses. Level growth and boundary placement are game mechanics.

Dynamic drop limit (1-based ranks): when the highest logo currently on the board is rank 8 or below, NJU (rank 6) is the maximum drop. Above rank 8, the maximum drop rank is highest board rank minus 3. All ranks from WHU to the current limit are eligible; lower ranks are more common. The queued previews remain eligible when the limit rises.

A newly dropped logo retains zero angular velocity and its upright orientation through free fall and landing until it first contacts another logo. After that contact, normal rigid-body rotation is enabled. Merged logos retain collision-generated angular momentum.
