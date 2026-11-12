# Biquge · Public-Domain Book Catalog

**English** ｜ [简体中文](README.zh.md) ｜ [Français](README.fr.md) ｜ [Deutsch](README.de.md) ｜ [Suomi](README.fi.md)

**96,220 public-domain books, 118 languages, 2,808,551 chapters** — an open dataset of bibliographic metadata only (no full text). Every book has its own Markdown page with title, author, dynasty, language, genre, chapter and character counts, and source attribution, linking back to its reading page.

[Read online](https://www.bqgmz.top/) ｜ [Full catalog CSV](catalog/books.csv) ｜ [Field definitions](DATA.md) ｜ [Sources & licensing](LICENSE.md) ｜ [Browse by language](list/lang/) ｜ [Browse by source](list/lib/)

![Books by language](assets/lang.png)

## Quick start

The repository holds 96k files, so there is **no need to clone** — fetch the CSV directly:

```bash
curl -L -o books.csv https://gitee.com/zhanyao668/bqgmz-catalog/raw/master/catalog/books.csv
# GitHub mirror: https://raw.githubusercontent.com/zhanyao/bqgmz-catalog/master/catalog/books.csv
```

```python
import pandas as pd

df = pd.read_csv("books.csv")          # 96,220 rows × 11 columns
df.nlargest(5, "chars")[["title", "author", "chapters", "chars"]]
df[df.lang == "en"].nlargest(5, "chapters")[["title", "chapters"]]
```

```bash
# JSONL for streaming
curl -sL https://gitee.com/zhanyao668/bqgmz-catalog/raw/master/catalog/books.jsonl \
  | jq -r 'select(.lang=="en") | [.title,.author,.chapters] | @tsv' | head
```

## What a record looks like

| id | title | author | dynasty | lang | unit | chapters | chars | libs |
|---|---|---|---|---|---|---|---|---|
| cc0bdf92e204 | 红楼梦 (Dream of the Red Chamber) | 曹雪芹 | 清 | zh | 回 | 120 | 729,481 | daizhige;scripta;wenshuoge |
| 910354ce8b29 | 三国演义 (Romance of the Three Kingdoms) | 罗贯中 | 明 | zh | 回 | 120 | 487,893 | daizhige;scripta;wenshuoge |
| 0a1d530e267f | 水浒传 (Water Margin) | 施耐庵 | 明 | zh | 回 | 120 | 777,108 | daizhige;scripta;wenshuoge |
| 1cb46e3a4782 | War and Peace | Tolstoy, Leo | — | en | 章 | 288 | 2,628,447 | gutenberg_full |
| 04abfdfbd8fe | The Adventures of Sherlock Holmes | Doyle, Arthur Conan | — | en | 章 | 12 | 454,708 | gutenberg_full |

Field definitions: [DATA.md](DATA.md).

## Scale

| Item | Value |
|---|---|
| Works | 96,220 |
| Chapters | 2,808,551 |
| Characters | ~24.57 billion |
| Languages / countries / genres | 118 / 33 / 8 |
| Sources (works involved, overlapping) | Project Gutenberg 78,045 · Daizhige 13,754 · Wenshuoge 12,450 · scripta-sinica 9,581 · chinese-poetry 41 |

![Books by genre](assets/units.png)

> Genre is inferred from each source's own chapter markers. The v5 pipeline treats some whole books as a single chapter, so **17,374 works have exactly 1 chapter** (e.g. *Gujin Tushu Jicheng*, *Baopuzi*) — that is expected, not missing data.

## Repository layout

```
README.md                 English (default), plus README.zh / fr / de / fi
b/<xx>/<id>/README.md     one page per book, xx = first two hex digits of workId (256 shards)
list/lang/<code>/         index by language (→ country/region)
list/style/<slug>/        index by chapter genre
list/lib/<source>/        index by source library
catalog/books.csv         full catalog (UTF-8, with header)
catalog/books.jsonl       same data, one JSON object per line
DATA.md / LICENSE.md      field definitions / sources & licensing
```

Paths mirror the website: `b/<xx>/<id>/` corresponds to `https://www.bqgmz.top/b/<id>/`.

## Sources & licensing

| Source | License | Notes |
|---|---|---|
| Daizhige (daizhige-org) | Public domain | Revised classical Chinese corpus (2026-10-11) |
| Project Gutenberg | Public domain (US) | License block preserved |
| chinese-poetry | Public domain | Classical Chinese poetry |
| scripta-sinica | **CC BY-SA 4.0** | Attribution and share-alike required |
| Wenshuoge | Public domain | Classical Chinese corpus |

This repository contains **bibliographic metadata only — no full text**. The data is not collated and contains OCR noise; it is suitable for search, statistics and corpus building, but not as a critical edition for textual scholarship. See [LICENSE.md](LICENSE.md).

## Citation

```bibtex
@misc{bqgmz_catalog_2026,
  title        = {Biquge · Public-Domain Book Catalog (96,220 works)},
  author       = {{bqgmz}},
  year         = {2026},
  url          = {https://gitee.com/zhanyao668/bqgmz-catalog},
  note         = {Bibliographic metadata; texts from Daizhige, Project Gutenberg, Wenshuoge, scripta-sinica and chinese-poetry}
}
```
