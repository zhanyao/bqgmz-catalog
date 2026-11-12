# 笔趣阁 · 公版书籍书目数据集

[English](README.md) ｜ **简体中文** ｜ [Français](README.fr.md) ｜ [Deutsch](README.de.md) ｜ [Suomi](README.fi.md) ｜ [日本語](README.ja.md)

**96,220 部公有领域书籍、118 个语种、2,808,551 章** —— 一个只有书目与结构、不含正文的开放数据集。每部书一个 Markdown 页，给出书名、作者、朝代、语种、体例、章数、字数与来源库，并回链在线阅读页。

[在线阅读](https://www.bqgmz.top/) ｜ [全量书目 CSV](catalog/books.csv) ｜ [字段说明](DATA.md) ｜ [来源与许可](LICENSE.md) ｜ [按语种浏览](list/lang/) ｜ [按来源库浏览](list/lib/)

![按语种分布](assets/lang.png)

## 30 秒用起来

仓库有 9.6 万个文件，**不用 clone 也能直接取数据**：

```bash
curl -L -o books.csv https://gitee.com/zhanyao668/bqgmz-catalog/raw/master/catalog/books.csv
# GitHub 镜像：https://raw.githubusercontent.com/zhanyao/bqgmz-catalog/master/catalog/books.csv
```

```python
import pandas as pd

df = pd.read_csv("books.csv")          # 96,220 行 × 11 列
df.nlargest(5, "chars")[["title", "author", "chapters", "chars"]]
df[df.lang == "zh"].groupby("dynasty").size().sort_values(ascending=False).head(10)
```

```bash
# JSONL 适合流式处理
curl -sL https://gitee.com/zhanyao668/bqgmz-catalog/raw/master/catalog/books.jsonl \
  | jq -r 'select(.lang=="zh") | [.title,.author,.chapters] | @tsv' | head
```

## 数据长什么样

| id | title | author | dynasty | lang | unit | chapters | chars | libs |
|---|---|---|---|---|---|---|---|---|
| cc0bdf92e204 | 红楼梦 | 曹雪芹 | 清 | zh | 回 | 120 | 729,481 | daizhige;scripta;wenshuoge |
| 910354ce8b29 | 三国演义 | 罗贯中 | 明 | zh | 回 | 120 | 487,893 | daizhige;scripta;wenshuoge |
| 0a1d530e267f | 水浒传 | 施耐庵 | 明 | zh | 回 | 120 | 777,108 | daizhige;scripta;wenshuoge |
| 1cb46e3a4782 | War and Peace | Tolstoy, Leo | — | en | 章 | 288 | 2,628,447 | gutenberg_full |
| 04abfdfbd8fe | The Adventures of Sherlock Holmes | Doyle, Arthur Conan | — | en | 章 | 12 | 454,708 | gutenberg_full |

字段定义见 [DATA.md](DATA.md)。

## 规模

| 项 | 数值 |
|---|---|
| 作品 | 96,220 部 |
| 章节 | 2,808,551 章 |
| 正文字数 | 约 245.7 亿字 |
| 语种 / 国家地区 / 体例 | 118 / 33 / 8 |
| 来源库（涉及书目，可重叠） | Project Gutenberg 78,045 · 殆知阁 13,754 · 文硕阁 12,450 · scripta-sinica 9,581 · chinese-poetry 41 |

![按章节体例分布](assets/units.png)

> 体例按各来源的分章标记自动判定；v5 管线会把一部分整本书当作单章处理，因此 **17,374 部作品的章节数为 1**（如《古今图书集成》《抱朴子》），属正常表现。

## 仓库结构

```
README.md                 英文（默认）；另有 README.zh / fr / de / fi / ja
b/<xx>/<id>/README.md     单书页，xx = workId 前两位，共 256 片
list/lang/<语种>/          按语种（→ 国家/地区）
list/style/<体例>/         按章节体例
list/lib/<来源库>/         按来源库
catalog/books.csv         全量书目（UTF-8，带表头）
catalog/books.jsonl       同上，每行一个 JSON 对象
DATA.md / LICENSE.md      字段说明 / 来源与许可
```

路径与站点一一对应：`b/<xx>/<id>/` 对应 `https://www.bqgmz.top/b/<id>/`。

## 来源与许可

| 来源 | 许可 | 说明 |
|---|---|---|
| 殆知阁（daizhige-org） | 公有领域 | 2026-10-11 修订版古籍 |
| Project Gutenberg | 公有领域（美国法） | 保留其许可声明 |
| chinese-poetry | 公有领域 | 诗词总集 |
| scripta-sinica | **CC BY-SA 4.0** | 引用须署名并以相同方式共享 |
| 文硕阁 | 公有领域 | 古籍原典 |

本仓库**只含书目元数据，不含任何作品正文**。数据未经校勘，含 OCR 噪声，适合检索、统计与语料构建，不适合作版本校勘或学术引用底本。详见 [LICENSE.md](LICENSE.md)。

## 引用

```bibtex
@misc{bqgmz_catalog_2026,
  title        = {笔趣阁 · 公版书籍书目数据集（96,220 部）},
  author       = {{bqgmz}},
  year         = {2026},
  url          = {https://gitee.com/zhanyao668/bqgmz-catalog},
  note         = {书目元数据；正文来自殆知阁、Project Gutenberg、文硕阁、scripta-sinica、chinese-poetry}
}
```
