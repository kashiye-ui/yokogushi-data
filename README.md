# yokogushi-data

3 士業横串アプリ（宅建・司法書士・行政書士）の **公開更新データ** リポジトリ。

アプリ本体（`kashiye-ui/yokogushi`、private）から `raw.githubusercontent.com` 経由で fetch される。
更新するたびにアプリ再リリース不要。

## 構成

```
shihoshoshi/
  prep_schools.json     # 主要予備校の直前期講座ダイジェスト
  exam_schedule.json    # 本試験 日程（願書〜合格発表）
takken/                 # （将来）
  ...
gyousei/                # （将来）
  ...
```

## 更新ルール

- **本試験日程**：年 1 回、法務省発表後（4 月頃）に更新
- **予備校情報**：月 1 程度、主要 4 社の公開情報を要約

## 著作権

- 各予備校情報：公式サイトの公開情報を要約引用
- 試験日程：法務省 公開情報（パブリックドメイン）
- アプリ本体側ではバンドル fallback も持つので、本 repo が一時 down してもアプリは動く

## URL 例

```
https://raw.githubusercontent.com/kashiye-ui/yokogushi-data/main/shihoshoshi/prep_schools.json
https://raw.githubusercontent.com/kashiye-ui/yokogushi-data/main/shihoshoshi/exam_schedule.json
```
