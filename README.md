# inou-labs.github.io

inou! プロジェクトの公式サイト。<https://inou-labs.github.io/>

素の HTML + CSS で構成されています。ビルドも `node_modules` も不要です。

## 構成

```
/
├── index.html          トップ
├── about.html          プロジェクト概要・体制
├── products.html       inou! PXRD ／ inou! OS 構想
├── research.html       コア技術・研究業績・研究室への動線
├── contact.html        お問い合わせ
├── assets/
│   ├── style.css       全ページ共通のスタイルシート
│   ├── favicon.svg
│   └── img/            図版・写真
└── .nojekyll
```

## ローカルで確認する

```sh
python3 -m http.server 8080
```

<http://localhost:8080/> を開きます。相対パスではなくルート相対パス（`/assets/...`）を
使っているため、ファイルを直接 `open` するのではなくサーバー経由で確認してください。

## 公開

`main` ブランチへの push がそのまま公開されます
（Settings → Pages → Deploy from a branch → `main` / `root`）。
ビルドステップがないため GitHub Actions は使っていません。

## 編集するときの注意

### ヘッダーとフッターは各ページにベタ書き

インクルード機構がないため、ナビゲーションは5ページすべてに複製されています。
リンクを追加・変更するときは **5ファイルすべて**を直してください。

ページごとの差分は、現在のページを示す `aria-current="page"` の位置だけです。

### 画像

`assets/img/` は合計 1MB 未満に保っています。追加するときは `sips` でリサイズします。

```sh
sips -Z 1600 -s format jpeg -s formatOptions 78 元画像.png --out assets/img/名前.jpg
```

### 掲載しない情報

ピッチ資料には、公開サイトに載せてはいけない情報が含まれています。
資料から文言を持ってくるときは以下を除外してください。

- 個人の携帯電話番号
- 「CEO候補」「CTO候補」など、法人未設立段階の肩書
- 未発表のメンバーの氏名・前職企業名
- 競合他社を名指しするポジショニング比較
- 市場規模・シェアの社内試算
- 工数・人件費の社内試算
- 課金モデルの具体的な条件

掲載してよい定量値は、査読付き論文に紐づくものに限っています
（試料量 80 mg / 300 mg、サンプル間相対標準偏差 2.7% / 9.3% など）。

公開前に確認するには:

```sh
grep -riE '080-|候補|億円|万円|従量課金' *.html
```

### 他社商標

`hero.jpg` と埋め込み動画には装置メーカーのロゴが写っています。
共同開発や推奨と誤読されないよう、キャプションで「PXRD装置は装置メーカー製」である旨を
必ず明記してください。

## 動画

`products.html` の実演動画は、小野研究室の YouTube チャンネルから埋め込んでいます。
動画ファイルはリポジトリに置いていません（元ファイルは 4.8MB あり、サイト全体より重い）。

| 項目 | 値 |
| --- | --- |
| 動画 ID | `udCIev6Gc4U` |
| チャンネル | [Osaka Univ. Ono Lab](https://www.youtube.com/@onolab_osaka) |
| 埋め込み元 | `youtube-nocookie.com`（`loading="lazy"`） |

差し替えるときは `products.html` の `iframe` の `src` と `title` を直します。
動画が非公開になると埋め込みが空になるため、公開範囲の変更時は要確認。

## 外部リンク

小野研究室の公式サイトへは3ページからリンクしています。
URL が変わったときは以下をまとめて直してください。

| リンク先 | 使用ページ |
| --- | --- |
| `https://nano-ap.eng.osaka-u.ac.jp/` | `contact.html` / `research.html` |
| `https://nano-ap.eng.osaka-u.ac.jp/member/` | `contact.html` / `about.html` |
| `https://nano-ap.eng.osaka-u.ac.jp/access/` | `contact.html` |

外部リンクには `target="_blank"` と `rel="noopener noreferrer"` を必ず付けます。

## 未確定事項

- [ ] `inou!` の正式ロゴ（現在は CSS のロゴタイプ、favicon は暫定）
- [ ] 独自ドメイン（`CNAME` 1行 + DNS 設定で後から移行可能）
