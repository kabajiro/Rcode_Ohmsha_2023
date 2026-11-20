---
layout: default
title: 正誤表
---

<style>
.er-head{display:flex;gap:28px;align-items:flex-start;margin:4px 0 28px;}
.er-head img{width:200px;max-width:38%;height:auto;border:1px solid #d0d7de;border-radius:6px;box-shadow:0 4px 14px rgba(0,0,0,.12);flex:none;}
.er-meta{flex:1;min-width:0;}
.er-meta h1{margin:0 0 6px;border:none;padding:0;}
.er-meta .er-sub{color:#57606a;margin:0 0 14px;font-size:1.05em;}
.er-meta dl{display:grid;grid-template-columns:auto 1fr;gap:4px 14px;margin:0;font-size:0.95em;}
.er-meta dt{color:#57606a;font-weight:600;}
.er-meta dd{margin:0;}
.er-note{padding:12px 16px;border-left:4px solid #0969da;background:#f6f8fa;border-radius:4px;margin:12px 0;}
@media (max-width:600px){.er-head{flex-direction:column;align-items:center;text-align:center}.er-meta dl{text-align:left}}
</style>

<div class="er-head">
<img src="assets/cover.jpg" alt="『医学研究のためのRによる統計解析入門』の表紙">
<div class="er-meta">
<h1>正誤表</h1>
<p class="er-sub">『医学研究のためのRによる統計解析入門』</p>
<dl>
<dt>著者</dt><dd>加葉田大志朗 著・新谷歩 監修</dd>
<dt>出版社</dt><dd>オーム社（<a href="https://www.ohmsha.co.jp/book/9784274230905.html">書籍ページ</a>）</dd>
<dt>発売</dt><dd>2023年9月27日</dd>
<dt>ISBN</dt><dd>978-4-274-23090-5</dd>
<dt>正誤情報の最終更新</dt><dd>2026年8月20日</dd>
</dl>
</div>
</div>

刊行後に判明した誤りと訂正の内容を，このページで随時お知らせします．紙面の修正は，今後の増刷・改訂の際に反映予定です．

[サポートページのトップに戻る](index.html)

## 誤植の訂正

| 該当箇所              | 誤                           | 正                           | 補足                                                 | 対象刷    |
| --------------------- | ---------------------------- | ---------------------------- | ---------------------------------------------------- | --------- |
| p.51 本文 下から4行目 | `data_strt` の差分によって | `date_strt` の差分によって | 本文中の変数名の誤植です．コードに誤りはありません． | 第3刷まで |

## 本文コードに関する補足

### p.86 ほか 第4章のコード実行時のエラーについて（変数 `years_fu` のデータ型）

第2章の手順で作成したデータフレーム `new` をそのまま利用して第4章を読み進めると，p.81〜84 の `t.test()`・`var.test()` などは問題なく実行できますが，p.86 の `hist()` で「x は数値でなければなりません」というエラーが生じます（p.93 の `shapiro.test()`・p.94 の `wilcox.test()` でも同様です）．

これは，第2章で日付型（date class）どうしの差分から作成した変数 `days_fu`・`years_fu`（p.54）が，厳密には数値型（numeric）ではなく，日数（days）という単位の情報が付与された difftime クラス（時間差を表すRのデータ型）になっているためです．RStudio の Environment パネルで `new` の中身を確認すると，これらの変数は「○○ days」のように表示されます．difftime クラスのままでも数値として扱ってくれる関数は多くありますが，`hist()` などの一部の関数は厳密な数値型のみを受け付けるため，上記のエラーが生じます．

基本的な対策は，関数 `as.numeric`（p.53 表2.8）を利用して厳密な数値型へ変換することです．第4章の最初のコード（p.81 の `t.test()`）の直前に，次の1行を実行することでエラーを回避できます．

```r
new$years_fu <- as.numeric(new$years_fu)
```

なお，配布している [Rcode.html](Rcode.html) では，第2章の最後（p.55）で書き出した new.csv を第4章の冒頭で `new <- read.csv("new.csv")` により読み込み直しており，CSVファイルを経由する過程で `years_fu` が数値型として読み込まれるため，このエラーは生じません．ただし，このような暗黙的な型変換に頼る構成は最適とは言い難いため，本書次回改訂時に上記の1行を第4章冒頭の紙面へ追記する予定です．[Rcode.html](Rcode.html) にはこの対応を反映済みです（2026年8月20日）．

## 紙面表示に関する補足

### p.51 `new30` 実行後のコンソール表示について（第3刷まで）

紙面では，`new30` のコード実行後のコンソール表示として1段目（`id`〜`sex_lab`）のみを記載していますが，実際の実行画面では，折り返し2段目に `ps_lab`・`treat_lab`・`depth_cm` が表示されます．

この手順で追加した変数（`treat_lab`・`depth_cm`）と，それ以前の手順で追加した `ps_lab` の内容が紙面上で確認できない状態となっていたため，次回増刷時に紙面を修正予定です．

- コード自体は問題なく実行できます．実際の実行結果（全列の表示）は [Rcode.html](Rcode.html) でご確認いただけます．
- なお，引数 `print = FALSE` は上記のデータ表示に関わるものではなく，「このようなデータを作成した」という説明表示を省略するためのオプションです．

## 誤りを見つけたら

本書の記述やコードに誤りと思われる箇所を見つけた場合は，オーム社の[書籍お問合せフォーム](https://www.ohmsha.co.jp/contact/book.php?isbn=978-4-274-23090-5)からお知らせください．頁番号と該当箇所（節・項，図表番号，コードの行など）を書き添えていただけると，確認がはやく進みます．オーム社の[書籍ページ](https://www.ohmsha.co.jp/book/9784274230905.html#errata)の「正誤表」欄もあわせてご確認ください．
