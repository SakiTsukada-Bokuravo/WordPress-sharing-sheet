# WP制作事業 テーマ作成用WP組み込みフロー

**【Bokuravo 社内用】**

このテキストは、コーディングガイドラインに沿ってコーディングした静的HTMLサイトを、WPへ組み込むフローです。

コーディングガイドラインを確認する場合は、[こちら](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/tree/tsukada/coding_guidline)から確認できます。

また、ファイル作成の紹介コードは[株式会社サラ様](https://thorough-sol.co.jp/)のコードを流用させて頂いています。



## ■このフローのゴール

HTMLサイトをWPで組み込み、最終的にWEBブラウザで表示するまでがゴールです。

## ■目次

[テーマフォルダ作成](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/tsukada/coding_guidline/include_wp_flow.md#%E3%83%86%E3%83%BC%E3%83%9E%E3%83%95%E3%82%A9%E3%83%AB%E3%83%80%E4%BD%9C%E6%88%90)

[テンプレートファイル分割](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/tsukada/coding_guidline/include_wp_flow.md#%E3%83%86%E3%83%B3%E3%83%97%E3%83%AC%E3%83%BC%E3%83%88%E3%83%95%E3%82%A1%E3%82%A4%E3%83%AB%E5%88%86%E5%89%B2)

[各ファイルを作成](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/tsukada/coding_guidline/include_wp_flow.md#%E5%90%84%E3%83%95%E3%82%A1%E3%82%A4%E3%83%AB%E3%82%92%E4%BD%9C%E6%88%90)

  [style.css テーマ宣言](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/tsukada/coding_guidline/include_wp_flow.md#stylecss%E3%81%AB%E3%83%86%E3%83%BC%E3%83%9E%E5%AE%A3%E8%A8%80)

[各ファイルの中身を作成](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/tsukada/coding_guidline/include_wp_flow.md#%E5%90%84%E3%83%95%E3%82%A1%E3%82%A4%E3%83%AB%E3%81%AE%E4%B8%AD%E8%BA%AB%E3%82%92%E4%BD%9C%E6%88%90)

  [functions.php](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/tsukada/coding_guidline/include_wp_flow.md#functionsphp%E4%BD%9C%E6%88%90)

  [head.php](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/tsukada/coding_guidline/include_wp_flow.md#head%E6%83%85%E5%A0%B1%E4%BD%9C%E6%88%90)

  [scripts.php](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/tsukada/coding_guidline/include_wp_flow.md#scriptsphp%E4%BD%9C%E6%88%90)

  [header.php](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/tsukada/coding_guidline/include_wp_flow.md#headerphp%E4%BD%9C%E6%88%90%E3%83%98%E3%83%83%E3%83%80%E3%83%BC%E3%83%8A%E3%83%93%E8%A8%AD%E5%AE%9A)

  [footer.php](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/tsukada/coding_guidline/include_wp_flow.md#footerphp%E4%BD%9C%E6%88%90)

  [front-page.php](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/tsukada/coding_guidline/include_wp_flow.md#front-pagephp%E4%BD%9C%E6%88%90)

  [front-page.php - お知らせ](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/tsukada/coding_guidline/include_wp_flow.md#%E3%83%88%E3%83%83%E3%83%97%E3%83%9A%E3%83%BC%E3%82%B8%E5%86%85%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9%E4%B8%80%E8%A6%A7%E4%BD%9C%E6%88%90)

  [index.php](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/tsukada/coding_guidline/include_wp_flow.md#indexphp%E4%BD%9C%E6%88%90)

  [page.php](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/tsukada/coding_guidline/include_wp_flow.md#pagephp%E4%BD%9C%E6%88%90)

WordPress組み込み後チェック


## ■テーマフォルダ作成

テーマ名と同じ名前のフォルダを作成し以下のディレクトリ構成にします。

<details>
<summary>ディレクトリ構造</summary>

```text

[Order1]
  │
  │ // ▼ --- 今回追加するファイル
  ├ [parts]
  │   ├ head.php    // head内の共通データ
  │   └ scripts.php // js記述、読込
  │
  ├ style.css
  ├ screenshot.png // テーマ画像(1200x900)
  ├ function.php   // サイト全体の設定等
  ├ front-page.php // TOPページ。index.phpより表示優先度が低い
  ├ footer.php     // フッター
  ├ header.php     // ヘッダー
  ├ page.php       // 固定ページ
  ├ index.php      // 必須ファイル。1番表示優先度が低いTOPページ
  │
  │ // ▼ --- HTMLコーディングで作成したファイル群
  ├ [src]
  │   └ 省略
  └ [dist]
      └ 省略
```
</details>


## ■テンプレートファイル分割

トップ(index.html)：`front-page.php`

ヘッダー:`header.php`

フッター:`footer.php`

head:`parts/head.php`

Javascript関連:`parts/scripts.php`

プラポリ(privacy.html)：`page.php`

問い合わせTOP(contact.html)：`page.php`

問い合わせ確認(contact_confirm.html)：`page.php`

問い合わせ完了(contact_complete.html)：`page.php`


<details>
<summary>なぜトップをfront-page.phpにするか</summary>


管理画面にはどのページをトップページにするかこのような表示設定があります。

![管理画面の表示設定](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/wp_admin_view_settings.png?raw=true)

PHPファイルにもトップページを表示可能なファイルが`index.php` `home.php` `front-page.php`と3つあります。

この3つのファイルには表示優先度がそれぞれ違います。

1. front-page.php（最優先）
2. home.php
3. index.php

それらの設定と、ニュース一覧ページも必要な場合それぞれファイルを分ける必要がありますので、

どのプランのトップページも`front-page.php`で統一します。

ニュース一覧：index.php
トップページ：front-page.php


▼詳しい各ファイルの表示優先度

> [詳細はこちら](https://www.at-freak.jp/column/wp_front-page/)

・front-page.php
・home.php
・index.php
上記3ファイルがテーマ内にあった場合、
トップページのテンプレートには、［ホームページの表示］の設定が

■［最新の投稿］の場合：
　front-page.phpが使用される

■［固定ページ］［ホームページ］のみ指定の場合：
　front-page.phpが使用される

■［固定ページ］［投稿ページ］のみ指定の場合：
　home.phpが使用される、
　かつ同じソースの固定ページ（投稿一覧ページ）が表出来上がる
</details>



## ■各ファイルを作成

テーマプランに合わせファイルを振り分けた後、それぞれ空のPHPファイルを作成します。
共通部分のコードはindex.html等からくり抜き作成します。
プラポリ・お問い合わせ3ページ分は固定ページで作成するため、固定ページ出力用のファイル1つを用意します。

`functions.php`(必須)

`index.php`(必須 ※Order2以降ニュース一覧になる)

`style.css`(必須)

`front-page.php`(トップページ表示)

`footer.php`(フッター)

`header.php`(ヘッダー)

`page.php`(固定ページ表示: プラポリ/問い合わせ入力/問い合わせ確認/問い合わせ完了)

`single.php`(ニュース詳細 ※Order2以降作成する)

`[parts]フォルダ > head.php` (head情報)

`[parts]フォルダ >  scripts.php` (JSファイル読み込み)


## ■各ファイルの中身を作成

- style.css
- functions.php
- scripts.php
- header.php: ページごとの動的クラス作成
- footer.php
- front-page.php
- front-page.php: ニュース一覧作成
- index.php
- page.php


### style.cssにテーマ宣言


テーマを有効にするため、追加した`style.css`にテーマ情報を記述します。
最低限Theme Nameを入れておけば、管理画面のテーマ選択画面にてテーマを有効化出来るようになります。
その他のテーマ情報は、任意となりますが、既存のテーマファイルが存在している場合はその内容に従って入力します。


▼ 全てのテーマ情報
```css
/*
Theme Name: 任意のテーマ名（必須）
Theme URL: テーマのサイトのURI
Description: テーマの説明
Author: Bokuravo Inc.
Version: テーマのバージョン
Tags: テーマの特徴を表すタグ（カンマ区切り/オプション）
License: テーマのライセンス
License URI: テーマのライセンスのURI
*/
```

▼ 例
```css
/*
Theme Name: Order1-A
Description: This is Order1-A theme.
Version: 1.0
*/
```

余談：
descriptionや管理画面内に「●●（自社名・自社サービス名）専用のWordPressテーマです」と明記してあると喜んでくださるクライアント様が多いようです。
このような細かくケアを行うと他社との差別化に繋がりますので、なるべく対応出来ると良いかもです。


### functions.php作成

`functions.php`に以下をそのまま記述します。

```php

<?
```


### head情報作成

`parts/head.php`を開き、head情報をhtmlからコピペ後パスを書き換えます。

※コード内のテキストはテンプレに合わせて変更してください。


▼ 記述例

```php

//parts/head.php例

<?php
  $themePath = get_template_directory_uri().'/dist/';
?>
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="keywords" content="キーワード1,キーワード2,キーワード3">
  <meta name="description" content="<?php bloginfo('description');?>">
  <meta name="format-detection" content="telephone=no">
  <meta property="og:title" content="<?php bloginfo('name');?>" />
  <meta property="og:description" content="<?php bloginfo('description');?>" />
  <meta property="og:type" content="website" />
  <meta property="og:locale" content="ja_JP" />
  <meta property="og:url" content="<?php bloginfo('url');?>" />
  <meta property="og:image" content="<?php echo $themePath; ?>img/ogp.png" />
  <meta property="og:image:width" content="1200px" />
  <meta property="og:image:height" content="630px" />
  <meta name="twitter:card" content="summary_large_image">
  <title><?php bloginfo('name');?></title>
  <link rel="canonical" href="<?php bloginfo('url');?>">
  <link rel="stylesheet" href="<?php echo $themePath; ?>css/style.css">
  <link rel="stylesheet" href="<?php echo $themePath; ?>css/swiper.min.css">
  <link rel="shortcut icon" href="<?php echo $themePath; ?>favicon.ico">
  <link rel="apple-touch-icon" sizes="180x180" href="<?php echo $themePath; ?>apple-touch-icon.png">
  <?php if(is_page('contact')): ?>
    <script>
    // お問い合わせ iosで拡大防止
    var ua = navigator.userAgent.toLowerCase();
    var isiOS = (ua.indexOf('iphone') > -1) || (ua.indexOf('ipad') > -1);
    if(isiOS) {
      var viewport = document.querySelector('meta[name="viewport"]');
      if(viewport) {
        var viewportContent = viewport.getAttribute('content');
        viewport.setAttribute('content', viewportContent + ', user-scalable=no');
      }
    }
    </script>
  <?php endif;?>
  <?php wp_head(); ?>
</head>
```


### scripts.php作成

`parts/scripts.php`を開き、JSファイルを読み込むコードを記述します。

※読み込むファイルはテンプレに合わせて変更してください。

```php
// parts/scripts.php

<?php
  $themePath = get_template_directory_uri().'/dist/';
?>

// 各ファイルを読み込む
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
<script src="<?php echo $themePath; ?>js/common.bundle.js"></script>
<script src="<?php echo $themePath; ?>js/top.bundle.js"></script>

function my_scripts() {
  wp_enqueue_style( 'style-name', get_template_directory_uri() . '/css/ファイル名.css', array(), '1.0.0', 'all' );
  wp_enqueue_script( 'script-name', get_template_directory_uri() . '/js/jsファイル名.js', array( 'jquery' ), '1.0.0', true );
  wp_enqueue_script( 'script-name', 'https://code.jquery.com/jquery-3.5.1.js', array(), '1.0.0', true ); // 外部URLを直接読み込む場合
}
add_action( 'wp_enqueue_scripts', 'my_scripts' );
```

`function my_scripts()`内、jQueryを読み込む必要がないライブラリの場合は`array()`の()内を空白にします。

`array()`の右隣`'1.0.0'`は任意のバージョン番号です。（キャッシュクリア対策等の意味が含まれます）


### header.php作成、ヘッダーナビ設定

`header.php`にパスとheader部分のHTMLの記述と、ヘッダーナビの表示設定をします。
`<main>`の開始タグを最後に入れることを忘れないでください。


### header.php作成

以下のコードはヘッダーナビ以外は省略していますが、header.phpに入れる全コードです。
共通化するためbodyタグの始まりと、mainタグの始まりもまとめて記述します。

<details>
<summary>header.phpの記述例</summary>

```php

// header.php
<?php
  $themePath = get_template_directory_uri().'/dist/';
  $postId = get_the_ID();// 投稿記事（ニュース）のIDを取得する
  $pageClass = get_post_meta($postId, 'page-class', true);// bodyに設定するカスタムクラスを変数に入れる
?>

<!DOCTYPE html>
<html lang="ja">

<?php get_template_part( 'parts/head' ); ?>// head情報を呼び出す

<?php if(is_front_page()):?>// front-page.phpを表示の時
<body class='top'>// bodyタグに「top」クラスを付与
<?php else : ?>// それ以外のページの時は
<body class='<?php echo $pageClass; ?>'>// 後に設定するカスタムクラスの値に応じてクラスを表示する
<?php endif; ?>

<div class="allwrapper">
  // 省略

  <nav class="header__nav" role="navigation" itemscope itemtype="http://schema.org/SiteNavigationElement">
    <?php 
      $headerNav =
      array(
        //カスタムメニュー名
        'theme_location' => 'header_nav',
        //ulを梱包する親divを非表示
        'container' => false,
        //カスタムメニューを設定しない際に固定ページでメニューを作成しない
        'fallback_cb' => false,
        // 出力される要素の中のulにメニュークラスを付ける
        'menu_class' => 'h_nav__list',
      );
      wp_nav_menu( $headerNav );
    ?>
   </nav>

</header>

<main class="m">
```
</details>

**ヘッダーナビ作成手順**

1. functions.phpにナビゲーションメニューの有効化設定を書く
2. 管理画面左メニュー > 外観 > メニュー からナビゲーションメニューを登録
3. PHP側の出力設定


### 1. functions.phpにナビゲーションメニューの有効化設定を書く

詳細な説明は[こちら](https://wp-fan.com/wordpress/register-custom-menu/)

functions.php内に以下を例に記述します。
このコードを書くことにより、初めて管理画面内でメニュー登録が行えるようになります。

`array()`内の`header_nav`、`footer_nav`はそれぞれ任意の名前に変更して構いません。
ただし、どのメニューか分かるように命名してください。

<details>
<summary>functions.phpの記述例</summary>

```php

// ************************************************
//  ナビゲーション
// ************************************************
//ナビゲーションを登録する
function register_custom_menus() {
  register_nav_menus( array(
    //この中にカスタムメニューを定義 '場所' => '説明'
    'header_nav' => 'ヘッダーナビゲーション',
    'footer_nav' => 'フッターナビゲーション'
  ));
}
add_action( 'after_setup_theme', 'register_custom_menus' );

// ナビゲーションに説明が入力されていたら、サブタイトルとして表示
function description_in_custom_nav_menu($item_output, $item){
  return preg_replace('/(<a.*?>[^<]*?)</', '$1' . "<span class='h_nav__sub_text'>{$item->description}</span><", $item_output);
}
add_filter('walker_nav_menu_start_el', 'description_in_custom_nav_menu', 10, 4);
```
</details>


### 2.ナビゲーションメニューを登録

管理画面左メニュー > 外観 > メニュー

「新しいメニューを作成しましょう」のリンクをクリックし、メニューを新規作成します。
メニュー名には1で設定したメニュー名を入れましょう。
その後CSS class(オプション)に、HTML側のliタグの指定しているクラス名を入れます。

![管理画面から出力したグローバルメニューのliタグにクラスを付ける](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/li-add-class.png)

もしメニューに日本語＋英語等のサブタイトルが入る場合は「説明」のテキストエリアにサブタイトルのテキストを入力します。
完了後、メニューの出力位置にチェックをつけます。

![メニュー作成例](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/custommenu1.png?raw=true)

※上記の作成例のリンクは、アンカーリンクを指定しています。
※ヘッダー、フッター等でそれぞれ異なるスタイルのメニューが必要な場合は必要分メニューを作成します。


### 3. PHP側の出力設定

`theme_location`の値は1で設定したメニュー名を入れます。
※コード内のクラス名はテンプレに合わせて変更してください。

<details>
<summary>header.phpの記述例</summary>

```php

// header.php
  <nav class="header__nav" role="navigation" itemscope itemtype="http://schema.org/SiteNavigationElement">
    <?php 
      $headerNav =
      array(
        //カスタムメニュー名
        'theme_location' => 'header_nav',
        //ulを梱包する親divを非表示
        'container' => false,
        //カスタムメニューを設定しない際に固定ページでメニューを作成しない
        'fallback_cb' => false,
        // 出力される要素の中のulにメニュークラスを付ける
        'menu_class' => 'h_nav__list',
      );
      wp_nav_menu( $headerNav );
    ?>
   </nav>
```
</details>


### footer.php作成

先程の`header.php`と同じ要領でfooter.phpを作成します。
以下は完成例のコード例です。
管理画面側のナビゲーション設定はヘッダーナビと同じ手順なため割愛します。

※コード内のクラス名はテンプレに合わせて変更してください。

<details>
<summary>footer.phpの記述例</summary>

```php

// footer.php
<?php
  $themePath = get_template_directory_uri().'/dist/';
?>
</div>
</main>

<!-- footer -->
<footer class="f">
  <div class="container wrapper f_container">
    <div class="f_head">
      <div class="f_head__info">
        <p class="f_head__logo">
          // テキストロゴ、画像ロゴの判別とそれに応じて出力する
          <?php 
            $custom_logo_id = get_theme_mod( 'custom_logo' );
            $logo = wp_get_attachment_image_src( $custom_logo_id , 'full' );
            if ( has_custom_logo() ) {
                    echo '<img src="' . esc_url( $logo[0] ) . '" alt="' . get_bloginfo( 'name' ) . '" class="f_head__logo_img">';
            } else {
                    echo get_bloginfo( 'name' );
            }
          ?>
        </p>
        <div class="f_address">
          <p class="f_address__text"><span class="f_address__text--postal_code">〒123-4567</span>東京都渋谷区渋谷1-1-1オーダービル1F</p><a class="f_address__link" href="#">Google map</a>
        </div>
      </div>
      <nav class="f_nav">
        <?php 
          $footerNav =
          array (
            //カスタムメニュー名
            'theme_location' => 'footer_nav',
            //ulを梱包する親divを非表示い
            'container' => false,
            //カスタムメニューを設定しない際に固定ページでメニューを作成しない
            'fallback_cb' => false,
            'menu_class' => 'f_nav__list'
          );
          wp_nav_menu( $footerNav );
        ?>
      </nav>
    </div>
    <div class="f_bottom"><small class="f_copy">© <?php echo date('Y');?> <?php bloginfo('name');?> All Rights Reserved.</small>
      <p class="f_privacy"><a class="f_privacy__link" href="<?php bloginfo('url');?>/privacy">プライバシーポリシー</a></p>
    </div>
  </div>
</footer>
<!-- / footer -->
<?php
  get_template_part( 'parts/scripts' );
  wp_footer();
?>

</body>

</html>
```
</details>



### front-page.php作成

`front-page.php`にHTMLコーディングを行ったディレクトリ内のファイルを読み込むためのパスを記述します。
この`get_template_directory_uri()`タグは、WP独自の関数で、動的にテーマディレクトリのパスを出力してくれます。

```php

<?php
  $themePath = get_template_directory_uri().'/dist/';
?>
```

次に上の記述の下に`<?php get_header(); ?>`を、
一番最後に`<?php get_footer(); ?>`を記述します。
それぞれのタグは外部ファイルに分けたヘッダー、フッターを呼び出すWP独自の関数です。


```php

<?php
  $themePath = get_template_directory_uri().'/dist/';
?>

<?php get_header(); ?>

<?php get_footer(); ?>
```

`<?php get_header(); ?>`の下に、`dispt/ index.html`のメインコンテンツのコードを全コピペします。

その後`<img>` `<a>`タグのパスをそれぞれ変更します。
最終的に全てのリンクパス、画像パスは以下のようになれば大丈夫です。

```php

// front-page.php

<?php
  $themePath = get_template_directory_uri().'/dist/';
?>
<?php get_header(); ?>

<section>

  // imgタグのパス変更
  <img src="<?php echo $themePath; ?>img/image.jpg">

  // aタグのパス変更
  <a href="<?php echo $linkUrl; ?>">

</section>

<?php get_footer(); ?>
```


### トップページ内ニュース一覧作成

`front-page.php`内に以下を記述し、投稿画面のプラグイン「アドバンスドカスタムフィールド」の「画面非表示」設定から「コンテンツエディタ」をチェックする。

![アドバンスドカスタムフィールド非表示設定](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/advanced-custom-field-hide-settings.png?raw=true)


※コード内のクラス名はテンプレに合わせて変更してください。

```php

// front-page.php
<div class="m__news_list">
  <?php
    $args = array(
      'posts_per_page' => 5 // 表示件数の指定
    );
    $posts = get_posts( $args );
    foreach ( $posts as $post ): // ループ開始
    $postId = get_the_ID(); // 投稿ページIDを出力
    $linkUrl = get_post_meta($postId, 'link_url', true); // 指定したIDの投稿のメタデータを取得する
    setup_postdata( $post ); // グローバル投稿データの設定
  ?>
  <?php if(empty($linkUrl)) : ?> // 外部リンクが設定されている時の表示
      <div class="m__news_item">
        <time class="m__news_date"><?php the_date( 'Y.m.d' ); ?></time>// 投稿日
        <span class="m__news_item_title">
          <?php the_title();?>// 記事タイトル
        </span>
      </div>
    <?php else : ?> // // 外部リンクデータが設定されていない時の表示
      <a href="<?php echo $linkUrl; ?>" class="m__news_item" target="_blank">
        <time class="m__news_date"><?php the_date( 'Y.m.d' ); ?></time>
        <span class="m__news_item_title">
          <?php the_title();?>
        </span>
      </a>
    <?php endif; ?>
   <?php
    endforeach; // ループ修了
    wp_reset_postdata();
  ?>
</div>

```
</details>



### index.php作成

index.phpは必須ファイルなためニュース一覧が必要ない場合でも中身を作成します。

```php

<?php
/*
* Order1-A:トップページ用テンプレート
*/
get_header(); ?>

<?php get_footer(); ?>
```



### page.php作成

個別ページ用のファイルを1つ用意し、ページごとにbodyのクラスを割り振ることでCSSの適用を切り替えます。
クラスの変更だけでは賄えない場合は新規の`page-●●.php`（●●はページ名）ファイルを作成してください。
PHP側に出力するクラスは`header.php`の中身を作成した段階で記述しています。


**個別ページ作成手順**
1. page.phpの中身を作成
2. 管理画面のカスタムフィールドを設定
3. 個別ページを作成


### 1. page.phpの中身を作成

`page.php`を`front-page.php`と同じようにヘッダー、フッター、中身を用意します。

<details>
<summary>page.php 記述例</summary>

```php

<?php
/*
* Template Name: Order1-A
*/
get_header();
?>
 
<?php if(have_posts()): while(have_posts()):the_post(); ?> // Start the Loop.
  the_content();
  endwhile; // End the loop.
endif;
?>
<?php get_footer(); ?>
```
</details>



### 2. 管理画面のカスタムフィールドを設定

固定ページごとにbodyタグにクラス名を入れて、ページ判別でCSSを切り替えるため、
管理画面のカスタムフィールドから以下のようにフィールドを追加します。
フィールド名は`page-class`にします。

![カスタムフィールド設定](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/cf-add-page-class.png?raw=true)


### 3. 個別ページを作成

次に固定ページを作成します。
エディターのモードをテキストに変更し、作成したHTMLのメインコンテンツ部分を流し込みます。


![エディターのモード](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/change-editor-mode.png?raw=true)


コンテンツの中身はこれらのファイルの`<main>`タグの中身を管理画面から直接書きます。

`privacy.html`
`contact.html`
`contact_confirm.html`
`contact_complete.html`
`about.html`


入力した個別クラスを記述し、固定ページを公開すると`<body>`に入力したクラス名が反映されます。

![カスタムフィールド設定](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/page-class-settings.png?raw=true)


![個別ページを公開すると入力したクラスが反映された](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/add-body-class.png?raw=true)


| 個別ページクラス名 |  |
| ------------- | ------------- |
| 会社情報  | about |
| プライバシーポリシー  | privacy  |
| お問い合わせ3ページ分  | contact |
---


## ■Contact Form 7でメールフォーム設定

まずこのプラグインがインストール済みか確認します。なければ新規追加してください。

- Contact Form 7
- Contact Form 7 add confirm

### お問い合わせメニューからフォームを新規作成

主にお問い合わせのパーツ部分となるHTMLだけ抜き出します。
以下の入力例を参考に、入力エリアのタグを専用タグに書き換えます。入力タグの次に`<p class="js-confirm"></p>`を1つ入れます。
このタグは確認ページ用のスタイルに必要になります。

![コンタクトフォーム作成例](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/contactform1.png?raw=true)

<details>
<summary>コンタクトフォーム 記述例全コード</summary>

```html
<dl class="form__item">
<dt class="form__label">貴社名</dt>
<dd class="form__desc">
[text company-name placeholder "株式会社DEMO Inc."]<p class="js-confirm"></p>
</dd>
</dl>

<dl class="form__item">
<dt class="form__label requied">お名前</dt>
<dd class="form__desc">
[text* user-name placeholder "山田太郎"]<p class="js-confirm"></p>
</dd>
</dl>

<dl class="form__item">
<dt class="form__label requied">電話番号（半角英数記号）</dt>
<dd class="form__desc">
[tel* tel placeholder "090-1234-5678"]<p class="js-confirm"></p>
</dd>
</dl>

<dl class="form__item">
<dt class="form__label requied">メールアドレス（半角英数記号）</dt>
<dd class="form__desc">
[email* email placeholder "temple@gmail.com"]<p class="js-confirm"></p>
</dd>
</dl>

<dl class="form__item">
<dt class="form__label requied">お問い合わせ内容</dt>
<dd class="form__desc">
[textarea* content]<p class="js-confirm"></p>
</dd>
</dl>

<div class="form__footer">
<p>
<a href="/privacy" target="_blank">プライバシーポリシー</a>をご確認の上、下記ボタンより先にお進みください。
</p>
</div>
<div class="form__btn">
<span class="form__btn-wrapper">[confirm class:btn "確認画面へ"][submit class:btn "送信する"]</span>
<span class="form__back-btn">[back class:form__back-input "入力内容を変更する"]</span>
</div>
```

</details>


### メールタブ設定

各入力欄にメールの送信設定を行います。
以下を参考に案件ごとに書き換えて使用してください。

| メール |  |
| ------------- | ------------- |
| 送信先  | 送信用アドレス |
| 送信元  | 送信名 <送信用アドレス>  |
| 題名  | ●●からのお問い合わせ |

<details>
<summary>メッセージ本文</summary>
━━━━━━□■□　お問い合わせ内容　□■□━━━━━━

・お問い合わせ内容の種類：[type]
・貴社名：[company_name]
・お名前：[user-name]
・電話番号︰[tel]
・メールアドレス：[mail]
・お問い合わせ内容：
[content]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━
</details>

---

| メール（2）自動返信メール |  |
| ------------- | ------------- |
| 送信先  | [email] |
| 送信元  | 送信名 <送信用アドレス>  |
| 題名  | お問い合わせ受け付け完了のお知らせ |

<details>
<summary>メッセージ本文</summary>

※このメールはシステムからの自動返信です

[user-name] 様

株式会社DEMOでございます。

以下の内容でお問い合わせを受け付けいたしました。
詳しい回答は、できる限り早急に担当よりご連絡差し上げます。
今しばらくお待ちくださいませ。

-----□■□ お問い合わせ内容 □■□-----

・お問い合わせ内容の種類：[type]
・貴社名：[company_name]
・お名前：[user-name]
・電話番号︰[tel]
・メールアドレス：[mail]
・お問い合わせ内容：[content]

----------------------------------------


——————————————————————————
【会社情報】
株式会社DEMO
住所：〒123-4567
東京都渋谷区渋谷1-1-1オーダービル1F
電話番号 01-1234-5678
——————————————————————————
</details>


### コンタクフォームを固定ページに出力する

コンタクトフォームが作成されるとショートコードが表示されます。
このコードを作成したお問い合わせの固定ページへ入れましょう。
お問い合わせは1つの固定ページで、入力・確認・完了ページ3ページ分を作ります。
最後にエディタ下の「固定ページクラス」に`contact`の入力を行います。

※コード内のクラス名はテンプレに合わせて変更してください。

<details>
<summary>お問い合わせ3P 記述例</summary>

```html

<section class="section js-contact-main">
<header class="section__header">
<h1 class="section__ttl">Contact<span class="section__ttl-ja">お問い合わせ</span></h1>
<p class="section__txt">このページからお問合せを受け付けております。<br>下記必須項目は必ず入力の上、お問合せ下さい。</p>
</header>
<div class="section__body">
<div class="form">
<div class="form__list">
<!-- ここに作成したコンタクトフォームのショートコードを入れる -->
[contact-form-7 id="40" title="コンタクトフォーム 1"]
</div>
</div>
</div>
</section>

<section class="section js-contact-complete">
<header class="section__header">
<h1 class="section__ttl section__ttl--complete">Contact<span class="section__ttl-ja">お問い合わせ</span></h1>
<div class="section__header-msg">
<h2>お問い合わせ送信完了</h2>
</div>
<div class="section__header-text section__header-text--complete">
<p>お問い合わせいただきありがとうございます。<br>後日、担当者からご連絡させていただきます。</p>
</div>
</header>

<div class="section__body">
<div class="form">
<div class="form__btn form__btn--complete">
<div class="form__btn-wrapper"><a class="btn btn--link" href="/">TOPに戻る</a></div>
</div>
</div>
</div>

</section>
```
</details>

## ■WordPress組み込み後チェック





## ■(Order2以降の内容-未完)ニュース一覧ページ作成

archive.phpに作成する方向です。

<details>
<summary>記述例（未完）</summary>

```php

<?php get_header(); ?> // header読み込み

<?php if(have_posts()) : while(have_posts()) : the_post(); ?>

// 1記事カード分のコードを入れる。日付・カテゴリー等のオプションは必要に応じて。
<div class="article">
 <h2><a href="<?php the_permalink(); ?>"><?php the_title(); ?></a></h2>
 <div class="date"><?php echo get_the_date('Y.m.d'); ?></div>
 <div class="category"><?php the_category(); ?></div>
 <div class="tag"><?php the_tags(); ?></div>
 <div class="sentence"><?php the_content(); ?></div>
</div>

// ページャー
<div class="pager">
 <div><?php previous_posts_link('前のページ'); ?></div>
 <div><?php next_posts_link('次のページ'); ?></div>
</div>

// 投稿記事がない場合の表示
<?php endwhile; else: ?>
  <div>お知らせがありませんでした。</div>
<?php endif; ?>

<?php wp_footer(); ?>

```
</details>