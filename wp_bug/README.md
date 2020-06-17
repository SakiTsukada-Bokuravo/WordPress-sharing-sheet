# 新規装飾パーツの実装時のバグ及び対処法

#### 現象

ボタン・見出し・ブロックに`<img>`タグで画像を表示したパーツがエディタ内で以下の現象が起きる。

1. 保存時にリンクやアイコンが消える。

2. リンクが選択出来なくなり URL が変更できない。

#### 対処方法

1. ボタン内のアイコン等には画像を使用せず、CSS の'background-image'での実装をお願いします。
2. tinymce-advanced の設定で上級者向け設定の下記 2 つのチェックを外す。
   1. クラシック版の段落ブロックを追加
   2. クラシック版の段落もしくはクラシックブロックをデフォルトのブロックにする (ハイブリッドモード)
   
![tinyMce Advanced setting](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/wp-tinymce-advance-setting.png?raw=true)
