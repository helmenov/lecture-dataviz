# Pythonによるデータ可視化 ― Quarto Book版

講義資料（スライド版 `lecture-dataviz/`）をもとにした、Quarto の book プロジェクトです。
章立てはスライド版と同じ全8コマ＋付録で、コードはレンダリング時に実行され、結果とグラフが本の中に埋め込まれます。

- 公開先の想定：https://github.com/helmenov/lecture-dataviz
- 受講者向けデータ：`data/` フォルダ（`data.zip` はフォルダを固めたもの。データ更新時は `zip -r data.zip data` で作り直す）

## ビルド方法（webbook と Reveal.js スライドの両方が作れます）

同じ `.qmd` ソースから、2種類の出力を生成します。

```bash
# webbook（プロジェクト直下で）
quarto render
# → _book/ にHTMLブック

# Reveal.js スライド（slides/ サブプロジェクトで）
cd slides
quarto render
# → slides/_slides/ に session1〜8 のスライド
（配布用 zip には _slides の生成物は含めていません。上記コマンドで生成してください）
```

- `slides/` の中の `.qmd` は、直下の原稿への**シンボリックリンク**です。編集は直下の `.qmd` で行えば、両方の出力に反映されます（`assets` と `data` もリンク）
- スライドは各コマ1デッキで、`##` と `###` 見出しが1枚のスライドになります（`slide-level: 3`、### は縦方向のスライド）。スライド内スクロールは使わず、全体の拡大縮小で収める方針です
- スライド側の見た目の調整は `slides/custom.css`（文字・コード・図の大きさ）で行っています。内容が多い節は、原稿側に `---`（水平線）でスライドの区切りを入れてあります（book では水平線として表示されます）
- 各章の冒頭の「進め方」段落は、book でのみ表示されます（スライドのタイトルをすっきりさせるため `unless-format="revealjs"` で出し分け）
- 実行環境：Python（pandas / matplotlib / matplotlib-fontja が入った環境）。
  別の venv を使う場合は `QUARTO_PYTHON=/path/to/python quarto render`

## 構成

- `_quarto.yml` … book の設定（タイトル・著者・章立て）
- `index.qmd` … はじめに（講義概要・日程 2026年11月14日（土）・15日（日））
- `session1.qmd`〜`session8.qmd` … 各コマの章
- `appendix_terms.qmd` … 用語のミニ辞典
- `appendix_trouble.qmd` … 困ったときの対処表
- `assets/` … 例図・Thonnyの画面写真
- `data/` … 実習データ

※ 講師用の解答例とテスト実施ガイドは、プロジェクト内の `teacher/` フォルダに**別の book** として置いてあります（受講者向けの本には含まれません）。
`cd teacher && quarto render` で `_teacher_book/` に生成されます。元のファイルはスライド版（`lecture-dataviz/code/answers/` と `test_guide.md`）です。
