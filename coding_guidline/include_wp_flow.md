# WP制作事業 テーマ作成用WP組み込みフロー

**【Bokuravo 社内用】**
このテキストは、コーディングガイドラインに沿ってコーディングした静的HTMLサイトを、WPへ組み込むフローです。
コーディングガイドラインを確認する場合は、[こちら](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/tree/tsukada/coding_guidline)から確認できます。
また、ファイル作成の紹介コードは[株式会社サラ様](https://thorough-sol.co.jp/)のコードを流用させて頂いています。

## このフローのゴール

HTMLサイトをWPで組み込み、最終的にWEBブラウザで表示するまでがゴールです。

## 目次

[テーマフォルダ作成]()

[テンプレートファイル分割]()

[各ファイルの中身を作成]()

[固定ページ作成]()

[WordPress組み込み後チェック]()


## テーマフォルダ作成

テーマ名と同じ名前のフォルダを作成し以下のディレクトリ構成にします。

<details>
<summary>▼ディレクトリ構造</summary>

```text

[SingleA / StandardA]
  │
  ├ [src]
  │   ├ [scss]
  │   │   ├ [foundation]
  │   │   │    ├ reset.scss
  │   │   │    ├ _base.scss
  │   │   │    ├ _variable.scss
  │   │   │    └ _mixin.scss
  │   │   │
  │   │   ├ [common]
  │   │   │    ├ _header.scss
  │   │   │    ├ _footer.scss
  │   │   │    └ ( _main.scss )
  │   │   │
  │   │   ├ [page]
  │   │   │    ├ style.scss
  │   │   │    ├ privacy.scss
  │   │   │    ├ contact.scss
  │   │   │    │ ▼----- StandardA -----▼
  │   │   │    ├ about.scss
  │   │   │    └ news.scss
  │   │   │
  │   │   ├ [theme_color]
  │   │   │    ├ tc_blue.scss
  │   │   │    └ tc_green.scss
  │   │   │
  │   │   └ [admin]
  │   │        └ admin.scss
  │   │
  │   ├ [js]
  │   │  ├ common.js
  │   │  ├ top.js
  │   │  ├ contact.js
  │   │  └ 各JSライブラリ本体
  │   │
  │   ├ [image]
  │   │
  │   └ [pug]
  │       ├ index.pug
  │       ├ contact.pug
  │       ├ contact_confirm.pug
  │       ├ contact_complete.pug
  │       ├ privacy.pug
  │       │ ▼----- StandardA -----▼
  │       ├ about.pug
  │       ├ news.pug
  │       ├ news_detail.pug
  │       │
  │       ├ [_config] 
  │       │    └ _config.pug
  │       │
  │       ├ [_element]
  │       │    ├ _header.pug
  │       │    └ _footer.pug
  │       │
  │       └ [_layout]
  │            └ _default.pug
  │
  │
  └ [dist]
      ├ [html]
      │   ├ index.html
      │   ├ contact.html
      │   ├ contact_confirm.html
      │   ├ contact_complete.html
      │   ├ privacy.html
      │   │ ▼----- StandardA -----▼
      │   ├ about.html
      │   ├ news.html
      │   └ news_detail.html
      │   
      ├ [css]
      │   ├ reset.css
      │   ├ style.css
      │   ├ privacy.css
      │   ├ contact.css
      │   │ ▼----- StandardA -----▼
      │   ├ about.css
      │   ├ news.css
      │   │
      │   ├ [theme_color]
      │   │    ├ tc_blue.css
      │   │    └ tc_green.css
      │   │
      │   └ [admin]
      │        └ admin.css
      ├ [js]
      │  ├ common.bundle.js
      │  ├ top.bundle.js
      │  └ contact.bundle.js
      │
      └ [image]
```
</details>


## テンプレートファイル分割

テーマプランによって下層ページが異なるので、プランに合わせファイルを振り分けます。
それぞれPHPファイルを作成します。


### 【singleA】【StandardA】

トップ(index.html)：`front-page.php`
プラポリ(privacy.html)：`page.php(固定ページ)`
問い合わせTOP(contact.html)：`page.php(固定ページ)`
問い合わせ確認(contact_confirm.html)：`page.php(固定ページ)`
問い合わせ完了(contact_complete.html)：`page.php(固定ページ)`

### 【StandardA】

私達について(about.html)：`page.php(固定ページ)`
ニュース一覧(news.html)：`home.php`
ニュース詳細(news_detail.html)：`single.php`

<details>
<summary>▼なぜトップを`front-page.php`にするか</summary>

管理画面にはどのページをトップページにするかこのような表示設定があります。

![管理画面の表示設定](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/wp_admin_view_settings.png?raw=true)

PHPファイルにもトップページを表示可能なファイルが`index.php` `home.php` `front-page.php`と3つあります。

この3つのファイルには表示優先度がそれぞれ違います。

1. front-page.php（最優先）
2. home.php
3. index.php

それらの設定と、StandardAプランの様にニュース一覧ページも必要な場合それぞれファイルを分ける必要がありますので、

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


## 各ファイルを作成

以下のファイル・フォルダを空のまま作成します。

`functions.php`

`index.php`

`style.css`

`front-page.php`(トップページ表示)

`footer.php`(フッター)

`header.php`(ヘッダー)

`page.php`(固定ページ表示)

`single.php`(記事詳細)

`[parts]フォルダ > head.php` (head情報)

`[parts]フォルダ >  scripts.php` (JSファイル読み込み)


<details>
<summary>▼この時点のディレクトリ構成</summary>

```text

[SingleA / StandardA]
  │
  ├ front-page.php
  ├ functions.php
  ├ footer.php
  ├ header.php
  ├ index.php
  ├ page.php
  ├ single.php
  ├ style.css
  │
  ├ [parts]
  │  ├ scripts.php
  │  └ head.php 
  │
  ├ [src]
  │  └ ...省略
  └ [dist]
     └ ...省略
```
</details>

## style.cssにテーマ宣言

テーマを有効にするため、追加した`style.css`にテーマ情報を記述します。

最低限Theme Nameを入れておけば、管理画面のテーマ選択画面にてテーマを有効化出来るようになります。

その他のテーマ情報は、任意となりますが、既存のテーマファイルが存在している場合はその内容に従って入力します。

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

余談：
descriptionや管理画面内に「●●（自社名・自社サービス名）専用のWordPressテーマです」と明記してあると喜んでくださるクライアント様が多いようです。

このような細かくケアを行うと他社との差別化に繋がりますので、なるべく対応しましょう。


## 各ファイルの中身を作成


### functions.php作成

`functions.php`に以下をそのまま記述します。

```php

<?
```


### head情報作成

`[parts] > head.php`を開き、head情報をhtmlからコピペ後パスを書き換えます。

記述例

```php

// [parts] > head.php

<?php
  $themePath = get_template_directory_uri().'/dist/';
?>
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="keywords" content="士業,集客,コンサルティング,株式会社サラ">
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

`[parts] > scripts.php`を開き、JSファイルを読み込むコードを記述します。

```php
// [parts] > scripts.php

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

作成手順

1. functions.phpにナビゲーションメニューの有効化設定を書く
2. header.phpにヘッダーナビのコード出力タグを記述
3. 管理画面左メニュー > 外観 > メニュー からナビゲーションメニューを登録
4. 管理画面左メニュー > 外観 > ウィジェット から2をウィジェット化


#### 1. functions.phpにナビゲーションメニューの有効化設定を書く

詳細な説明は[こちら](https://wp-fan.com/wordpress/register-custom-menu/)

<details>
<summary>functions.phpの記述例</summary>

```php

//ナビゲーションを登録する
function register_my_menus() {
	register_nav_menus( array(
		//この中にカスタムメニューを定義する　 '場所' => '説明'
		'header' => 'ヘッダーナビゲーション',
		'footer' => 'フッターナビゲーション'
	));
}
//アクションフックを追加
add_action( 'after_setup_theme', 'register_my_menus' );
```
</details>


#### 2. header.phpにヘッダーナビのコード出力タグを記述

<details>
<summary>header.phpの記述例</summary>

```php

<?php
  $themePath = get_template_directory_uri().'/dist/'; // パス
  $postId = get_the_ID(); //投稿のID（数値）取得
  $pageClass = get_post_meta($postId, 'page-class', true); // bodyに付けるクラス
?>
<!DOCTYPE html>
<html lang="ja">
<?php get_template_part( 'parts/head' ); ?>// head情報読み込み
<body class='<?php echo $pageClass; ?>'>
  <div class="allwrap">
    <header class="header js-sticky">
      <div class="header__frame">
        <div class="header__frame_inner">
          <h1 class="header__logo">
            <a href="<?php bloginfo('url');?>">
              <img src="<?php echo $themePath; ?>img/logo_white.svg" class="header__logo_img" alt="株式会社サラ">
              <img src="<?php echo $themePath; ?>img/logo_navy.svg" class="header__logo_img--navy" alt="株式会社サラ" >
            </a>
          </h1>

          <button type="button" class="header__nav_hamburger sp">
            <span class="header__nav_hamburger_icon"></span>
          </button>
        </div>

        <!-- Navigation -->
        <nav class="header__nav" role="navigation" itemscope itemtype="http://schema.org/SiteNavigationElement">
          // logo
          <p class="header__nav_logo">
            <a href="<?php bloginfo('url');?>">
              <img src="<?php echo $themePath; ?>img/logo_white.svg" class="header__logo_img" alt="株式会社サラ" >
            </a>
          </p>

          <?php wp_nav_menu(
            array (
              //カスタムメニュー名
              'theme_location' => 'header__nav',
              //コンテナを表示しない
              'container' => false,
              //カスタムメニューを設定しない際に固定ページでメニューを作成しない
              'fallback_cb' => false,
              // 出力される要素の中のulにメニュークラスを付ける
              'menu_class' => 'header__nav_list',
            )
          ); ?>
         </nav>
         <!-- /Navigation -->
      </div>
    </header>

    <main class="m">
```
</details>

その後出力される`<ul>`の子要素`<li>`に任意のクラスを付けるには、管理画面から個別にクラスを付けます。

![管理画面から出力したグローバルメニューのliタグにクラスを付ける](https://gyazo.com/ceaf77a81b78442b3564d697f66cdf24)


#### 3. & 4. ナビゲーションメニューを登録、ウィジェット化

詳細は[こちら](https://design-plus1.com/tcd-w/faq/custom_menu.html)

HTMLタグもそのまま登録と出力することが可能です。

![メニュー登録にはHTMLタグも使用可能](https://gyazo.com/245d67ca5739b00338a20404319644c0)


### footer.php作成

`header.php`の作成と同じ要領で、footer部分のHTMLのコピー＆ペースト、
グローバルナビの設定を行います。
`</main>`の閉じタグを忘れずに記述します。

1. functions.phpにナビゲーションメニューの有効化設定を書く
2. footer.phpにフッターナビのコード出力タグを記述
3. 管理画面左メニュー > 外観 > メニュー からナビゲーションメニューを登録
4. 管理画面左メニュー > 外観 > ウィジェット から2をウィジェット化


#### 1. functions.phpにナビゲーションメニューの有効化設定を書く

詳細な説明は[こちら](https://wp-fan.com/wordpress/register-custom-menu/)

<details>
<summary>functions.phpの記述例</summary>

```php

//ナビゲーションを登録する
function register_my_menus() {
	register_nav_menus( array(
		//この中にカスタムメニューを定義する　 '場所' => '説明'
		'header' => 'ヘッダーナビゲーション',
		'footer' => 'フッターナビゲーション'
	));
}
//アクションフックを追加
add_action( 'after_setup_theme', 'register_my_menus' );
```
</details>


#### 2. footer.phpにヘッダーナビのコード出力タグを記述

<details>
<summary>footer.phpの記述例</summary>

```php

<?php
  $themePath = get_template_directory_uri().'/dist/';
?>
</main>
<footer class="footer">
  <div class="footer__wrap">
    <div class="ctr cont_ctr">
      <div class="footer__2col">
        <p class="footer__logo">
          <a href="<?php bloginfo('url');?>" class="footer__logo_link">
            <img src="<?php echo $themePath; ?>img/logo_white.svg" alt="株式会社サラ">
          </a>
        </p>

        <!-- Navigation -->
        <nav class="footer__nav" role="navigation" itemscope itemtype="http://schema.org/SiteNavigationElement">
          <?php wp_nav_menu(
            array (
              //カスタムメニュー名
              'theme_location' => 'footer__nav',
              //コンテナを表示しない
              'container' => false,
              //カスタムメニューを設定しない際に固定ページでメニューを作成しない
              'fallback_cb' => false,
              // 出力される要素の中のulにメニュークラスを付ける
              'menu_class' => 'footer__nav_list',
            )
          ); ?>
        </nav>
        <nav class="footer__nav">
          <ul class="footer__nav_list">
            <li class="footer__nav_item">
              <a href="<?php bloginfo('url');?>#news" class="footer__nav_link">
                <span class="footer__nav_text--main">NEWS</span>
                <span class="footer__nav_text--sub">お知らせ</span>
              </a>
            </li>
            <li class="footer__nav_item">
              <a href="<?php bloginfo('url');?>#message" class="footer__nav_link">
                <span class="footer__nav_text--main">MESSAGE</span>
                <span class="footer__nav_text--sub">代表挨拶</span>
              </a>
            </li>
            <li class="footer__nav_item">
              <a href="<?php bloginfo('url');?>#philosophy" class="footer__nav_link">
                <span class="footer__nav_text--main">PHILOSOPHY</span>
                <span class="footer__nav_text--sub">理念</span>
              </a>
            </li>
            <li class="footer__nav_item">
              <a href="<?php bloginfo('url');?>#service" class="footer__nav_link">
                <span class="footer__nav_text--main">SERVICE</span>
                <span class="footer__nav_text--sub">事業内容</span>
              </a>
            </li>
          </ul>
          <ul class="footer__nav_list">
            <li class="footer__nav_item">
              <a href="<?php bloginfo('url');?>#works" class="footer__nav_link">
                <span class="footer__nav_text--main">WORKS</span>
                <span class="footer__nav_text--sub">実績</span>
              </a>
            </li>
            <li class="footer__nav_item">
              <a href="<?php bloginfo('url');?>#company" class="footer__nav_link">
                <span class="footer__nav_text--main">COMPANY</span>
                <span class="footer__nav_text--sub">会社概要</span>
              </a>
            </li>
            <li class="footer__nav_item">
              <a href="<?php bloginfo('url');?>/contact" class="footer__nav_link">
                <span class="footer__nav_text--main">CONTACT</span>
                <span class="footer__nav_text--sub">お問い合わせ</span>
              </a>
            </li>
          </ul>
        </nav>
      </div>
      <p class="footer__privacy"><a href="<?php bloginfo('url');?>/privacy" class="footer__privacy_link">PRIVACY POLICY</a></p>
      <small class="footer__copy">©2020 THOROUGH All Rights Reserved.</small>
    </div>
  </div>
</footer>
</div>
<?php
  get_template_part( 'parts/scripts' );
  wp_footer();
?>

</body>

</html>
```
</details>


#### 3. & 4. ナビゲーションメニューを登録、ウィジェット化

`header.php`と同じ要領で作成します。


### front-page.php作成

`front-page.php`にファイル読み込みパスを記述します。

```php

<?php
  $themePath = get_template_directory_uri().'/dist/';
?>
```

次に上の記述の下に`<?php get_header(); ?>`を
一番最後に`<?php get_footer(); ?>`を記述します。

```php

<?php
  $themePath = get_template_directory_uri().'/dist/';
?>

<?php get_header(); ?>

<?php get_footer(); ?>
```

`<?php get_header(); ?>`の下に`[dist] > index.html`の`<main>`内のコードを全コピペします。

最後に`<img>` `<a>`タグのパスをそれぞれ変更します。

最終的にパスはこうなります。

```php

// front-page.php

<?php
  $themePath = get_template_directory_uri().'/dist/';
?>
<?php get_header(); ?> // header読み込み

// ---- ここに<main>タグ内のコンテンツ

// imgタグのパス変更
<img src="<?php echo $themePath; ?>img/image.jpg">

// aタグのパス変更
<a href="<?php echo $linkUrl; ?>">

// ---- ここまで<main>タグ内のコンテンツ

<?php get_footer(); ?> // footer読み込み
```


### index.php作成

index.phpは必須ファイルなためニュース一覧が必要ない場合でも中身を作成します。

```php

<?php
/*
トップページ用テンプレート
*/
get_header(); ?>

<?php get_footer(); ?>
```

<details>
<summary>ニュース一覧作成例</summary>

ヘッダーを出力する`<?php get_header(); ?>`
フッターを出力する`<?php get_footer(); ?>`

▼記述例

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

// 投稿記事がない場合の表示
<?php endwhile; else: ?>
  <div>お知らせがありませんでした。</div>
<?php endif; ?>

// ページャー
<div class="pager">
 <div><?php previous_posts_link('前のページ'); ?></div>
 <div><?php next_posts_link('次のページ'); ?></div>
</div>

<?php wp_footer(); ?>

```
</details>

## 固定ページ作成

`page.php`front-page.phpと同じ要領でヘッダー、フッターを用意。
コンテンツの中身はこれらのファイルの<main>タグの中身を管理画面から直接書きます。

privacy.html
contact.html
contact_confirm.html
contact_complete.html
about.html

## 投稿ページ作成



## WordPress組み込み後チェック