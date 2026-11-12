# Biquge · Catalogue de livres du domaine public

[English](README.md) ｜ [简体中文](README.zh.md) ｜ **Français** ｜ [Deutsch](README.de.md) ｜ [Suomi](README.fi.md) ｜ [日本語](README.ja.md)

**96 220 livres du domaine public, 118 langues, 2 808 551 chapitres** — un jeu de données ouvert qui ne contient que des métadonnées bibliographiques, sans texte intégral. Chaque ouvrage possède sa propre page Markdown : titre, auteur, dynastie, langue, genre, nombre de chapitres et de caractères, bibliothèque source — avec un lien vers la page de lecture.

[Lire en ligne](https://www.bqgmz.top/) ｜ [Catalogue CSV complet](catalog/books.csv) ｜ [Description des champs](DATA.md) ｜ [Sources et licences](LICENSE.md) ｜ [Parcourir par langue](list/lang/) ｜ [Parcourir par source](list/lib/)

![Livres par langue](assets/lang.png)

## Démarrage en 30 secondes

Le dépôt contient 96 000 fichiers : **inutile de le cloner**, récupérez directement le CSV :

```bash
curl -L -o books.csv https://gitee.com/zhanyao668/bqgmz-catalog/raw/master/catalog/books.csv
# Miroir GitHub : https://raw.githubusercontent.com/zhanyao/bqgmz-catalog/master/catalog/books.csv
```

```python
import pandas as pd

df = pd.read_csv("books.csv")          # 96 220 lignes × 11 colonnes
df.nlargest(5, "chars")[["title", "author", "chapters", "chars"]]
df[df.lang == "fr"].nlargest(5, "chapters")[["title", "chapters"]]
```

```bash
# JSONL, adapté au traitement en flux
curl -sL https://gitee.com/zhanyao668/bqgmz-catalog/raw/master/catalog/books.jsonl \
  | jq -r 'select(.lang=="fr") | [.title,.author,.chapters] | @tsv' | head
```

## À quoi ressemble un enregistrement

| id | title | author | dynasty | lang | unit | chapters | chars | libs |
|---|---|---|---|---|---|---|---|---|
| cc0bdf92e204 | 红楼梦 (Le Rêve dans le pavillon rouge) | 曹雪芹 | 清 | zh | 回 | 120 | 729,481 | daizhige;scripta;wenshuoge |
| 910354ce8b29 | 三国演义 (Les Trois Royaumes) | 罗贯中 | 明 | zh | 回 | 120 | 487,893 | daizhige;scripta;wenshuoge |
| 0a1d530e267f | 水浒传 (Au bord de l'eau) | 施耐庵 | 明 | zh | 回 | 120 | 777,108 | daizhige;scripta;wenshuoge |
| 1cb46e3a4782 | War and Peace | Tolstoy, Leo | — | en | 章 | 288 | 2,628,447 | gutenberg_full |
| 04abfdfbd8fe | The Adventures of Sherlock Holmes | Doyle, Arthur Conan | — | en | 章 | 12 | 454,708 | gutenberg_full |

Définition des champs : [DATA.md](DATA.md).

## Chiffres clés

| Élément | Valeur |
|---|---|
| Œuvres | 96 220 |
| Chapitres | 2 808 551 |
| Caractères | ~24,57 milliards |
| Langues / pays / genres | 118 / 33 / 8 |
| Sources (œuvres concernées, cumulables) | Project Gutenberg 78 045 · Daizhige 13 754 · Wenshuoge 12 450 · scripta-sinica 9 581 · chinese-poetry 41 |

![Œuvres par genre](assets/units.png)

> Le genre est déduit des marqueurs de chapitres propres à chaque source. Le pipeline v5 traite certains ouvrages entiers comme un seul chapitre : **17 374 œuvres comptent exactement 1 chapitre** (par ex. *Gujin Tushu Jicheng*, *Baopuzi*) — c'est normal, il ne manque pas de données.

## Organisation du dépôt

```
README.md                 anglais (par défaut) ; aussi README.zh / fr / de / fi / ja
b/<xx>/<id>/README.md     une page par livre, xx = deux premiers chiffres hexadécimaux du workId (256 fragments)
list/lang/<code>/         index par langue (→ pays/région)
list/style/<slug>/        index par genre de chapitrage
list/lib/<source>/        index par bibliothèque source
catalog/books.csv         catalogue complet (UTF-8, avec en-tête)
catalog/books.jsonl       mêmes données, un objet JSON par ligne
DATA.md / LICENSE.md      description des champs / sources et licences
```

Les chemins reprennent ceux du site : `b/<xx>/<id>/` correspond à `https://www.bqgmz.top/b/<id>/`.

## Sources et licences

| Source | Licence | Remarques |
|---|---|---|
| Daizhige (daizhige-org) | Domaine public | Corpus chinois classique révisé (2026-10-11) |
| Project Gutenberg | Domaine public (États-Unis) | Bloc de licence conservé |
| chinese-poetry | Domaine public | Poésie chinoise classique |
| scripta-sinica | **CC BY-SA 4.0** | Attribution et partage à l'identique obligatoires |
| Wenshuoge | Domaine public | Corpus chinois classique |

Ce dépôt ne contient que des **métadonnées bibliographiques — aucun texte intégral**. Les données ne sont pas collationnées et comportent du bruit OCR ; elles conviennent à la recherche, aux statistiques et à la constitution de corpus, mais pas comme édition critique. Voir [LICENSE.md](LICENSE.md).

## Citation

```bibtex
@misc{bqgmz_catalog_2026,
  title        = {Biquge · Catalogue de livres du domaine public (96 220 œuvres)},
  author       = {{bqgmz}},
  year         = {2026},
  url          = {https://gitee.com/zhanyao668/bqgmz-catalog},
  note         = {Métadonnées bibliographiques ; textes issus de Daizhige, Project Gutenberg, Wenshuoge, scripta-sinica et chinese-poetry}
}
```
