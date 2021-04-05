# WP制作事業 テーマ作成用WP組込フロー

**【Bokuravo 社内用】**

このテキストは、コーディングガイドラインに沿ってコーディングした静的HTMLサイトを、WPへ組み込むフローです。

[コーディングガイドライン](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/tree/tsukada/coding_guidline)はこちら

~~また、ファイル作成の紹介コードは[株式会社サラ様](https://thorough-sol.co.jp/)のコードを流用させて頂いています。~~

Order1-Aテーマが完成したので、参照コードは[Order1-A](https://github.com/SakiTsukada-Bokuravo/Order1-A)に差し替わります。


## ■このフローのゴール

HTMLサイトをWPで組み込み、最終的にWEBブラウザで表示するまでがゴールです。

## ■目次

[テーマフォルダ作成](include_wp_flow.md#%E3%83%86%E3%83%BC%E3%83%9E%E3%83%95%E3%82%A9%E3%83%AB%E3%83%80%E4%BD%9C%E6%88%90)

[テンプレートファイル分割](include_wp_flow.md#%E3%83%86%E3%83%B3%E3%83%97%E3%83%AC%E3%83%BC%E3%83%88%E3%83%95%E3%82%A1%E3%82%A4%E3%83%AB%E5%88%86%E5%89%B2)

[各ファイルを作成](include_wp_flow.md#%E5%90%84%E3%83%95%E3%82%A1%E3%82%A4%E3%83%AB%E3%82%92%E4%BD%9C%E6%88%90)

[style.css テーマ宣言](include_wp_flow.md#stylecss%E3%81%AB%E3%83%86%E3%83%BC%E3%83%9E%E5%AE%A3%E8%A8%80)

[各ファイルの中身を作成](include_wp_flow.md#%E5%90%84%E3%83%95%E3%82%A1%E3%82%A4%E3%83%AB%E3%81%AE%E4%B8%AD%E8%BA%AB%E3%82%92%E4%BD%9C%E6%88%90)

[functions.php](include_wp_flow.md#functionsphp%E4%BD%9C%E6%88%90)

[head.php](include_wp_flow.md#head%E6%83%85%E5%A0%B1%E4%BD%9C%E6%88%90)

[scripts.php](include_wp_flow.md#scriptsphp%E4%BD%9C%E6%88%90)

[header.php](include_wp_flow.md#headerphp%E4%BD%9C%E6%88%90%E3%83%98%E3%83%83%E3%83%80%E3%83%BC%E3%83%8A%E3%83%93%E8%A8%AD%E5%AE%9A)

[footer.php](include_wp_flow.md#footerphp%E4%BD%9C%E6%88%90)

[front-page.php](include_wp_flow.md#front-pagephp%E4%BD%9C%E6%88%90)

[front-page.php - お知らせ](include_wp_flow.md#%E3%83%88%E3%83%83%E3%83%97%E3%83%9A%E3%83%BC%E3%82%B8%E5%86%85%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9%E4%B8%80%E8%A6%A7%E4%BD%9C%E6%88%90)

[index.php](include_wp_flow.md#indexphp%E4%BD%9C%E6%88%90)

[page.php](include_wp_flow.md#pagephp%E4%BD%9C%E6%88%90)

[構造化マークアップの設定]()

WordPress組み込み後チェック


## ■テーマフォルダ作成

テーマ名と同じ名前のフォルダを作成し以下のディレクトリ構成にします。

<details>
<summary>ディレクトリ構造</summary>

```text

[Order1-A]
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

ヘッダー：`header.php`

フッター：`footer.php`

head：`parts/head.php`

Javascript関連：`parts/scripts.php`

プラポリ(privacy.html)：`page.php`

問い合わせTOP(contact.html)：`page.php`

問い合わせ確認(contact_confirm.html)：`page.php`

問い合わせ完了(contact_complete.html)：`page.php`

---
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

---


## ■各ファイルを作成

テーマプランに合わせ各HTMLファイルをどのPHPへ振り分けるか決まりました。

その後それぞれ空のPHPファイルを作成します。

ヘッダー、フッター等の共通コードはトップページのindex.htmlから作成します。

会社情報・プラポリ・お問い合わせ3ページ分は固定ページで作成するため、

固定ページ出力用のPHPファイル1つを用意します。

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
- header.php：ページごとの動的クラス作成
- footer.php
- front-page.php
- front-page.php：ニュース一覧作成
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
Theme Name: 株式会社DEMO様用テーマ
THeme URL: https://order1a.wpt-demo.com/
Description: これは株式会社DEMO様用テーマです。
Author: Bokuravo Inc.
AuthorURI: https://bokuravo.co.jp/
Version: 1.0
License: WordPress Theme, Copyright 2020 Bokuravo Inc. Order1-A is distributed under the themes of the GNU GPL and Split license.
License URI: GNU GPL Lv2:https://www.gnu.org/licenses/old-licenses/gpl-2.0.html / Split liesnce:スプリットライセンス表記のURL
*/
```


### functions.php作成

`functions.php`のコードです。
主にロゴ有効化設定、グローバルナビの設定等、管理画面メインメニューの表示切り替え設定があります。

「投稿画面で本文編集エリアを非表示」はニュース投稿ページ用のコードです。

```php

<?php
// ************************************************
//  カスタムロゴ
// ************************************************

// カスタムロゴ有効化設定
add_theme_support('custom-logo');


// ************************************************
//  ナビゲーション
// ************************************************
add_action( 'after_setup_theme', 'register_custom_menus' );

//ナビゲーションを登録する
function register_custom_menus() {
  register_nav_menus( array(
    //この中にカスタムメニューを定義 '場所' => '説明'
    'header_nav' => 'ヘッダーナビゲーション',
    'footer_nav' => 'フッターナビゲーション'
  ));
}

// ナビゲーションに説明が入力されていたら、サブタイトルとして表示
add_filter('walker_nav_menu_start_el', 'description_in_custom_nav_menu', 10, 4);
function description_in_custom_nav_menu($item_output, $item){
  return preg_replace('/(<a.*?>[^<]*?)</', '$1' . "<span class='h_nav__sub_text'>{$item->description}</span><", $item_output);
}

// ************************************************
//  固定/投稿ページ内の画像URL等の絶対パスを相対パスに変更
// ************************************************
add_filter('the_content','img_short_path');
function img_short_path($cont){
  $cont = str_replace('"image/', '"' . get_bloginfo('template_directory') . '/dist/image/', $cont);
  return $cont;
}

// ************************************************
//  投稿画面で本文編集エリアを非表示
// ************************************************
add_action( 'init' , 'my_remove_post_editor_support' );
function my_remove_post_editor_support() {
  remove_post_type_support( 'post', 'editor' );
}

// ************************************************
//  head内不要なタグを削除
// ************************************************
add_action( 'init' , 'head_Cleaneup' );

function head_Cleaneup() {
  // category feeds
  remove_action( 'wp_head', 'rsd_link' );
  // windows live writer(WP外部サービス利用時に情報取得に使うリンク)
  remove_action( 'wp_head', 'wlwmanifest_link' );
  // previous link(Microsoftが提供するブログエディター「Windows Live Writer」を使用する際のマニフェストファイルへのリンク生成を削除)
  remove_action( 'wp_head', 'wp_oembed_add_discovery_links' );
  remove_action('wp_head','rest_output_link_wp_head');
  remove_action('wp_head','wp_oembed_add_host_js');
  // Embed(ver4.4からのoembedに対応するWP記事URLの引用機能)
  remove_action( 'wp_head', 'parent_post_rel_link', 10, 0 );
  // start link
  remove_action( 'wp_head', 'start_post_rel_link', 10, 0 );
  // links for adjacent posts
  remove_action('wp_head', 'wp_print_styles', 8);
  // default cssの削除
  remove_action('wp_head', 'index_rel_link');
  // ページネーション rel="index" 削除
  remove_action( 'wp_head', 'adjacent_posts_rel_link_wp_head', 10, 0 );
  // WP version
  remove_action( 'wp_head', 'wp_generator' );
  // remove WP version from css
  remove_action('wp_head', 'feed_links', 2);
  // EditURI link
  remove_action('wp_head', 'feed_links_extra', 3);
  // post and comment feeds
  remove_action('wp_head', 'adjacent_posts_rel_link_wp_head', 10, 0);
  // 前へ、次へボタンのリンク
  remove_action('wp_head', 'print_emoji_detection_script', 7);
  // remove emoji
  remove_action('wp_print_styles', 'print_emoji_styles');
  // remove emoji style css
  wp_deregister_script('comment-reply');
}

// ************************************************
//  ADMIN - LEFT SIDE MENU
// ************************************************
add_action( 'admin_menu', 'remove_menus', 999 );

function remove_menus(){
  global $current_user;

  if(!($current_user->user_login=="tech_admin")) {
    remove_submenu_page( 'edit.php', 'edit-tags.php?taxonomy=category' ); // カテゴリー
    remove_submenu_page( 'edit.php', 'edit-tags.php?taxonomy=post_tag' ); // タグ
    remove_menu_page( 'edit-comments.php' ); //コメント
    remove_menu_page('edit.php?post_type=page' ); // 固定ページ
    remove_menu_page('edit.php?post_type=acf-field-group' ); // Advanced custom field
    remove_submenu_page('users.php', 'users.php'); // ユーザー一覧
    remove_menu_page( 'plugins.php' ); //プラグインメニュー
    remove_menu_page( 'tools.php' ); //ツールメニュー
    remove_submenu_page( 'themes.php', 'themes.php' ); // テーマ
    remove_submenu_page( 'themes.php', 'theme-editor.php' ); // テーマ直編集エディタ
    remove_submenu_page( 'themes.php', 'nav-menus.php' ); // メニュー
    remove_menu_page('wpcf7'); // お問い合わせ
    remove_menu_page('wp-structuring-markup/wp-structuring-markup.php'); // Schema.org
    remove_submenu_page('options-general.php', 'options-reading.php'); // 表示設定
    remove_submenu_page('options-general.php', 'options-writing.php'); // 投稿設定
    remove_submenu_page('options-general.php', 'options-media.php' ); // メディア設定
    remove_submenu_page('options-general.php', 'options-discussion.php'); // ディスカッション設定
    remove_submenu_page('options-general.php', 'options-permalink.php'); // パーマリンク設定
    remove_submenu_page('options-general.php', 'akismet-key-config'); // Akismet（アンチスパム）
    remove_submenu_page('options-general.php', 'rlrsssl_really_simple_ssl'); // SSL設定
    remove_submenu_page('options-general.php', 'options-privacy.php'); // プライバシーポリシー設定
  }
}
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
  <title><?php bloginfo('name');?></title>
  <link rel="canonical" href="<?php bloginfo('url');?>">
  <link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Noto+Sans+JP:wght@400;500;700&display=swap">
  <link rel="stylesheet" href="<?php echo $themePath; ?>css/reset.css">
  <link rel="stylesheet" href="<?php echo $themePath; ?>css/style.css">
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
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
<script src="<?php echo $themePath; ?>js/common.bundle.js"></script>

<?php if(is_front_page()) : ?> // TOPページであれば、以下のJSを読み込む
<script src="<?php echo $themePath; ?>js/top.bundle.js"></script>
<?php endif; ?>

<?php if(is_page('contact')) : ?> // 音合わせページページ遷移関連コード
<script>
  $(function(){
    var $formBackInput = $('.form__back-input');
    var $formBackBtn = $('.form__back-btn');
    var $formList = $('.form__list');
    var $selectWrap = $('.select-wrap');

    function confirmFn(){
      $('.form__item .form__desc').each(function(){
        var $this = $(this);
        var $inputHidden = $this.find('input[type="hidden"]');
        var val = $this.find('input[type="hidden"]').val();
        if(!$inputHidden.length){
          val = $this.find('textarea').val();
        }
        $this.find('.js-confirm').text(val).show();
      });
    }

    function checkBackBtn(){
      if($formBackInput.hasClass('wpcf7c-force-hide')){
        $formBackBtn.hide();
        $formList.removeClass('form__list--confirm');
        $selectWrap.removeClass('confirmed');
      }else{
        $formBackBtn.show();
        $formList.addClass('form__list--confirm');
        $selectWrap.addClass('confirmed');
        confirmFn();
      }
    }

    checkBackBtn();
    document.addEventListener( 'wpcf7submit', function() {
      setTimeout(function(){
        checkBackBtn();
      }, 500);
    });

    document.addEventListener( 'wpcf7mailsent', function() {
      window.scrollTo(0, 0);
      $('.js-contact-main').hide();
      $('.js-contact-complete').fadeIn();
    }, false );

    $('.wpcf7c-btn-back').on("click", function(){
      $formBackBtn.hide();
      $('.js-confirm').hide();
    });
  });
</script>
<?php endif; ?>
```


### header.php作成、ヘッダーナビ設定

まず完成例です。この後順に手順を説明します。

`header.php`にPHP用の記述、header部分のHTMLの記述、ヘッダーナビの表示設定をします。

```php
// header.php完成例

<?php
  $themePath = get_template_directory_uri().'/dist/';
  $postId = get_the_ID();
  $pageClass = get_post_meta($postId, 'page-class', true);
?>
<!DOCTYPE html>
<html lang="ja">
<?php get_template_part( 'parts/head' ); ?> // parts/head.phpを読み込む
<?php if(is_front_page()):?> // if文開始。TOPページの場合
<body class='top'>// bodyタグに「top」クラスを付与
<?php else : ?>// それ以外のページの時は
<body class='<?php echo $pageClass; ?>'>// 後に設定するカスタムクラスの値に応じてクラスを表示する
  <div class="allwrapper">
    <header class="h js-sticky">
      <div class="h_container">
        <p class="h_logo">
          <a class="h_logo__link" href="<?php bloginfo('url');?>"> // 管理画面で入力されてあるサイトURLを出力
          <?php // カスタムロゴの出力コード
            $custom_logo_id = get_theme_mod( 'custom_logo' );
            $logo = wp_get_attachment_image_src( $custom_logo_id , 'full' );
            if ( has_custom_logo() ) { // もしカスタムロゴ画像が入っていたら
              echo '<img src="' . esc_url( $logo[0] ) . '" alt="' . get_bloginfo( 'name' ) . '" class="h_logo__img">';
            } else { // カスタムロゴがなくテキストロゴが入っていたら
              echo get_bloginfo( 'name' );
            }
          ?>
          </a>
        </p>
        <button class="h_nav__hamburger sp_show"><span class="h_nav__hamburger_icon"></span></button>
        <nav class="h_nav">
          <?php // カスタムメニュー設定
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
            wp_nav_menu( $headerNav );0 // ヘッダーナビゲーションを出力
          ?>
        </nav>
      </div>
    </header>

    <main class="m">
```

**ヘッダーナビ作成手順**

1. functions.phpにナビゲーションメニューの有効化設定を書く
2. PHP側の出力設定を追加する（上記のコード）
3. 管理画面左メニュー > 外観 > メニュー からヘッダーナビゲーションを登録


### 1. functions.phpにナビゲーションメニューの有効化設定を書く

詳細な説明は[こちら](https://wp-fan.com/wordpress/register-custom-menu/)

functions.php内の以下のコードです。
このコードを書くことにより、初めて管理画面内でメニュー登録が行えるようになります。

`array()`内の`header_nav`、`footer_nav`はそれぞれ任意の名前に変更して構いませんが、
どのメニューか分かるように命名してください。

<details>
<summary>functions.php ナビゲーション設定の記述例</summary>

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


### 2. PHP側の出力設定

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


### 3.ナビゲーションメニューを登録

管理画面左メニュー > 外観 > メニュー

「新しいメニューを作成しましょう」のリンクをクリックし、メニューを新規作成します。
メニュー名には1で設定したメニュー名（ここではheader_nav）を入れましょう。
その後CSS class(オプション)に、HTML側のliタグの指定しているクラス名を入れます。

![管理画面から出力したグローバルメニューのliタグにクラスを付ける](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/li-add-class.png)

もしメニューに日本語＋英語等のサブタイトルが入る場合は「説明」のテキストエリアにサブタイトルのテキストを入力します。
完了後、メニューの出力位置にチェックをつけます。

![メニュー作成例](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/custommenu1.png?raw=true)

※上記の作成例のリンクは、アンカーリンクを指定しています。
※ヘッダー、フッター等でそれぞれ異なるスタイルのメニューが必要な場合は必要分メニューを作成します。


### footer.php作成

まずは完成例です。

先程の`header.php`と同じ要領でfooter.phpを作成します。

管理画面側のナビゲーション設定はヘッダーナビと同じ手順なため割愛します。

※コード内のクラス名はテンプレに合わせて変更してください。

<details>
<summary>footer.phpの完成例</summary>

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

以下完成例です。

コード量が多いため順に説明します。

<details>
<summary>footer.phpの完成例</summary>
```php

// front-page.php
<?php
	$themePath = get_template_directory_uri().'/dist/';
?>

<?php get_header(); ?>
<section class="first_view js-firstview">
	<div class="first_view__list">
		<div class="first_view__item">
			<figure class="first_view__image_box"><img class="first_view__image pc_show" src="<?php echo $themePath; ?>image/fv_image@2x.jpg" alt="ファーストビューイメージ"><img class="first_view__image sp_show" src="<?php echo $themePath; ?>image/fv_image_sp@2x.jpg" alt="ファーストビューイメージ"></figure>
			<div class="container wrapper first_view__container">
				<h1 class="first_view__catch">Site production<br>tailored to customers</h1>
				<p class="first_view__subcatch">Design / web template</p>
			</div>
		</div>
	</div>
	<p class="first_view__scroller"><span class="first_view__scroller_text">Scroll</span></p>
</section>
<section class="philosophy bg_white">
	<div class="container wrapper">
		<h2 class="philosophy__title">
			<p class="philosophy__title_text--sub">Philosophy</p>
			<p class="philosophy__title_text">選び続けられる価値のある<br>テーマを提供する</p>
		</h2>
		<div class="philosophy__detail">
			<p class="philosophy__detail_text">ここには1行推奨30〜35文字のテキストが入ります。ここには1行推奨30〜35文字のテキストが入ります。<br><br>ここには1行推奨30〜35文字のテキストが入ります。ここには1行推奨30〜35文字のテキストが入ります。<br><br>ここには1行推奨30〜35文字のテキストが入ります。ここには1行推奨30〜35文字のテキストが入ります。</p>
			<a class="main_button" href="<?php bloginfo('url');?>/about">View More</a>
		</div>
	</div>
</section>
<section class="service bg_gray" id="service">
	<div class="container wrapper">
		<h2 class="main_title">Service<span class="main_title--sub">事業内容</span></h2>
		<ul class="service__card">
			<li class="service_card__item">
				<figure class="service_card__image_wrapper"><img class="service_card__image" src="<?php echo $themePath; ?>image/card_image.jpg" alt="ここに画像が入ります。"></figure>
				<div class="service_card__body">
					<h3 class="service_card__title">見出しテキスト</h3>
					<p class="service_card__text">ここには1行推奨30〜35文字のテキストが入ります。ここには1行推奨30〜35文字のテキストが入ります。</p>
				</div>
			</li>
			<li class="service_card__item">
				<figure class="service_card__image_wrapper"><img class="service_card__image" src="<?php echo $themePath; ?>image/card_image.jpg" alt="ここに画像が入ります。"></figure>
				<div class="service_card__body">
					<h3 class="service_card__title">見出しテキスト</h3>
					<p class="service_card__text">ここには1行推奨30〜35文字のテキストが入ります。ここには1行推奨30〜35文字のテキストが入ります。</p>
				</div>
			</li>
			<li class="service_card__item">
				<figure class="service_card__image_wrapper"><img class="service_card__image" src="<?php echo $themePath; ?>image/card_image.jpg" alt="ここに画像が入ります。"></figure>
				<div class="service_card__body">
					<h3 class="service_card__title">見出しテキスト</h3>
					<p class="service_card__text">ここには1行推奨30〜35文字のテキストが入ります。ここには1行推奨30〜35文字のテキストが入ります。</p>
				</div>
			</li>
			<li class="service_card__item">
				<figure class="service_card__image_wrapper"><img class="service_card__image" src="<?php echo $themePath; ?>image/card_image.jpg" alt="ここに画像が入ります。"></figure>
				<div class="service_card__body">
					<h3 class="service_card__title">見出しテキスト</h3>
					<p class="service_card__text">ここには1行推奨30〜35文字のテキストが入ります。ここには1行推奨30〜35文字のテキストが入ります。</p>
				</div>
			</li>
		</ul>
	</div>
</section>
<section class="news bg_white" id="news">
	<div class="container wrapper">
		<h2 class="main_title">News<span class="main_title--sub">ニュース</span></h2>
		<ul class="news__list">

			<?php
				$args = array(
					'posts_per_page' => 3
				);
				$posts = get_posts( $args );
				foreach ( $posts as $post ):
				$postId = get_the_ID();
				$linkUrl = get_post_meta($postId, 'link_url', true);
				setup_postdata( $post );
			?>
			<?php if(empty($linkUrl)) : ?>
			<li class="news_list__item">
				<span class="news_list__inner">
					<time class="news_list__date"><?php the_time( 'Y.m.d' ); ?></time>
					<p class="news_list__text"><?php the_title();?></p>
				</span>
			</li>
			<?php else : ?>
			<li class="news_list__item">
				<a class="news_list__link" href="<?php echo $linkUrl; ?>">
					<time class="news_list__date"><?php the_time( 'Y.m.d' ); ?></time>
					<p class="news_list__text"><?php the_title();?></p>
				</a>
			</li>
			<?php endif; ?>

			<?php
				endforeach;
				wp_reset_postdata();
			?>
		</ul>
	</div>
</section>
<section class="contact theme_color">
	<div class="container wrapper">
		<h2 class="main_title main_title--white contact__title">Contact<span class="main_title--sub">お問い合わせ</span></h2>
		<p class="contact__text">お気軽にご相談ください</p><a class="contact__button" href="<?php bloginfo('url');?>/contact">お問い合わせはコチラ</a>
	</div>
</section>
<?php get_footer(); ?>
```
</details>

`front-page.php`にHTMLコーディングを行ったディレクトリ内のファイルを読み込むためのパスを記述します。

```php

<?php
  $themePath = get_template_directory_uri().'/dist/';
?>
```

この`get_template_directory_uri()`タグは、WP独自の関数で、動的にテーマディレクトリのパスを出力してくれます。

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

こうすることにより、ドメインが変わった場合でも自動で取得・出力してくれるため修正の手間が減ります。

最終的に全てのリンクパス、画像パスは以下のようになれば大丈夫です。

```php

// front-page.php

<?php
  $themePath = get_template_directory_uri().'/dist/';
?>
<?php get_header(); ?>

<section>

  // imgタグのパス
  <img src="<?php echo $themePath; ?>img/image.jpg">

  // aタグのパス
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

index.phpは必須ファイルなため空でも中身を作成します。

```php

<?php ?>
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

page.php 記述例

```php

<?php
/*
* Template Name: Order1-A theme
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

以下の入力例を参考に、入力エリアのタグを専用タグに書き換えます。

入力タグの次に`<p class="js-confirm"></p>`を1つ入れます。（確認ページのスタイル用に必要）

![コンタクトフォーム作成例](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/contactform1.png?raw=true)

<details>
<summary>コンタクトフォーム 記述例</summary>

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
Order1-Aデモサイトからお問い合わせがありました。

━━━━━━□■□　お問い合わせ内容　□■□━━━━━━

・貴社名：[company-name]
・お名前：[user-name]
・電話番号︰[tel]
・メールアドレス：[email]
・お問い合わせ内容：
[content]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
</details>

---

| メール（2）自動返信メール |  |
| ------------- | ------------- |
| 送信先  | [email] |
| 送信元  | Order1-Aデモサイト <info@order1a.wpt-demo.com>  |
| 題名  | お問い合わせ受け付け完了のお知らせ |

<details>
<summary>メッセージ本文</summary>

※このメールはシステムからの自動返信です。
ご返信いただいてもお答えできませんのでご了承ください。

[user-name] 様

Order1-Aテーマデモサイトでございます。
以下の内容でお問い合わせを受け付けいたしました。
詳しい回答は、できる限り早急に担当よりご連絡差し上げます。
今しばらくお待ちくださいませ。

-----□■□ お問い合わせ内容 □■□------------

・貴社名：[company-name]
・お名前：[user-name]
・電話番号︰[tel]
・メールアドレス：[email]
・お問い合わせ内容：[content]

----------------------------------------


——————————————————————————
【会社情報】
Order1-A
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

## ■WordPress管理画面側の設定

[Order1-A案件 テーマ作成フロー](/order1a_flow.md)を参考に、設定・確認を行います。



## ■(Order2以降の内容-未完)ニュース階層ページ作成

### ニュース一覧ページの作成

archive.phpに作成します。

<details>
<summary>記述例（WPラビット探偵用コードより）</summary>

```php

<!-- archive.php -->
<?php
// テンプレートがあるかをチェック
$url = $_SERVER['REQUEST_URI'];
$url = explode('?', $url);
$url = $url[0];

$path = get_template_directory() . substr($url, 0, strlen($url) - 1) . '.php';
if (file_exists($path)) {
    include($path);
    exit();
}

// index.phpを付加して検索
$path = get_template_directory() . $url . '/index.php';
if (file_exists($path)) {
    include($path);
    exit();
}
?>
<?php get_header(); ?>
<section class="archive archive_topic">
  <h2 class="h2">News<span>ニュース一覧</span></h2>
<?php if ( have_posts() ) : while ( have_posts() ) : the_post(); ?>
  <?php
  $loop
  ?>
   <?php the_posts_pagination(); ?>
<?php endwhile; ?>
<?php else : ?>
<p>まだ投稿された記事がないようです。</p>
</section>
<?php endif; ?>
<?php get_footer(); ?>
```
</details>


### ニュース詳細ページの作成

正式なデザインが決まっていないため、必要な内容を出力するコードを記載します。

### 出力する内容
- ページタイトル（post_typeによって表示分岐）
- ニュースタイトル
- 投稿日
- サムネイル画像有無によって表示分岐
- 本文表示

<details>
<summary>記述例（WPラビット探偵用コードより）</summary>

```php

<?php get_header(); ?>

// CSSは最低限のスタイリング用
<style>
.single_header {
  padding-top: 180px;
}
.single {
  margin-bottom: 40px;
}
.single_title {
  box-shadow: 0 1px 0 rgba(99,99,99,0.5);
  font-size: 24px;
}
.single_thumbnail {
  margin:40px auto;
  width: 100%;
}
.single img {
  height: auto;
  margin:0 auto;
}
</style>
<section class="single_header bg_white">
  <header class="container wrapper">
    <?php if (get_post_type() === 'topic'): ?>
      <h1 class="branch_main_title">News<span class="branch_main_title--sub">ニュース詳細</span></h1>
    <?php endif; ?>
  </header>
</section>
<article class="single single_<?php echo esc_attr(get_post_type()); ?> bg_white">
<?php if(have_posts()) : ?>
  <?php while(have_posts()) : the_post(); ?>
  <div class="container wrapper">
  <div class="single_head_info">
    <h1 class="single_title"><?php the_title(); ?></h1><!-- タイトルを表示 -->
    <p class="archive_date"><?php echo get_the_time('Y.m.d'); ?></p>
  </div>
  <?php if(get_the_post_thumbnail()) : ?>
  <figure class="single_thumbnail">
    <?php the_post_thumbnail( array(710, 533) ); ?>
  </figure>
  <?php endif; ?>
      <?php the_content(); ?><!-- 本文を表示 -->
    <?php endwhile; ?>
  <?php endif; ?>
  </div>
</article>
<?php get_footer(); ?>

```
</details>


## ■カスタム投稿タイプの作成

オーダーによっては、ニュース投稿ページの他に、違うカテゴリーで投稿ページを分けたいこともあるかもしれません。

そんなときは、カスタム投稿タイプ機能を使用します。

### 作成の大まかな流れ

1. カスタム投稿タイプをアクションフックに登録
2. カスタムタクソノミーをアクションフックに登録
3. article-{カスタム投稿タイプ登録名}.php 作成
4. single-{カスタム投稿タイプ登録名}.php 作成

### 1.カスタム投稿タイプをアクションフックに登録

次のようなコードをfunctions.phpに記述します。

手書きでは大変なため、便利なプラグイン（[Custom Post Type UI](https://ja.wordpress.org/plugins/custom-post-type-ui/)）を活用しましょう。


プラグインインストール後、以下の事項に沿って登録していきます。

たぶん以下の記述が最低限必要な事項と思われます。（抜け等あればご指摘ください）

<details>
<summary>functions.php内 カスタム投稿タイプの登録</summary>

```php

/*************************************************
カスタム投稿タイプ
まとめ(slug:matome)
*************************************************/
add_action( 'init', 'custom_post_type_matome');

function custom_post_type_matome() { 
	register_post_type( 'matome',
		array( 'labels' => array(
			'name' => __( 'まとめ' ),
			'singular_name' => __( 'まとめ' ),
			'all_items' => __( 'まとめ' ),
			'add_new' => __( '新規追加' ),
			'add_new_item' => __( 'まとめを新規投稿' ),
			'edit' => __( 'Edit' ),
			'edit_item' => __( 'まとめを編集' ),
			'new_item' => __( 'まとめを新規投稿' ),
			'view_item' => __( 'まとめを表示' ),
			'search_items' => __( 'まとめを検索' ),
			'not_found' =>  __( 'まとめが投稿されていません。' ),
			'not_found_in_trash' => __( 'ゴミ箱にまとめはありませんでした。' ),
			'parent_item_colon' => ''
			), /* end of arrays */
			'description' => __( 'まとめ 投稿機能です。' ),
			'public' => true,
			'publicly_queryable' => true,
			'exclude_from_search' => false,
			'show_ui' => true,
			'query_var' => true,
			'menu_position' => 5,
			'rewrite'	=> array( 'slug' => 'matome', 'with_front' => true ),
			'has_archive' => 'matome',
			'capability_type' => 'post',
			'hierarchical' => true,
      'supports' => array( 'title', 'editor', 'thumbnail', 'excerpt','revisions','sticky'),
      'map_meta_cap'=> true,
			'taxonomies' => array('matome_cat')//使用するタクソノミー
		) /* end of options */
  ); /* end of register post type */

  register_taxonomy(
    'matome_cat', // 「カスタムタクソノミー」を使用するオブジェクトタイプを指定します。
    'matome', // register_post_typeで登録したカスタム投稿タイプ名
    array(
      'label' => 'まとめカテゴリー',
      'labels' => array(
        'edit_item' =>'まとめカテゴリーを編集',
        'add_new_item' => '新規カテゴリーを追加',
        'search_items' => 'まとめカテゴリーを検索'
      ),
      'rewrite' => array('matome_cat' => 'matome'),
      'hierarchical' => true,
      'public' => true,
      'query_var' => true,
      'singular_label' => 'まとめカテゴリー',
      'show_in_rest' => true
    )
  );
}
```
</details>