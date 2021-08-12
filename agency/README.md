# 代理業用WPについて

現在代理業用WPは2種類存在します。  
以下は主に代理業用1：wp-kiji-maker.comのカスタマイズ箇所の手順・マニュアルになります。  
  
- 代理業用1：wp-kiji-maker.com（テーマは無料テーマの[bones](https://github.com/squibbleFish/theme-bones)を使用。後述するアンケート記事機能付き）  
https://wp-kiji-maker.com/wp-login.php  

- 代理業用2：lab-beautybooks.com（wp-kiji-maker.comと同一テーマ）  
https://lab-beautybooks.com/wp_beautybooks/wp-login.php  
  
※上記2サイトはTOPにアクセスしても何も表示させていません。  
  
# wp-kiji-maker.com エディターについて

wp-kiji-maker.comの投稿エディターはカスタムされ、  
エディタ内に様々な装飾ボタンがあります。  
その中の`Parts`ボタンも、カスタマイズで追加したパーツ集です。  

![エディタ画像](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/agency_editor1.png)
  
これらの装飾パーツを追加・修正するときの方法を紹介します。  
  
独自に追加したボタンや装飾はこちらのテストページに載っています。  
  
http://wp-kiji-maker.com/test3/  
  
なお、一部の追加ボタンはBokuravoスニペット集のボタンと同じです。（WP用にCSS側の記述が一部更新）  

http://bokuravo.sixcore.jp/kakunin/tsukada/template/lp/snipet/  
  
## Partsボタン内、各装飾パーツのCSSを修正する

自身の確認サーバー等で HTML デザイン化後、WP 用に CSS 及び HTML を調整します。  
WP の管理画面・サイト側記事詳細ページ両方に CSS のを反映させる必要があります。  
  
まずFTPで次のディレクトリへ移動しデータを全てDLします。  
  
`wp-content/plugins/visual-editor-extensions/`  
  
その中の`cssフォルダ`にある、`xeory_contents_decorator.css`を編集します。  
  
▼フルパス  
`wp-content/plugins/visual-editor-extensions/css/xeory_contents_decorator.css`  
  
  
▼修正するボタンのCSSを特定する方法  
wp-kiji-maker.comのWP管理画面へログイン後、投稿ページへ移動します。  
`Parts`ボタンをクリックし、装飾パーツのポップアップを表示した状態で、  
ブラウザのデベロッパーツールから対象のクラスを選択して見つけて下さい。  

<details>
<summary>:bulb: Tips 更新したCSSが反映されないとき</summary>

WPには沢山のCSSが読み込まれるため、セレクタの指定によっては、CSS反映の優先度が低く、反映されない場合があります。  
`.post`や`.entry-content`はWPが動的につける大枠のクラスになりますので、大枠のクラスから指定するようにしてください。  
分からなければ、既存のCSSセレクタをコピーしての使用をお願いします。
</details>

## Partsボタン内、各パーツのHTMLを追加する

`visual-editor-extensions/view.php`からHTMLを追加します。  
`<div class="content">`～`</div>`までがセットです。  
例では見出しパーツのHTMLを引っ張ってきています。  
実際は`<form>`～`</form>`内にボタンや見出しのHTMLを追加してください。  

```html

<!-- sample -->
<div class="content">
  <form>
    <div class="insert-content">
      <h2 class="m__title m__title--13-blue">
        見出しが入ります。見出しが入ります。
      </h2>
    </div>
    <input type="button" id="submit" class="button" name="insert" value="挿入する" onclick="return false;" />
  </form>
</div>

```

#### 注意点

パーツ自体に min-height（パーツのデザインによってお好みで）/max-width（～ 640px）を指定し、ある程度のサイズ感に留めておきます。

### [新規装飾パーツの実装時のバグ及び対処法](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/tree/master/wp_bug)

## アニメーションマーカー（黄）の編集

![アニメーションマーカー（黄）](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/agency_editor2.png)  

`visual-editor-extensions/js/attension.js`を展開。  
206～221行目にコードがあります。  
  
<details>
<summary>:bulb: Tips コード内optionの説明</summary>

```javascript

ed.addCommand('animation_marker_yellow_cmd', //コマンドID
  function() {
    var selected_text = ed.selection.getContent();
    var start_elem = '<span class="marker_yellow" data-aos="fade-right">';
    var end_elem = '</span>';
    tinymce.activeEditor.selection.setContent(start_elem + selected_text + end_elem);

  });
ed.addButton('animation_marker_yellow', //ボタンの名前
  {
    title: 'アニメーションマーカー（黄）',//titleテキスト
    image: url + '/img/animation_marker.svg',//ボタン画像
    cmd: 'animation_marker_yellow_cmd',//コマンドID
    classes: 'marker_yellow'//ボタンのクラス
  }
);

```
  
cmd：他のIDに被らないユニークIDを独自に設定  
title：エディタ内でホバーしたときに表示するテキスト  
image：エディタ内に表示するボタンの画像  
classes：ボタンのクラス
</details>

## 投稿ページエディター下にあるタブ類

デフォルトにはない、カスタマイズを追加したタブを複数追加しています。  

### アンケート記事LP用ファイル読み込み設定
  
後述する[アンケート記事用のCSS](#cssについて)を設定する  
  
![アンケート記事LP用ファイル読み込み設定](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/tab1.png)  

### ページ別クラス  
  
ページごとの<body>タグにクラスをつけるタブ  
  
![ページ別クラスページごとの<body>タグにクラスをつけるタブ](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/tab2.png)  

### ヘッダー画像設定
  
記事ヘッダーを追加するタブ  
  
![ヘッダー画像設定](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/tab3.png)  

### 広告コード設定  

<head>内にHTMLコードを追加できるタブ  
  
![広告コード設定](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/tab4.png)  

### メタタグを設定  
  
<meta>タグを設定するタブ  
  
![メタタグを設定](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/tab5.png)  

### CSSを設定  
  
ページごとにCSSを追加できます。  
  
![CSSを設定](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/tab6.png)  



### オプションタブの編集

`カスタムフィールド` > `フィールドグループ`に各オプションの設定タブがあるので、そこから編集をしてください。  


# アンケート記事
  
WP管理画面のメニューには、投稿の他に「アンケート記事」があります。  
こちらは4パターンのアンケート形式の記事LPを作成する専用の投稿ページになります。  
  
## テンプレート一覧
  
記事作成の担当者が次のテンプレートをコピーして、実際に記事作成を行っています。  

### mensclear  
http://wp-kiji-maker.com/questionnaire/qq_template_mensclear/  
  
### leasebacksenmon_lp1_ver1  
http://wp-kiji-maker.com/questionnaire/qq_template_leasebacksenmon_lp1_ver1/  
  
### leasebackconcierge_lp20_ver2_type1  
http://wp-kiji-maker.com/questionnaire/qq_template_leasebackconcierge_lp20_ver2_type1/  

### ieuru_lp02_ver1  
http://wp-kiji-maker.com/questionnaire/qq_template_ieuru_lp02_ver1/  
  
	
## 関連のファイル保存先

▼アンケート記事のHTML、PHP  
`wp-content\themes\new_article_template\questionnaire_template`  
  
▼CSS  
`wp-content\themes\new_article_template\library\css\qq`  


## アンケート記事の構造

`カスタム投稿タイプ`という仕組みを使っています。  
投稿エディタにHTMLを直接入れてビジュアルタブで、  
見たまま編集が出来るような仕組みになっています。  
こちらはHTMLが分からない記事編集者でも、自身で編集行えるようにするためです。  
ただし票数は数値固定です。（チェックを入れても数値が動的に変更するようにはしていません）  
  
▼テキストタブ  
![アンケート記事テキストタブ](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/question1.png)  

▼ビジュアルタブ  
![アンケート記事ビジュアルタブ](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/question2.png)  

### テーマ

アンケート記事には、[アンケート記事テンプレート一覧](#アンケート記事テンプレート一覧)に書いたとおり、  
4種類のレイアウトパターンに加え、テーマカラーを変更できるカスタマイズタブを作成してあります。  
このタブ設定は[こちら](#オプションタブの編集)と同じカスタムフィールドで設定しています。

### テーマカラー変更

![アンケート記事LP用ファイル読み込み設定](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/tab1.png)  

`はい`を選択し、変更したいテーマカラーのボタンを選択。  
プレビューを選択し、テーマカラー変更の確認後`更新`ボタンを押します。  
テーマカラーをデフォルトのものに戻したい場合は、  
`テーマ解除`を選択し、再度更新をしてください。  

### CSSについて

上記[テーマカラー変更](#テーマカラー変更)の下に、`ページ別クラス`タブがあります。  
アンケート記事のパターン別にクラスを指定していますので、  
CSSが適用されない事がある場合は、こちらの設定を見直して、クラスがついているかどうか確認してください。  

![ページ別クラスページごとの<body>タグにクラスをつけるタブ](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/tab2.png)  

### アンケート記事毎の<body>タグに付与しているクラス名

```text

▼ <body>クラス：mensclear  
http://wp-kiji-maker.com/questionnaire/qq_template_mensclear/  
  
▼ <body>クラス：mensclear  
http://wp-kiji-maker.com/questionnaire/qq_template_leasebacksenmon_lp1_ver1/  
  
▼ <body>クラス：leasebackconcierge_lp20_ver2_type1  
http://wp-kiji-maker.com/questionnaire/qq_template_leasebackconcierge_lp20_ver2_type1/  

▼ <body>クラス：ieuru_lp02_ver1
http://wp-kiji-maker.com/questionnaire/qq_template_ieuru_lp02_ver1/

```

