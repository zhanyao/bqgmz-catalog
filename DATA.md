# 数据字段

`catalog/books.csv`（UTF-8，带表头）与 `catalog/books.jsonl`（每行一个 JSON 对象）字段一致。

| 字段 | 类型 | 说明 |
|---|---|---|
| `id` | string | 站点内作品 ID（12 位十六进制） |
| `title` | string | 书名，保留原文，未做繁简归一；Gutenberg 撞名时带 `（#书号）` 后缀 |
| `author` | string | 作者；空串表示原文未署名 |
| `dynasty` | string | 朝代，仅从原始文件名标注中提取；取不到为空串 |
| `lang` | string | 语种代码（`zh` / `en` / `fr` …）；`other` 表示未判定 |
| `country` | string | 由国家/地区推导表得到的展示名（如 `英美`、`中国`） |
| `unit` | string | 章节单位（回 / 卷 / 章 / 题 / 段 / 年 …） |
| `chapters` | int | 章节数 |
| `chars` | int | 正文字数；多来源副本时取**实际阅读本**，不是副本相加 |
| `libs` | string | 来源库，`;` 分隔（`daizhige` / `scripta` / `gutenberg_full` / `poetry`） |
| `url` | string | 站内书籍页绝对地址 |

统计口径与生成时间见根目录 `README.md`。

> 语种由国家/地区推导是**近似**：英语作品横跨英美，故标 `英美`；拉丁语标 `古罗马`。
