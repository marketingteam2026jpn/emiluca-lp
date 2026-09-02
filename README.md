# EMILUCA ハーブピーリング 広告用LP

広告（Meta / Google など）から流入させる専用のランディングページ。
既存の公式サイト（emiluca.salon）とは別に運用する。

## 公開URL

| 店舗 | URL |
|---|---|
| 岡山店 | https://marketingteam2026jpn.github.io/emiluca-lp/okayama/ |

## 検索に出さないための設定

このLPは検索結果に出さない前提で作っている。以下の2点で制御している。

1. 全ページの `<head>` に `<meta name="robots" content="noindex, nofollow, noarchive, nosnippet, noimageindex, notranslate">`
2. リポジトリ直下の `robots.txt` に `Disallow: /`

※ `robots.txt` はドメイン直下でしか読まれないため、github.io のサブパスで公開している間は
実効性を持つのは 1 の meta タグのみ。独自ドメインに載せ替えたときは `robots.txt` も効くようになる。
広告のリンク先として使う分には meta noindex で十分。

## ディレクトリ構成

```
/index.html          ルート（/okayama/ へリダイレクト・noindex）
/robots.txt
/assets/             全店共通の画像（FV・メニュー・症例・お客様の声・理由・流れ・ロゴ）
/okayama/index.html  岡山店LP本体
/okayama/shop/       岡山店の店舗写真（外観・施術ルーム・スタッフ）
```

## 他店舗に展開するとき

`okayama/` をコピーして、**下記4か所だけ**を差し替える。それ以外は全店共通なので触らない。

| # | 箇所 | 内容 |
|---|---|---|
| 1 | LINEのURL（全5か所） | `https://emiluca.salon/url/{エリア}/{県}/{店舗}/line.html` に差し替え |
| 2 | 電話番号（`tel:` 2か所＋表示3か所） | 店舗の番号へ |
| 3 | FV右上の所在地表記 | `<p class="hero__area">` の2行目 |
| 4 | 「エミルカ ◯◯店」セクション | 住所・アクセス・駐車場・営業時間・定休日・地図・店舗写真 |

タイトルタグと最終CTAの「24時間受付・◯◯店」も店舗名に合わせて変更する。

### 現在の岡山店の設定値

- LINE: `https://emiluca.salon/url/chu-shikoku/okayama/okayama/line.html`
  （公式サイトと同じ計測用リダイレクト。転送先は `https://lin.ee/1N4KlHx`。
  GTM `GTM-WXZZVG3` と Metaピクセル `384903723449031` が発火する）
- TEL: 090-7575-8384
- 住所: 〒701-1211 岡山県岡山市北区一宮1230 美容室 carsa infinity 内

## 構成の意図

- オファー（通常22,000円 → 初回9,600円 / 56%OFF）をファーストビュー内に置く
- LINE CTA を画面下に常時固定し、本文中にも4か所配置
- 施術事例（Before / After）を最大のボリュームにする（キャプション付き8件＋一覧15件）
- 事例以外の説明はすべて短くまとめる（理由3つ・流れ4ステップ・FAQ6問）

## 素材

写真・症例・お客様の声はすべて公式サイト（emiluca.salon / okayama.emiluca.salon）から取得。
症例のお悩み・メニュー・通院期間の記載は公式サイトの施術事例ページの内容に合わせている。

## 更新方法

```bash
git clone https://github.com/marketingteam2026jpn/emiluca-lp.git
# 編集後
git add -A && git commit -m "update" && git push origin main
```

数分でGitHub Pagesに反映される。
