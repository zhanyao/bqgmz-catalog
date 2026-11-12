# Biquge · パブリックドメイン書籍目録

[English](README.md) ｜ [简体中文](README.zh.md) ｜ [Français](README.fr.md) ｜ [Deutsch](README.de.md) ｜ [Suomi](README.fi.md) ｜ **日本語**

**96,220 冊のパブリックドメイン書籍、118 言語、2,808,551 章** — 本文を含まず、書誌メタデータのみを収録したオープンデータセットです。各書籍には Markdown ページがあり、書名・著者・王朝・言語・体裁・章数・字数・出典を記載し、閲覧ページへリンクしています。

[オンラインで読む](https://www.bqgmz.top/) ｜ [全目録 CSV](catalog/books.csv) ｜ [フィールド定義](DATA.md) ｜ [出典とライセンス](LICENSE.md) ｜ [言語別に見る](list/lang/) ｜ [出典別に見る](list/lib/)

![言語別の分布](assets/lang.png)

## 30 秒で使い始める

リポジトリには 9.6 万ファイルあるため、**clone は不要**です。CSV を直接取得してください:

```bash
curl -L -o books.csv https://gitee.com/zhanyao668/bqgmz-catalog/raw/master/catalog/books.csv
# GitHub ミラー: https://raw.githubusercontent.com/zhanyao/bqgmz-catalog/master/catalog/books.csv
```

```python
import pandas as pd

df = pd.read_csv("books.csv")          # 96,220 行 × 11 列
df.nlargest(5, "chars")[["title", "author", "chapters", "chars"]]
df[df.lang == "ja"].nlargest(5, "chapters")[["title", "chapters"]]
```

```bash
# JSONL はストリーム処理向け
curl -sL https://gitee.com/zhanyao668/bqgmz-catalog/raw/master/catalog/books.jsonl \
  | jq -r 'select(.lang=="ja") | [.title,.author,.chapters] | @tsv' | head
```

## レコードの例

| id | title | author | dynasty | lang | unit | chapters | chars | libs |
|---|---|---|---|---|---|---|---|---|
| cc0bdf92e204 | 红楼梦（紅楼夢） | 曹雪芹 | 清 | zh | 回 | 120 | 729,481 | daizhige;scripta;wenshuoge |
| 910354ce8b29 | 三国演义（三国志演義） | 罗贯中 | 明 | zh | 回 | 120 | 487,893 | daizhige;scripta;wenshuoge |
| 0a1d530e267f | 水浒传（水滸伝） | 施耐庵 | 明 | zh | 回 | 120 | 777,108 | daizhige;scripta;wenshuoge |
| 1cb46e3a4782 | War and Peace | Tolstoy, Leo | — | en | 章 | 288 | 2,628,447 | gutenberg_full |
| 04abfdfbd8fe | The Adventures of Sherlock Holmes | Doyle, Arthur Conan | — | en | 章 | 12 | 454,708 | gutenberg_full |

フィールド定義は [DATA.md](DATA.md) を参照してください。

## 規模

| 項目 | 値 |
|---|---|
| 作品数 | 96,220 |
| 章数 | 2,808,551 |
| 字数 | 約 245.7 億字 |
| 言語 / 国・地域 / 体裁 | 118 / 33 / 8 |
| 出典（重複あり） | Project Gutenberg 78,045 · 殆知閣 13,754 · 文碩閣 12,450 · scripta-sinica 9,581 · chinese-poetry 41 |

![体裁別の分布](assets/units.png)

> 体裁は各出典の章立て記号から自動判定しています。v5 パイプラインでは一部の書物を 1 章として扱うため、**17,374 作品が章数 1** になっています（例:『古今図書集成』『抱朴子』）。データ欠落ではなく仕様です。

## リポジトリ構成

```
README.md                 英語（デフォルト）。ほかに README.zh / fr / de / fi / ja
b/<xx>/<id>/README.md     書籍ごとのページ。xx は workId の先頭 2 桁の 16 進数（256 分割）
list/lang/<code>/         言語別インデックス（→ 国・地域）
list/style/<slug>/        体裁別インデックス
list/lib/<source>/        出典別インデックス
catalog/books.csv         全目録（UTF-8、ヘッダー付き）
catalog/books.jsonl       同じ内容を 1 行 1 JSON で
DATA.md / LICENSE.md      フィールド定義 / 出典とライセンス
```

パスはサイトと対応しています: `b/<xx>/<id>/` は `https://www.bqgmz.top/b/<id>/` に対応します。

## 出典とライセンス

| 出典 | ライセンス | 備考 |
|---|---|---|
| 殆知閣（daizhige-org） | パブリックドメイン | 2026-10-11 改訂版の漢籍 |
| Project Gutenberg | パブリックドメイン（米国法） | ライセンス表示を保持 |
| chinese-poetry | パブリックドメイン | 漢詩総集 |
| scripta-sinica | **CC BY-SA 4.0** | 出典表示と同一条件での共有が必要 |
| 文碩閣 | パブリックドメイン | 漢籍 |

本リポジトリは**書誌メタデータのみで、本文は一切含みません**。データは校勘されておらず OCR ノイズを含みます。検索・統計・コーパス構築には適しますが、版本校勘や学術引用の底本には適しません。詳細は [LICENSE.md](LICENSE.md) を参照してください。

## 引用

```bibtex
@misc{bqgmz_catalog_2026,
  title        = {Biquge · パブリックドメイン書籍目録（96,220 作品）},
  author       = {{bqgmz}},
  year         = {2026},
  url          = {https://gitee.com/zhanyao668/bqgmz-catalog},
  note         = {書誌メタデータ。本文は殆知閣、Project Gutenberg、文碩閣、scripta-sinica、chinese-poetry より}
}
```
