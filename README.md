# MICHIORI サポート兼LP

iOSアプリ **MICHIORI（歩数で世界の名道を旅する）** の紹介ページ（LP）、サポートページ、プライバシーポリシーを公開するためのリポジトリです。アプリ本体のソースコードは含みません。

- トップ（LP＋サポート）： https://michiori.pages.dev/
- プライバシーポリシー： https://michiori.pages.dev/privacy-policy

Cloudflare Pages（プロジェクト `michiori`）が `main` ブランチと連携しており、pushすると自動で配信されます。GitHub Pagesも同じ内容を `https://ryo92ys.github.io/michiori-support/` で配信したままにしてあり、控えとして残しています。

Cloudflare Pagesは拡張子なしのURLを正とし、`/privacy-policy.html` は `/privacy-policy` へ転送します。外部へ知らせるURLは拡張子なしの形を使ってください。

## ファイル

| ファイル | 役割 |
|---|---|
| `index.html` | LP（紹介）とサポート（お問い合わせ・FAQ）を上下に並べた1枚のページ |
| `privacy-policy.html` | プライバシーポリシーの公開版 |
| `style.css` | 3ページ共通のスタイル。前半が既存のサポート・ポリシー用、後半がLP用 |
| `images/` | ルート画像、アプリ画面、OGP画像、アイコン |

## トップページが1枚である理由

App Store Connectに登録済みのサポートURLは `https://michiori.pages.dev/`（ルート）です。ルートを紹介専用にするとサポート情報がその場から消えるため、**LPを上半分、サポートを下半分（`#support`）に置いた1枚**にしています。ページ構成を変えるときは、App Store Connectの登録URLと合わせて判断してください。

## App Storeへの導線

- Smart App Banner：`index.html` の `<meta name="apple-itunes-app" content="app-id=6800734656" />`。iOSのSafariでのみ、ページ上部に帯が出ます。
- ボタン：`https://apps.apple.com/app/id6800734656` を2か所（ヒーローとページ末尾）に置いています。

Apple IDを変えるときは、この3か所をまとめて置き換えてください。

```
grep -n "6800734656" index.html
```

流入はApp Store ConnectのApp Analyticsの **Web Referrer** で見えます。SNSごとに分けて測りたくなったら、Appleのキャンペーンリンク（`?pt=<プロバイダID>&ct=<キャンペーン名>&mt=8`）へ差し替えてください。`ct` だけを付けても集計されません。

## 内容を変えるときに気をつけること

- **プライバシーポリシーの原文**はアプリ本体リポジトリの `docs/privacy-policy.md` です。本文を変えるときは原文と `privacy-policy.html`、最終更新日を同じ作業の中で揃えてください。
- **サポートのFAQ**は、通知の間隔・購入の復元・iCloudでの引き継ぎといった実装の挙動を書いています。アプリの挙動を変えたときは合わせて見直してください。
- **LPの記述**（無料範囲、距離、地点数、価格、対応OS）は、アプリ本体リポジトリの `docs/app-store-listing.md` の掲載文と揃えています。片方だけ直さないでください。東海道の300円は日本のストアでの価格です。
- **画像**はすべてアプリ本体の素材から作った自作の生成物で、第三者の利用条件はかかりません（本体リポジトリの `docs/content-provenance.md`）。作り直すときは本体リポジトリで次を実行します。

```
sips -Z 880 -s format jpeg -s formatOptions 50 WorldRoutes/Resources/Assets.xcassets/Kumano.imageset/kumano.png --out ~/Documents/michiori-support/images/route-kumano.jpg
```

画面写真は `docs/app-store-screenshots/` の元画像を幅660、ルート画像は `Assets.xcassets` の元画像を幅880で書き出しています。OGP画像（`images/ogp.jpg`）は1200×630で、文字は入れていません。
