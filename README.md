# yokogushi-data

3 士業横串アプリ（宅建・司法書士・行政書士）の **公開更新データ** リポジトリ。

アプリ本体（`kashiye-ui/yokogushi`、private）から `raw.githubusercontent.com` 経由で fetch される。
更新するたびにアプリ再リリース不要。

## 構成

```
shihoshoshi/
  prep_schools.json     # 主要予備校の直前期講座ダイジェスト
  exam_schedule.json    # 本試験 日程（願書〜合格発表）
  privacy.html / terms.html
gyousei/
  （同上）
takken/
  data_patch.json       # 出荷データ（お題・論点）の誤り修正パッチ
```

## 更新ルール

- **本試験日程**：年 1 回、法務省発表後（4 月頃）に更新
- **予備校情報**：月 1 程度、主要 4 社の公開情報を要約
- **`data_patch.json`**：誤りが見つかり次第。ストア審査を待たずに反映される

## data_patch.json について

お題の論点文は e-Gov の条文から AI が作成しており、**実測で 4% 前後の誤りが残る**
（宅建・サンプル50件検査 2026-08-05）。全件を人が確認するのは現実的でないため、
**見つかったものをここで直す**運用にしている。

- アプリは起動時に 1 回だけ取得し、バンドル済みデータを書き換える
- 照合は**論点文の完全一致**。並び順（index）には依存しない
- 取得できない／オフラインならバンドルのまま動く（完全オフライン動作は維持）

```jsonc
{
  "version": 1,
  "fix":    [{ "tab": "keywords", "match": "<現在の論点文>",
               "subtopic": "<直した論点文>", "statute_ref": "<直した条文>" }],
  "remove": [{ "tab": "keywords", "match": "<消す論点文>" }]
}
```

**投入前に必ず** アプリ側リポジトリの `1_takken/_data_patch/verify_patch.cjs` を走らせ、
`match` が「ちょうど1件」当たることを確認する（0件＝効かない／2件以上＝巻き添え）。

## 著作権

- 各予備校情報：公式サイトの公開情報を要約引用
- 試験日程：法務省 公開情報（パブリックドメイン）
- アプリ本体側ではバンドル fallback も持つので、本 repo が一時 down してもアプリは動く

## URL 例

```
https://raw.githubusercontent.com/kashiye-ui/yokogushi-data/main/shihoshoshi/prep_schools.json
https://raw.githubusercontent.com/kashiye-ui/yokogushi-data/main/shihoshoshi/exam_schedule.json
```
