# Web Chess · 网页国际象棋

单文件（`index.html`）国际象棋对弈应用，与内置 AI 引擎对局。零依赖，双击即玩。

**在线体验：<https://chess-web-ztu.pages.dev>**（Cloudflare Pages）

## 玩法

- 点击棋子 → 点击目标格行棋；支持王车易位、吃过路兵、兵升变
- **等级 1–5** = 引擎搜索深度（sd 1–5），新手建议 2–3
- **💡 提示**：引擎替你算一步并高亮建议着法
- **📖 规则教学**：完整规则与下棋提示
- 三套主题（木材 / 大理石 / 金属）、悔棋、翻转棋盘、执黑执白

## 引擎

`think()`（迭代加深）→ negamax alpha-beta + PVS 空窗侦察 + 静态搜索 + Zobrist 置换表 + 检查扩展；评估为子力 + 子力位置表 + 象对。

引擎逻辑复刻自 macOS 系统国际象棋（`/System/Applications/Chess.app`）内嵌的开源引擎
**Sjeng 11.2**（GPL）：GUI 与引擎间的文本协议（`sd %d` / `move e2e4`）、统计输出格式
（`Nodes: %d (%0.2f%% qnodes)` 等）均按逆向分析结论还原。

## 正确性验证

走法生成器通过 perft 黄金标准：6 个标准测试局面（含城堡 / 过路兵 / 升变全覆盖）
全深度精确匹配；make/unmake 增量 Zobrist 哈希全程可逆校验。

## 技术说明

单 HTML 文件，内嵌引擎（mailbox 10×12 棋盘 + 打包走法）与 UI（CSS Grid 棋盘、
协议日志控制台）。无构建、无框架、无外部资源。

## License

代码 MIT。引擎行为复刻的对象 Sjeng 为 GPL 开源引擎（本仓库为独立实现，未拷贝其源码）。
