# 日程調整アプリ

マトリクス形式（行：参加者、列：日程）の日程・参加可否調整 Web アプリです。  
GitHub Pages で動作し、ビルドステップ不要です。

---

## 機能

- **参加可否のトグル** — セルをクリックするごとに `—（未回答）→ ○ → △ → ×` と切替
- **参加者・日程の追加／削除／並び替え** — 名前のダブルクリックで編集
- **集計行** — 各日程の ○ / △ / × の人数を自動集計
- **URL 共有** — 現在の状態を Base64 エンコードして URL ハッシュに付与。リンクを開くだけで同じ状態を復元
- **JSON 出力 / 読込** — データのバックアップと復元
- **ローカル保存** — LocalStorage に自動保存（ブラウザを閉じても状態が維持される）
- **レスポンシブ** — スマホでも横スクロールで利用可能
- **ダーク / ライトモード** — OS 設定に追従、ヘッダーのボタンで手動切替も可能

---

## ファイル構成

```
/
└── index.html   ← アプリ本体（単一ファイルで完結）
└── README.md    ← このファイル
```

---

## GitHub Pages での公開手順

### 1. リポジトリを作成する

1. [github.com](https://github.com) にログインし、右上の **＋ → New repository** をクリック
2. Repository name を入力（例: `schedule-app`）
3. **Public** を選択
4. **Create repository** をクリック

### 2. ファイルをアップロードする

#### 方法 A：ブラウザから直接アップロード（最も簡単）

1. 作成したリポジトリのページを開く
2. **Add file → Upload files** をクリック
3. `index.html`（と必要なら `README.md`）をドラッグ＆ドロップ
4. **Commit changes** をクリック

#### 方法 B：Git を使う

```bash
git clone https://github.com/あなたのユーザー名/schedule-app.git
cd schedule-app
# index.html をこのフォルダにコピー
git add index.html README.md
git commit -m "Add schedule app"
git push origin main
```

### 3. GitHub Pages を有効にする

1. リポジトリページの **Settings** タブを開く
2. 左サイドバーの **Pages** をクリック
3. **Source** の **Branch** を `main`（または `master`）に設定、フォルダは `/ (root)` のまま
4. **Save** をクリック

数分後、以下の URL でアクセスできます：

```
https://あなたのユーザー名.github.io/schedule-app/
```

---

## データ共有の仕組み

「共有リンクをコピー」ボタンを押すと、現在の状態（参加者・日程・回答）が JSON → URI エンコード → Base64 変換されて URL のハッシュ（`#data=...`）に付与されます。

そのリンクを開くと自動的にデータが復元されます。受け取った側は読み取り専用ではなく、自分の回答も入力できます（入力内容は送信者には届きません。再度「共有リンクをコピー」で状態を更新してください）。

---

## ローカルで確認する

ブラウザで `index.html` を直接開くだけで動作します：

```bash
open index.html        # macOS
start index.html       # Windows
xdg-open index.html    # Linux
```

または Live Server（VS Code 拡張）を使うと、ファイルを保存するたびに自動リロードされます。
