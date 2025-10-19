# 🍽️ にこもぐ（NikoMogu）

小規模保育園向けの「給食・アレルギー管理アプリ」です。  
ハッカソンで6名チーム（フロント2名 / バックエンド3名 / インフラ1名）で開発しました。  
私は主に **バックエンド・DB設計・認証機能** を担当しました。

---

## 🎯 コンセプト

保育園での「給食情報・アレルギー対応・保護者連絡」を  
**一つのアプリで簡単に管理できる仕組みを作る** ことを目的としています。

- 保育士が献立・食材アレルギーを登録  
- 保護者がアプリで毎日の給食やアレルギー対応を確認  
- 園と保護者がチャットで連絡を取り合える

---

## 👶 ペルソナ
| 属性 | 内容 |
|------|------|
| 年齢 | 60代 |
| 職業 | 小規模保育園の園長 |
| 園児数 | 約20名 |
| 課題 | アレルギー対応食や献立の共有が紙ベースで煩雑 |
| ニーズ | 給食内容・アレルギー情報をデジタル化し、保護者と共有したい |

---

## 🧩 主な機能

| 機能カテゴリ | 内容 |
|---------------|------|
| 🔐 認証機能 | ユーザー登録 / ログイン / JWTによる認証処理 |
| 👶 園児管理 | 園児情報・クラス・アレルギー情報の登録・更新 |
| 🍱 給食管理 | 献立登録 / アレルギー食材との紐付け / メニュー一覧表示 |
| 💬 チャット機能 | 保護者と園のメッセージ送受信 |
| 🧠 管理機能 | 管理者によるユーザー・園児・メニュー管理 |
| 🧾 PDF対応 | アレルギー票をPDFで添付・表示可能 |

---

## 👨‍💻 担当部分（HARU）

| 項目 | 内容 |
|------|------|
| フレームワーク | Flask + SQLAlchemy |
| DB設計 | ER図作成、テーブル構造設計（10テーブル構成） |
| 認証処理 | JWTによるセッションレス認証を実装 |
| CRUD処理 | ユーザー・園児・メニュー・チャット機能を担当 |
| エラー処理 | バリデーション・例外対応・戻り値の統一 |
| コード整備 | モジュール分割 / コードレビュー / 可読性改善 |

---

## 🗺 ER図
![ER Diagram](docs/er.png)

- Users 1:N Children  
- Children M:N Allergens（中間テーブル：ChildrenAllergens）  
- Meals M:N Allergens（中間テーブル：MealAllergens）  
- Menus 1:1..N Meals（meal_id1〜4構成）  
- Channels 1:N Messages（チャット管理）

---

## 🧱 使用技術

| 分類 | 使用技術 |
|------|-----------|
| 言語 | Python 3.x |
| フレームワーク | Flask |
| データベース | MySQL |
| ORM | SQLAlchemy |
| 認証 | JWT, Flask-Login |
| テンプレート | Jinja2 |
| フロント | HTML, CSS, JavaScript |
| コンテナ環境 | Docker, docker-compose |
| バージョン管理 | Git, GitHub |

---

## 📁 ディレクトリ構成

```
.
├── ChatApp              # Jチーム開発ディレクトリ
│   ├── __init__.py
│   ├── app.py
│   ├── models.py
│   ├── static   # 静的ファイル用ディレクトリ
│   |   ├── css　 # cssを格納
|   |   ├── img　 # 画像ファイルを格納
|   |   └── js    # javascriptを格納
│   ├── templates       # Template(HTML)用ディレクトリ
|   |   ├── common     #管理者、ユーザーの共通画面を格納
|   |   ├── registration　# 新規会員登録用ディレクトリ
|   |   ├── management　# 管理用ディレクトリ
|   |   └── user　　　　# ユーザー用ディレクトリ
|   | 
│   └── util
├── Docker
│   ├── Flask
│   │   └── Dockerfile # Flask(Python)用Dockerファイル
│   └── MySQL
│       ├── Dockerfile  # MySQL用Dockerファイル
│       ├── init.sql    # MySQL初期設定ファイル
│       └── my.cnf
├── docker-compose.yml   # Docker-composeファイル
└── requirements.txt     # 使用モジュール記述ファイル
```

---

## ⚙️ セットアップ

```bash
# クローン
git clone https://github.com/devharu-49/nikomogu.git
cd nikomogu

# 依存パッケージをインストール
pip install -r requirements.txt

# 環境変数（例）
export FLASK_APP=ChatApp/app.py
export FLASK_ENV=development

# アプリ起動
flask run
