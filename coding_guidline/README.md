# WP制作事業 テーマ作成用コーディングガイドライン

***【Bokuravo 社内用】***
WP制作事業におけるテーマ作成のコーディングガイドラインです。
主にSCSSを扱うことを前提にしています。
もしCSSを直接編集する場合、目次内に(SCSS)が付いている項目は飛ばして構いません。

## 目的

メンテナンス性に優れたHTML/CSS設計を行う事を第1とし、一定のコーディング品質を保つための指針となります。
実際の案件により、ガイドラインの内容と沿わないケースも出てくることも予想されます。
よってガイドラインの内容を一読しても疑問点が残る場合、またはガイドラインに沿わないケースがある場合はまずはチーム内で相談の上、ケースバイケースでご対応をお願いします。

## 目次

### 基本設計
#### 【HTML/CSS】
ディレクトリ構造
マージン
インデント
命名規則
メディアクエリ(SCSS)
ファイルのコンパイル、モジュール(SCSS)
再利用可能コンポーネント

#### 【Javascript】
Javascript用クラスの付け方
状態が変化するイベント用のクラス名
Javascriptファイルのモジュール化

## ディレクトリ構造

作業時のフォルダについて

以下をベースとしてディレクトリを作成してください。

CSS,SCSSに関し、FLOCSS（フロックス）のディレクトリ構造を一部参考にしています。

管理画面のCSSに関して、まだWP組み込み時のガイドラインが作成できていないため、仮で置いています。


```text:wp-content/themes/singleA

[singleA]
├ [css]
│   ├ reset.css
│   └ style.css
│
├ [scss]
│   ├ [foundation] // サイト全体のデフォルトスタイル管理 ※_が頭に付いているSCSSはreset.cssにまとめる。
│   │    ├ reset.scss
│   │    ├ _base.scss // サイト構成の基盤となるHTML直指定のスタイル（pタグのline-height等）
│   │    ├ _variable.scss // 変数
│   │    └ _mixin.scss
│   │
│   ├ [common] // サイトの共通部分管理
│   │    ├ _header.scss
│   │    ├ _footer.scss
│   │    └ ( _main.scss ) // 不要なら作成しない※後述
│   │
│   ├ [page]
│   │    ├ style.scss
│   │    ├ privacy.scss // プラポリ
│   │    ├ contact.scss // お問い合わせ（入力・確認・完了）
│   │    ▼----- SingleA -----▼
│   │    ├ about.scss // 私達について
│   │    └ news.scss // ニュース（一覧・詳細）
│   │
│   ├ [theme_color] // 1ページ単位でのテーマカラー変更用のスタイル管理
│   │    ├ tc_blue.scss
│   │    └ tc_green.scss
│   │
│   └ [admin] // ※現段階で仮置き。管理画面カスタマイズ用CSS
│        └ admin.scss
│
├ [js]
│  ├ common.bundle.js // サイト全体で適応するJS
│  ├ top.bundle.js // ページごとに適用するJS
│  └ 各JSライブラリ本体
│
└ [html]
   ├ index.html
   ├ contact.html
   ├ contact_confirm.html
   ├ contact_complete.html
   ├ privacy.html
    ▼----- SingleA -----▼
   ├ about.html
   ├ news.html
   └ news_detail.html
```

#### _reset.scss

ブラウザのデフォルトのスタイルをリセットするcssを定義します。
SCSSを扱う場合は、コンパイル時reset.cssファイルにまとめてください。
使用するリセットCSS：[ress.css](https://github.com/filipelinhares/ress)

#### _base.scss

サイト構成の基盤となるスタイルを定義。基本的にHTMLタグ自体にスタイルを定義します。

#### _variable.scss

サイト全体で使う変数を管理。

#### _mixin.scss

サイト全体で使うmixinを管理。

#### header.scss

サイト全体で使うヘッダースタイル。

#### footer.scss

サイト全体で使うフッタースタイル。

#### main.scss

ヘッダー・フッター以外にサイト全体で使うスタイルで、ヘッダー、フッター以外のサイト全体スタイルを定義する場合に作成してください。

#### [page]フォルダ内SCSS

`style.scss`：サイトTOPページ、メインコンテンツのスタイル。
`privacy.scss`：プライバシーポリシー用スタイル。
`contact.scss`：お問い合わせ（入力・確認・完了ページ）

#### ※スタンダードＡ用スタイル

シングルＡ作成時の場合不要。


## マージン

- 上下間のマージン：`margin-bottom`で余白を統一して付ける。
- 左右間のマージン：`margin-right`で余白を統一して付ける。

## インデント

HTML/CSS共に半角スペース2つで統一。

## 命名規則

(MindBEMding)[https://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/]を元に

親要素：Block

子要素：Element

子要素の別パターン：module

主に上記の3つに分類します。

BlockとElementの区切りにはアンダーバー2つ`__`で区切り、

子要素の別パターンにはハイフン2つ`--`で区切ります。


```css:CSS

.block__element--modifire {}

```

### その他事項

- クラス名に大文字は使用しないでください。
- CSSの指定セレクタはクラス名にし、なるべくHTMLタグ、idを指定しないでください。（※例外：JSのイベントを適応する場合やアンカーリンク指定はid付与OK）
- CSSにはなるべく2つ以上のクラス名にしないでください。（※例外：後述のJS状態変化のクラスには使用OK）
- `!important`はなるべく使用しないでください。
- CSSセレクタの優先度を一定に統一するため、2つ以上のクラスはなるべく使用しないでください。
- セマンティックなクラス名にしてください。（後述）
- 複数の英単語を繋げたクラス名にする時はスネークケース（アンダーバー1つ）で単語を繋いでください。（後述）

```scss:CSS

Bad
p {} // リセット・全体の調整以外に使用しない。
#parent {} // アンカーリンク・JS用以外にはなるべく使用しない。
p.parent {} // HTMLタグは使用しない。
.parent p {} // HTMLタグは使用しない。
.parent-child {} // JSとの差別化のためにハイフンは使用しない。
.parent .parent__child {} // 2つ以上指定しない。

Good
.parent {}
.parent__child_text {}
```

#### セマンティックなクラス名とは

クラス名は他の開発者が見て判断出来るよう役割に応じたクラス名にし、

使用する英単語はなるべく省略せず、クラス名を見てどこのパーツか、他の開発者にも伝わるよう命名してください。

```scss:CSS

Bad // 意味が分かりにくい。
.col_xl_3 {}

Good // どの配置のパーツか把握しやすい。
.parent_card {}
.parent_card__text {}
.parent_card__text--red {}
```

#### 複数の英単語を繋げたクラス名にする時
スネークケースにします。

子要素がある場合以下のGoodモデルのように付与します。

```css:CSS

Bad
.parent-card {} // ハイフンは使用しない
.parentCard {} // キャメルケースは使用しない

Good
.parent_card {} // 親要素
.parent_card__text {} // 親要素「parent_card」の子要素
```

## メディアクエリ(SCSS)

`_mixin.scss`にてメディアクエリ、ブレイクポイントを一括管理し、使用するSCSSファイルで呼び出します。
`()`内が未指定の場合はデフォルトの値が入ります。

```scss:呼び出したいSCSS

@include mediaquery() {
  .parent {
    // ここにCSSプロパティを記述
  }
}

```

`()`内のデフォルトの値を変更する場合

`_mixin.scss`を確認し、必要なメディアクエリの値を確認します。


```scss:呼び出したいSCSS

@include mediaquery(max-480) { // ここに別のメディアクエリの指定値を記述
  .parent {
    // ここにCSSプロパティを記述
  }
}

```


## 再利用可能コンポーネント

リセットCSSやサイト全体のレイアウトを決めるための基本スタイル以外は、

ページが増加するにつれCSS管理が複雑になるため、基本的に再利用可能なコンポーネント（小さいボタンやブロック）を作らないでください。

ページ単位でCSSファイルを作成し、CSSの影響範囲を管理してください。


## ファイルのコンパイル、モジュール(SCSS)

SCSSはgulpでモジュール化します。
CSSへコンパイルする時の改行位置はオプションを`extend:nested`に変更してください。

```css:コンパイル後のCSS

Bad
.parent {
  color:red; }

.parent { color:red; }

Good
.parent {
  color:red;
}
```


## Javascript

### Javascript用クラスの付け方

どのクラスがJSイベントと連携しているか明らかにするため、クラス名の頭に`.js`を付けます。

CSS用のクラスと差別化を図り可読性向上のために英単語の繋ぎにハイフンを使用し、

`.js-`が付くクラスには原則CSSを付けません。


```html:HTML

Bad
<div class="parent_card js_animation">
  <p class="parent_card__text">TEXT</p>
</div>

Good
<div class="parent_card js-animation">
  <p class="parent_card__text">TEXT</p>
</div>
```


### 状態が変化するイベント用のクラス名

スクロール連動等で状態が変化する場合のJSクラス名は`.is-active`のように`.is-●●`を付けてください。

`.is-●●`自体にCSSを定義せず、必ずそのパーツのクラスとJSイベント用クラスセットでCSSを付与するようお願いします。


```html:HTML

Bad
<!-- ".parent_card"自体にJSイベントを紐付けない。（どれにJSのイベントが紐付いているか分からない） -->
<div class="parent_card">
  <p class="parent_card__text">TEXT</p>
</div>

Good 
<!--「js-fade-in」を付与することになり、「js-fade-in」がイベント自体の発火クラス、「is-active」で活性・非活性を切り替えるのが分かる。-->
<div class="parent_card js-fede-in is-active">
  <p class="parent_card__text">TEXT</p>
</div>
```

```scss:CSS

.parent_card {
  background: #000;
}

Bad
.is-active { // その他このクラス名が付いているHTMLも一緒に変化してしまう。
  background: #fff;
}

Good 
.parent_card.is-active { // これなら「.is-active」を使い回しても他のCSSに影響しない。
  background: #fff;
}
```

### Javascriptファイルのモジュール化

最終的にgulp,webpackでモジュール化をお願いします。

サイト全体で活用するファイルと個々のページごとに使用するファイルに分別してください。

```html:HTML

<script src="common.js"></script><!-- サイト全体用 -->
<script src="top.js"></script><!-- 個々のページ用（この場合はトップページ） -->
```