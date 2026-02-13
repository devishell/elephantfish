# Elephantfish 中国象棋 AI

基于 [Elephantfish](https://github.com/bupticybee/elephantfish) 引擎的网页版中国象棋，**单个 HTML 文件**即可运行，无需任何依赖。

![游戏截图](screenshot.png)

## 特性

- **零依赖** — 单个 `elephantfish.html` 文件，双击即可在浏览器中打开
- **完整 AI 引擎** — 移植自 Elephantfish Python 版，包含完整搜索算法
- **多种模式** — 人机对战 / 人人对战 / AI 对战
- **可调难度** — 搜索深度 1~20 层自由设置
- **AI 执棋选择** — 可切换 AI 执红或执黑，棋盘自动翻转
- **走子可视化** — 棋盘上高亮显示最近一步走法路径
- **实时评分** — 局面评分 + 走棋记录含评分变化和 AI 思考耗时

## AI 算法

```
搜索框架
├── MTD-bi (MTD(f) 变体)
│   └── Alpha-Beta 搜索 (bound 函数)
│       ├── 转置表 (Transposition Table)
│       ├── 空着裁剪 (Null Move Pruning)
│       ├── Killer 启发 (最佳走法优先)
│       ├── 走法排序 (吃子 + PST 增量评分)
│       └── 静态搜索 (Quiescence Search)
│
评估函数
├── PST 位置价值表 (Piece-Square Tables)
│   ├── 7 种棋子各有 10×9 的位置权重
│   └── 红/黑方镜像使用
└── 困毙 / 和棋检测
```

核心实现参考象眼引擎 (UCCI) 的子力价值和位置评估表。

## 快速开始

### 方法一：直接打开

```bash
# 下载后双击 elephantfish.html 即可
open elephantfish.html
```

### 方法二：本地服务器（推荐）

```bash
python3 -m http.server 8080
# 浏览器访问 http://localhost:8080/elephantfish.html
```

## 操作说明

| 操作 | 说明 |
|------|------|
| 点击己方棋子 | 选中棋子，显示合法走法 |
| 点击绿色/红色标记 | 移动或吃子 |
| 🔄 新游戏 | 重新开局 |
| ↩️ 悔棋 | 撤销走法（人机模式自动撤回两步） |
| 📍 坐标 | 切换棋盘坐标显示 |
| ⚫/🔴 AI执棋 | 切换 AI 执黑/执红（自动翻转棋盘） |

## 技术细节

- **棋盘表示**：10×9 二维数组，正值红方、负值黑方
- **哈希**：91 字符紧凑编码（含走棋方维度），替代 JSON.stringify
- **搜索优化**：就地 make/unmake 修改棋盘，避免深拷贝
- **转置表**：Map 实现，包含 upper/lower bound 双边界
- **走法生成**：完整中国象棋规则（将帅对脸、蹩马腿、塞象眼等）

## 致谢

- [Elephantfish](https://github.com/bupticybee/elephantfish) — 原版 Python 实现
- [Sunfish](https://github.com/thomasahle/sunfish) — Elephantfish 的灵感来源
- 象眼引擎 (UCCI) — 子力价值和位置评估表参考

## License

MIT