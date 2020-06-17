# WordPress-sharing

【Bokuravo 社内用】記事 LP 用 WP の情報共有シートです。:deciduous_tree:

## はじめに

改修中に困ったらこのリポジトリを参照してください。  
もしかすると対処方法が載っているかもしれません。  
こちらのファイルに対処方法が記載されていない場合や、新たなバグや修正が困難な箇所が見つかった場合は、なるべく詳細に追記して頂きますようお願いします。

## 装飾パーツ

### 新規追加時の実装手順

自身の確認サーバー等で HTML デザイン化後、WP 用に CSS 及び HTML を調整します。  
WP の管理画面・サイト側記事詳細ページ両方に CSS のを反映させる必要があります。

**管理画面・サイト側記事詳細ページ両方に効く CSS**  
`\wp-content\plugins\visual-editor-extensions\css\xeory_contents_decorator.css`

**管理画面のみに効く CSS**  
`\wp-content\plugins\visual-editor-extensions\css\admin-style.css`

#### 注意点

パーツ自体に min-height（パーツのデザインによってお好みで）/max-width（～ 640px）を指定し、ある程度のサイズ感に留めておきます。

### [新規装飾パーツの実装時のバグ及び対処法](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/tree/master/wp_bug)
