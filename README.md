# デクさん観覧車 - Cafe Information Page

サイバーパンク×サイケデリックスタイルのカフェ・バー情報サイト

## 🚀 デプロイ方法（GitHub + Render）

### 📋 必要なもの

- GitHubアカウント
- Renderアカウント（無料プランでOK）
- Googleアカウント（GAS用）

---

## ステップ1: GitHubリポジトリの作成

### 1-1. 新規リポジトリを作成

1. [GitHub](https://github.com/) にログイン
2. 右上の「+」→「New repository」をクリック
3. Repository name: `cafe-deku-kanransha`（任意）
4. Public または Private を選択
5. 「Create repository」をクリック

### 1-2. ファイルをプッシュ

```bash
cd "/Users/y-abe/Downloads/Cafe Information Page/build/testhtml"

# Gitの初期化
git init

# ファイルを追加
git add index.html .gitignore README.md

# コミット
git commit -m "Initial commit: デクさん観覧車サイト"

# リモートリポジトリを追加
git remote add origin https://github.com/YOUR_USERNAME/cafe-deku-kanransha.git

# プッシュ
git branch -M main
git push -u origin main
```

**注意**: `YOUR_USERNAME`は自分のGitHubユーザー名に置き換えてください。

---

## ステップ2: Renderでデプロイ

### 2-1. 新規サイトを作成

1. [Render](https://render.com/) にログイン
2. ダッシュボードで「New +」→「Static Site」をクリック
3. GitHubリポジトリを接続（初回は認証が必要）
4. 作成したリポジトリ `cafe-deku-kanransha` を選択

### 2-2. 設定

以下の設定を入力：

- **Name**: `deku-kanransha`（任意）
- **Branch**: `main`
- **Build Command**: （空白のまま）
- **Publish Directory**: `.`

「Create Static Site」をクリック

### 2-3. デプロイ完了

数分でデプロイが完了し、URLが発行されます：
```
https://deku-kanransha.onrender.com
```

---

## ステップ3: Google Apps Script（予約API）のセットアップ

### 3-1. GASプロジェクトを作成

1. [Google Apps Script](https://script.google.com/) にアクセス
2. 「新しいプロジェクト」をクリック
3. プロジェクト名を「デクさん観覧車API」に変更

### 3-2. Code.gsをコピー

1. ローカルの `Code.gs` ファイルを開く
2. 内容を全てコピー
3. GASエディタの「コード.gs」に貼り付け
4. 「保存」をクリック

### 3-3. ウェブアプリとしてデプロイ

1. 右上の「デプロイ」→「新しいデプロイ」
2. 「種類の選択」→⚙️アイコン→「ウェブアプリ」
3. 設定：
   - **説明**: v1
   - **次のユーザーとして実行**: 自分
   - **アクセスできるユーザー**: 全員
4. 「デプロイ」をクリック
5. 権限を承認
6. **ウェブアプリのURL**をコピー
   ```
   https://script.google.com/macros/s/ABC...XYZ/exec
   ```

---

## ステップ4: GAS URLをサイトに設定

### 4-1. index.htmlを編集

ローカルの `index.html` の**7453行目**付近を編集：

```javascript
// 変更前
const gasApiUrl = "https://script.google.com/macros/s/YOUR_GAS_DEPLOYMENT_ID/exec";

// 変更後（ステップ3-3でコピーしたURLを貼り付け）
const gasApiUrl = "https://script.google.com/macros/s/ABC...XYZ/exec";
```

### 4-2. GitHubにプッシュ

```bash
git add index.html
git commit -m "Update GAS API URL"
git push origin main
```

### 4-3. Renderで自動再デプロイ

Renderが自動的に変更を検知して再デプロイします（数分）。

---

## ✅ 完成！

これで全てのセットアップが完了しました。

**サイトURL**: `https://deku-kanransha.onrender.com`（自分のURL）

### 機能確認

1. サイトにアクセス
2. 予約フォームに入力
3. 「予約を確定する」をクリック
4. メールが届くことを確認
   - 店舗: frankenradio@gmail.com
   - お客様: 入力したメールアドレス

---

## 🔧 トラブルシューティング

### 問題: 予約フォームが動作しない

**原因**: GAS URLが正しく設定されていない

**対処**:
1. index.htmlの7453行目のURLを確認
2. GASのURLが正しくコピーされているか確認
3. GitHubにプッシュしたか確認

### 問題: メールが届かない

**原因1**: 迷惑メールフォルダに入っている
→ 迷惑メールフォルダを確認

**原因2**: GASの実行ログでエラーが出ている
→ GASエディタの「実行数」でログを確認

### 問題: Renderのデプロイが失敗する

**原因**: 設定が間違っている
→ Build Commandは空白、Publish Directoryは`.`に設定

---

## 📝 更新方法

### サイト（HTML）の更新

1. ローカルで `index.html` を編集
2. GitHubにプッシュ
```bash
git add index.html
git commit -m "サイト更新"
git push origin main
```
3. Renderが自動的に再デプロイ

### API（GAS）の更新

1. GASエディタで `Code.gs` を編集
2. 「保存」
3. 「デプロイ」→「デプロイを管理」→既存デプロイを編集
4. 「バージョン」を「新バージョン」に変更
5. 「デプロイ」

※URLは変わりません

---

## 🎨 カスタマイズ

### 店舗情報の変更

`index.html` 内の以下の部分を検索して編集：
- 住所: `〒150-0001 東京都渋谷区神宮前3-3-3`
- 電話番号: `03-9876-5432`
- メール: `deku@kanransha.tokyo`
- 営業時間

### メニューの変更

`index.html` 内で以下を検索：
- `specialMenu`
- `cocktailMenu`
- `beerMenu`
- `foodMenu`

### カラースキームの変更

Tailwind CSSのクラスを編集：
- `from-pink-500` → ピンク系
- `to-purple-600` → パープル系
- `to-cyan-500` → シアン系

---

## 📞 サポート

問題が解決しない場合：
1. GASの実行ログを確認
2. ブラウザのコンソール（F12）でエラーを確認
3. GitHub Issuesで報告

---

## 📄 ライセンス

このプロジェクトは個人利用・商用利用ともに自由です。

---

**異次元体験をお届けしましょう！🎡✨**

