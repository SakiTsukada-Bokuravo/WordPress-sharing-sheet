# WP制作事業 テーマ作成用WP組み込みフロー

**【Bokuravo 社内用】**
このテキストは、コーディングガイドラインに沿ってコーディングした静的HTMLサイトを、WPへ組み込むフローです。
コーディングガイドラインを確認する場合は、[こちら](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/tree/tsukada/coding_guidline)から確認できます。
また、ファイル作成の紹介コードは[株式会社サラ様](https://thorough-sol.co.jp/)のコードを流用させて頂いています。


## このフローのゴール

HTMLサイトをWPで組み込み、最終的にWEBブラウザで表示するまでがゴールです。

## 目次

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

  [page.php作成](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/tsukada/coding_guidline/include_wp_flow.md#pagephp%E4%BD%9C%E6%88%90)

  [各page-●●.php作成](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/tsukada/coding_guidline/include_wp_flow.md#%E5%90%84page-php%E4%BD%9C%E6%88%90)

WordPress組み込み後チェック


## テーマフォルダ作成

テーマ名と同じ名前のフォルダを作成し以下のディレクトリ構成にします。

<details>
<summary>ディレクトリ構造</summary>

```text

[Order1]
  │
  ├ [src] // HTML,CSSコーディング時の作業フォルダ
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
  └ [dist] // コンパイル後フォルダ
      ├ [html]
      │   ├ index.html
      │   ├ contact.html
      │   ├ contact_confirm.html
      │   ├ contact_complete.html
      │   ├ privacy.html
      │   ├ about.html
      │   ├ news.html
      │   └ news_detail.html
      │   
      ├ [css]
      │   ├ reset.css
      │   ├ style.css
      │   ├ privacy.css
      │   ├ contact.css
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


トップ(index.html)：`front-page.php`
プラポリ(privacy.html)：`page-privacy.php(固定ページ)`
問い合わせTOP(contact.html)：`page-contact.php(固定ページ)`
問い合わせ確認(contact_confirm.html)：`page-contact-confirm.php(固定ページ)`
問い合わせ完了(contact_complete.html)：`page-contact-complete.php(固定ページ)`


<details>
<summary>なぜトップを`front-page.php`にするか</summary>

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

`index.php`(※Order2以降ニュース一覧)

`style.css`

`front-page.php`(トップページ表示)

`footer.php`(フッター)

`header.php`(ヘッダー)

`page.php`(固定ページ表示)

`page-privacy.php`(プラポリ表示)

`page-contact.php`(問い合わせ入力表示)

`page-contact-confirm.php`(問い合わせ確認表示)

`page-contact-complete.php`(問い合わせ完了表示)

`single.php`(記事詳細※Order2以降作成する)

`[parts]フォルダ > head.php` (head情報)

`[parts]フォルダ >  scripts.php` (JSファイル読み込み)


<details>
<summary>この時点のディレクトリ構成</summary>

```text

[Order1]
  │
  ├ front-page.php
  ├ functions.php
  ├ footer.php
  ├ header.php
  ├ index.php
  ├ page.php
  ├ page-contact.php
  ├ page-contact-confirm.php
  ├ page-contact-complete.php
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

![管理画面から出力したグローバルメニューのliタグにクラスを付ける](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/li-add-class.png)


#### 3. & 4. ナビゲーションメニューを登録、ウィジェット化

詳細は[こちら](https://design-plus1.com/tcd-w/faq/custom_menu.html)

HTMLタグもそのまま登録と出力することが可能です。

![メニュー登録にはHTMLタグも使用可能](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/menu-settings.png)


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


### トップページ内ニュース一覧作成

`front-page.php`内に以下を記述し、投稿画面のプラグイン「アドバンスドカスタムフィールド」の「画面非表示」設定から「コンテンツエディタ」をチェックする。

![アドバンスドカスタムフィールド非表示設定](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/advanced-custom-field-hide-settings.png?raw=true)

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
トップページ用テンプレート
*/
get_header(); ?>

<?php get_footer(); ?>
```

### page.php作成

`page.php`を`front-page.php`と同じ要領でヘッダー、フッターを用意します。

<details>
<summary>page.php 記述例</summary>

<?php
/*
Template Name: お問い合わせ
*/
?>
 
<?php get_header(); ?>
  
 
<?php if(have_posts()): while(have_posts()):the_post(); ?>
  
  <h1><?php the_title(); ?></h1>
  
  <p><?php the_content(); ?></p>
  
<?php endwhile; endif; ?>
 
 
<?php get_footer(); ?>
</details>


### 各page-●●.php作成


`page-●●.php`の「●●」には固定ページで設定した「スラッグ名（パーマリンク）」か「ページID」が入りますが、
今回は分かりやすく「スラッグ名」を入れることにします。

作成手順

1. page-●●.phpの中身を作成
2. 固定ページ作成
3. パーマリンクを指定
4. エディタにコンテンツの中身をHTMLに入力

#### 1. page-●●.phpの中身を作成

`page.php`を作成した要領で、各page-●●.phpの中身も同じ様に作成します。

#### 2. 固定ページ作成

管理画面左メニュー > 固定ページ > 新規作成 ページタイトル入力

[固定ページ作成例](https://gyazo.com/8ec0708e2f8baaaacf20542dfff4d282)


#### 3. パーマリンクを設定

すでに作成してある`page-●●.php`の`●●`と同じ名称をパーマリンクに入力します。

[パーマリンクの設定例](https://gyazo.com/12b78db072a0278eaaebb7caba5659e2)

すると作成した`page-●●.php`が有効になり、
その固定ページのURLにアクセスすると`page-●●.php`の中身が表示されるようになります。


#### 4. エディタにコンテンツの中身をHTMLに入力

エディターのモードをテキストに変更し、作成したHTMLのメインコンテンツ部分をコピー＆ペーストします。

[エディターのモード](https://gyazo.com/eac1266cb8e017c14117a79dd387bc82)


コンテンツの中身はこれらのファイルの<main>タグの中身を管理画面から直接書きます。

`privacy.html`
`contact.html`
`contact_confirm.html`
`contact_complete.html`
`about.html`

## WordPress組み込み後チェック




<details>
<summary>(Order2以降の内容-未完)ニュース一覧ページ作成</summary>

<details>
<summary>記述例</summary>

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

</details>