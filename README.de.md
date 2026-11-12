# Biquge · Katalog gemeinfreier Bücher

[English](README.md) ｜ [简体中文](README.zh.md) ｜ [Français](README.fr.md) ｜ **Deutsch** ｜ [Suomi](README.fi.md) ｜ [日本語](README.ja.md)

**96.220 gemeinfreie Bücher, 118 Sprachen, 2.808.551 Kapitel** — ein offener Datensatz mit ausschließlich bibliografischen Metadaten, kein Volltext. Jedes Buch hat eine eigene Markdown-Seite mit Titel, Autor, Dynastie, Sprache, Genre, Kapitel- und Zeichenzahl sowie Quellbibliothek und verlinkt auf die Leseseite.

[Online lesen](https://www.bqgmz.top/) ｜ [Vollständiger Katalog (CSV)](catalog/books.csv) ｜ [Feldbeschreibung](DATA.md) ｜ [Quellen und Lizenzen](LICENSE.md) ｜ [Nach Sprache durchsuchen](list/lang/) ｜ [Nach Quelle durchsuchen](list/lib/)

![Bücher nach Sprache](assets/lang.png)

## Schnellstart in 30 Sekunden

Das Repository enthält 96.000 Dateien — **kein Klonen nötig**, laden Sie die CSV direkt:

```bash
curl -L -o books.csv https://gitee.com/zhanyao668/bqgmz-catalog/raw/master/catalog/books.csv
# GitHub-Spiegel: https://raw.githubusercontent.com/zhanyao/bqgmz-catalog/master/catalog/books.csv
```

```python
import pandas as pd

df = pd.read_csv("books.csv")          # 96.220 Zeilen × 11 Spalten
df.nlargest(5, "chars")[["title", "author", "chapters", "chars"]]
df[df.lang == "de"].nlargest(5, "chapters")[["title", "chapters"]]
```

```bash
# JSONL für Streaming
curl -sL https://gitee.com/zhanyao668/bqgmz-catalog/raw/master/catalog/books.jsonl \
  | jq -r 'select(.lang=="de") | [.title,.author,.chapters] | @tsv' | head
```

## So sieht ein Datensatz aus

| id | title | author | dynasty | lang | unit | chapters | chars | libs |
|---|---|---|---|---|---|---|---|---|
| cc0bdf92e204 | 红楼梦 (Der Traum der roten Kammer) | 曹雪芹 | 清 | zh | 回 | 120 | 729,481 | daizhige;scripta;wenshuoge |
| 910354ce8b29 | 三国演义 (Die Geschichte der Drei Reiche) | 罗贯中 | 明 | zh | 回 | 120 | 487,893 | daizhige;scripta;wenshuoge |
| 0a1d530e267f | 水浒传 (Die Räuber vom Liang-Schan-Moor) | 施耐庵 | 明 | zh | 回 | 120 | 777,108 | daizhige;scripta;wenshuoge |
| 1cb46e3a4782 | War and Peace | Tolstoy, Leo | — | en | 章 | 288 | 2,628,447 | gutenberg_full |
| 04abfdfbd8fe | The Adventures of Sherlock Holmes | Doyle, Arthur Conan | — | en | 章 | 12 | 454,708 | gutenberg_full |

Felddefinitionen: [DATA.md](DATA.md).

## Kennzahlen

| Position | Wert |
|---|---|
| Werke | 96.220 |
| Kapitel | 2.808.551 |
| Zeichen | ~24,57 Milliarden |
| Sprachen / Länder / Genres | 118 / 33 / 8 |
| Quellen (betroffene Werke, überschneidend) | Project Gutenberg 78.045 · Daizhige 13.754 · Wenshuoge 12.450 · scripta-sinica 9.581 · chinese-poetry 41 |

![Werke nach Genre](assets/units.png)

> Das Genre wird aus den Kapitelmarkierungen der jeweiligen Quelle abgeleitet. Die v5-Pipeline behandelt manche Bücher als ein einziges Kapitel: **17.374 Werke haben genau 1 Kapitel** (z. B. *Gujin Tushu Jicheng*, *Baopuzi*) — das ist beabsichtigt, es fehlen keine Daten.

## Aufbau des Repositories

```
README.md                 Englisch (Standard); außerdem README.zh / fr / de / fi / ja
b/<xx>/<id>/README.md     eine Seite pro Buch, xx = erste zwei Hex-Ziffern der workId (256 Fragmente)
list/lang/<code>/         Index nach Sprache (→ Land/Region)
list/style/<slug>/        Index nach Kapitelgenre
list/lib/<source>/        Index nach Quellbibliothek
catalog/books.csv         vollständiger Katalog (UTF-8, mit Kopfzeile)
catalog/books.jsonl       gleiche Daten, ein JSON-Objekt pro Zeile
DATA.md / LICENSE.md      Felddefinitionen / Quellen und Lizenzen
```

Die Pfade entsprechen der Website: `b/<xx>/<id>/` gehört zu `https://www.bqgmz.top/b/<id>/`.

## Quellen und Lizenzen

| Quelle | Lizenz | Hinweis |
|---|---|---|
| Daizhige (daizhige-org) | Gemeinfrei | Überarbeitetes klassisches Korpus (2026-10-11) |
| Project Gutenberg | Gemeinfrei (USA) | Lizenzblock bleibt erhalten |
| chinese-poetry | Gemeinfrei | Klassische chinesische Dichtung |
| scripta-sinica | **CC BY-SA 4.0** | Namensnennung und Weitergabe unter gleichen Bedingungen |
| Wenshuoge | Gemeinfrei | Klassisches Korpus |

Dieses Repository enthält **nur bibliografische Metadaten — keinen Volltext**. Die Daten sind nicht kollationiert und enthalten OCR-Rauschen; sie eignen sich für Suche, Statistik und Korpusaufbau, nicht als kritische Edition. Siehe [LICENSE.md](LICENSE.md).

## Zitierung

```bibtex
@misc{bqgmz_catalog_2026,
  title        = {Biquge · Katalog gemeinfreier Bücher (96.220 Werke)},
  author       = {{bqgmz}},
  year         = {2026},
  url          = {https://gitee.com/zhanyao668/bqgmz-catalog},
  note         = {Bibliografische Metadaten; Texte aus Daizhige, Project Gutenberg, Wenshuoge, scripta-sinica und chinese-poetry}
}
```
