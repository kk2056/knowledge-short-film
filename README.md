# knowledge-short-film

在抖音上，有一类内容正在悄悄火起来：全程没人出镜、没人解说，就靠画面和字幕，把一个小知识点讲清楚。网友把这类内容叫「Vibe 知识大赏」。

这个 skill 就是专门用来生成这类视频的。它自带的两套画风，是分析过几条千万级爆款之后，提炼出来的共性。

一套叫「夜曲」，走深色质感路线，讲偏底层、偏难懂的知识，画面慢慢铺，让观众沉进去。

另一套叫「寓言」，走故事演绎路线，把心理学、行为学里那些抽象概念，直接用一个小剧情演出来，让观众"看见"逻辑。

用法很简单，把一段写好的文案，或者一个选题，丢给 Agent。它会先帮你选画风、写好逐字字幕、排好分镜，再生成一套能直接运行的代码工程。渲染之前，会先给你一段 30 秒左右的样片，你确认没问题，它才做全片。音效它会自动配好，BGM 想换成自己的也可以。

原理不复杂。用 Canvas 和 JavaScript 一帧一帧把画面画出来，再驱动浏览器逐帧截图，把截图串成视频、叠上声音。字体走开源协议，不夹带私货。说白了，就是用一条代码流水线，把这种视频稳定生产出来。

## 夜曲：《折叠》

题目是蛋白质折叠，2024 年诺贝尔化学奖。这里是开头 33 秒。

![折叠](examples/fold_C.gif)

## 寓言：《鸽子的迷信》

一只鸽子怎么变得迷信。这里是开头 33 秒。

![鸽子的迷信](examples/pigeon_B.gif)

## 安装

把这个目录放到 Agent 的 skill 目录，文件夹名保持 `knowledge-short-film`。WorkBuddy 常见位置是 `~/.workbuddy/skills/knowledge-short-film`；Claude Code 是 `~/.claude/skills/knowledge-short-film`。交给 Agent 的流程在 `SKILL.md`。

```bash
pip install -r requirements.txt
python -m playwright install
python engine/get_fonts.py
```

还需要本机已经安装的 Google Chrome 和 ffmpeg。渲染脚本打开的是本机 Chrome。字体是 SIL Open Font License，不放进仓库，所以要先跑一次 `get_fonts.py`。

在你自己的项目里建工程，不要建在这个 skill 目录里。

```bash
python scripts/new_film.py <工程目录> --world C
python engine/render.py <工程目录> --serve
```

`--world` 用 `C`（夜曲）或 `B`（寓言）。命令和写法见 `references/engine.md`。

## 许可

引擎、脚本和文档里的方法说明使用 MIT 许可，见 `LICENSE`。

做新片请用 `python scripts/new_film.py` 建一个空骨架，照自己的分镜表现写，不要把 `examples/` 里的画面搬进自己的片子。
