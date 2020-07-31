# WP制作事業 テーマ作成用WP組み込みフロー

**【Bokuravo 社内用】**
このテキストは、コーディングガイドラインに沿ってコーディングした静的HTMLサイトを、WPへ組み込むフローです。
コーディングガイドラインを確認する場合は、[こちら](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/tree/tsukada/coding_guidline)から確認できます。

## このフローのゴール

HTMLサイトをWPで組み込み、最終的にWEBブラウザで表示するまでがゴールです。

## 目次

[テーマフォルダ作成]()

[各ファイルをテーマフォルダにコピー＆読み込み]()

[テーマ宣言]()

[index.php作成]()

[外部ファイルパスを変更]()

[テンプレートファイル分割]()

[固定ページ作成]()

[投稿ページ作成]()

[WordPress組み込み後チェック]()


## テーマフォルダ作成

テーマ名と同じ名前のフォルダを作成します。

コーディングガイドラインに沿ってコーディングし終わっている場合、以下のような構成になっているかと思います。


<details>
<summary>ディレクトリ構造</summary>
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

## 各ファイルをテーマフォルダにコピー＆読み込み

まず`[dist]`内の`[css]` `[js]` `[image]`フォルダをすべてテーマフォルダにコピペします。
`functions.php` `index.php` `style.css` この３つの空ファイルを作成します。

### CSSとJSを読み込む

`functions.php`を開き、テーマフォルダに格納した`[css]` `[js]`を読み込むコードを記述します。

```php
// functions.php

function my_scripts() {
  wp_enqueue_style( 'style-name', get_template_directory_uri() . '/css/ファイル名.css', array(), '1.0.0', 'all' );
  wp_enqueue_script( 'script-name', get_template_directory_uri() . '/js/jsファイル名.js', array( 'jquery' ), '1.0.0', true );
  wp_enqueue_script( 'script-name', 'https://code.jquery.com/jquery-3.5.1.js', array(), '1.0.0', true ); // 外部URLを直接読み込む場合
}
add_action( 'wp_enqueue_scripts', 'my_scripts' );
```

上記のようにCSS,JSを読み込ませます。

jQuery本体はWP側で予め読み込まれますので記述は不要ですが、バージョンを指定する場合は別途記述する必要があります。

jQueryを読み込む必要がないライブラリの場合は、`array()`と空白にします。

その横の`'1.0.0'`は任意のバージョン番号です。（キャッシュ対策等も含まれます）

## テーマ宣言

テーマを有効にするため、追加した`style.css`にテーマ名を記述します。

```scss
/*
Theme Name: 任意のテーマ名
*/
```

## index.php作成

## 外部ファイルパスを変更

## テンプレートファイル分割

## 固定ページ作成

## 投稿ページ作成

## WordPress組み込み後チェック