# WP制作事業 テーマ作成用ガイドライン

***【Bokuravo 社内用】***
このファイルはWPテーマ作成のコーディングガイドラインの目次です。

## Introduction（本ページ）

[README.md](README.md)

同階層ファイルの管理用。

## Order1-A案件 テーマ作成フロー

[order1a_flow.md](order1a_flow.md)

オーダー1A制作案件の概要説明です。  
全体的な制作の流れを記しています。  
なお、このページではテーマ制作の説明を省いています。  
テーマ制作は別ページの[coding_guidline.md](coding_guidline.md)を参考にしてください。

## WP環境をまるごと複製フロー

[duplication_flow.md](duplication_flow.md)

オーダー1Aテーマと、WP管理画面のDBをエクスポートし、複製先へ複製する手順です。  
おそらくこのやり方でWPサイトを多く構築する事になると思います。  
  
オーダー1Aテーマが入っているデモサイト（[wpt-demo.com](https://wpt-demo.com/)）はマルチサイト化（サブディレクトリ型）にしているためです。  

#### Tips

[マルチサイト化とは](https://www.sejuku.net/blog/83193)（外部サイトへ飛びます）

## WPテーマガイドライン

[coding_guideline.md](coding_guideline.md)

テーマのコーディングを行う上で、ガイドラインを定めました。  
テーマのHTML/CSSのルールや、テーマの構造についてはこちらのページにまとまっています。

## WP組込フロー

[include_wp_flow.md](include_wp_flow.md)

このフローは上記WP環境まるごと複製フローをせずに、1から新規でテーマを作成する時の流れです。  
HTMLコーディングが完了してからの、WPのテーマに組み込む際の流れを記しています。

## WPリニューアル制作フロー

[renewal_flow.md](renewal_flow.md)

WPリニューアルの際の作業項目の確認メモになります。  
ラビット探偵WPリニューアル案件の実例を元に、メモを作成しました。  
良ければお役立て下さい。