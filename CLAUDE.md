# health-app

健康記録 Web アプリ。体重・食事・睡眠・運動・気分を1日単位で記録し、ローカルに保存して可視化する。

公開先: https://mai602.github.io/health-app/

## 構成

- **シングルファイル構成**: `index.html` 1枚に HTML / CSS / JavaScript がすべて含まれる（約2,274行）。フレームワーク・ビルドツール不使用。
- **データ保存**: ブラウザの `localStorage` のみ。サーバー無し。キーは `healthRecords`, `userFoods`, `weightGoal`。
- **デプロイ**: GitHub Pages（`main` ブランチの `/(root)` から自動公開）。`git push` すれば1〜2分で反映される。

## 主要機能

| 機能 | 概要 |
|---|---|
| 記録タブ (`#record`) | 食事・体重・睡眠・運動・気分を入力するフォーム群 |
| 一覧タブ (`#list`) | 過去の記録を日付順に閲覧、フィルタ可能 |
| 食材データベース | `foodDatabase` (index.html:1097-) に主要食材のカロリー・栄養素を内蔵。入力中にサジェスト |
| ユーザー食材 | ユーザーが追加した食材は `userFoods` として localStorage に保存 |
| 栄養バランス計算 | `calculateDayNutrition()` で炭水化物・タンパク質・脂質・食物繊維・各種ビタミンを集計 |
| 運動カロリー計算 | `calculateBurnedCalories()` で運動種目 × 時間 × 体重から消費カロリー算出 |
| 気分相関分析 | 食事・運動などと気分（5段階）の相関を表示 |

## コード上の主な定数・関数の場所

- `foodDatabase` … index.html:1097
- `categoryHints` (食材カテゴリ推定) … index.html:1137
- `mealTypes` (朝/昼/晩/おやつ) … index.html:1266
- `exerciseTypes` (運動種目とMETs) … index.html:1284
- `nutrients` / `nutrientFoods` / `categoryProfile` (栄養素関連) … index.html:1321-1345
- `records` 等のグローバル状態 … index.html:1431-1437

## 編集・公開フロー

```bash
cd ~/Desktop/health-app
# index.html を編集
git add index.html
git commit -m "変更内容の説明"
git push
```

push から1〜2分で公開サイトに反映される。

## 注意事項

- データはブラウザごとにローカル保存 → 別の端末・別のブラウザでは記録は引き継がれない
- HTTPS 必須（GitHub Pages 設定で `Enforce HTTPS` 有効）
- `.gitignore` で `.DS_Store` のみ除外
