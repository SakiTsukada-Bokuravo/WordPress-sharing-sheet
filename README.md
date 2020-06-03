# WordPress-sharing
【Bokuravo社内用】記事LP用WPの情報共有シートです。:deciduous_tree:


## はじめに
改修中に困ったらこのリポジトリを参照してください。  
もしかすると対処方法が載っているかもしれません。  
こちらのファイルに対処方法が記載されていない場合や、新たなバグや修正が困難な箇所が見つかった場合は、なるべく詳細に追記して頂きますようお願いします。

## 装飾パーツ

### 新規追加時の実装手順
自身の確認サーバー等でHTMLデザイン化後、WP用にCSS及びHTMLを調整します。  
WPの管理画面・サイト側記事詳細ページ両方にCSSのを反映させる必要があります。  

** 管理画面・サイト側記事詳細ページ両方に効くCSS **
` \wp-content\plugins\visual-editor-extensions\css\xeory_contents_decorator.css `

** 管理画面のみに効くCSS **
` \wp-content\plugins\visual-editor-extensions\css\admin-style.css `

#### 注意点
パーツ自体にmin-height（パーツのデザインによってお好みで）/max-width（～640px）を指定し、ある程度のサイズ感に留めておきます。


### 新規装飾パーツの実装時のバグ及び対処法

#### バグ
- ボタン・見出し・ブロックに'<img>'タグで画像を表示したパーツがエディタ内でバグる。

#### 対処方法
画像を表示せず、CSSの'background'での実装をお願いします。