# WP制作事業 テーマ作成用コーディングガイドライン

***【Bokuravo 社内用】***
WP制作事業におけるテーマ作成のコーディングガイドラインです。

## 目的

メンテナンス性に優れたHTML/CSS設計を行う事を第1とし、一定のコーディング品質を保つための指針となります。
実際の案件により、ガイドラインの内容と沿わないケースも出てくることも予想されます。
よってガイドラインの内容を一読しても疑問点が残る場合、またはガイドラインに沿わないケースがある場合はまずはチーム内で相談の上、ケースバイケースでご対応をお願いします。

## 目次

基本設計
【HTML/CSS】
1. ディレクトリ構造
2. マージン
3. インデント
4. 命名規則
5. 再利用可能コンポーネント

【Javascript】
6. Javascript用クラスの付け方

## 1. ディレクトリ構造

作業時のフォルダについて。
CSS,SCSSに関しFLOCSS（フロックス）のディレクトリ構造を参考に、以下をベースとして環境構築する。


```text:wp-content/themes/singleA

[project]
├ [css]
│   ├ reset.css
│   └ style.css
│
├ [scss]
│   ├ [foundation] // サイト全体のデフォルトスタイル管理 ※_が頭に付いているSCSSはreset.cssにまとめる。
│   │     ├ reset.scss
│   │     ├ _base.scss // サイト構成の基盤となるHTML直指定のスタイル
│   │     ├ _variable.scss // 変数
│   │     └ _mixin.scss
│   │
│   ├ [common] // サイトの共通部分管理
│   │    ├ _header.scss
│   │    ├ _footer.scss
│   │    └ ( _main.scss ) // 不要なら作成しない※後述
│   │
│   ├ [pages]
│   │    ├ style.scss
│   │    ├ privacy.scss // プラポリ
│   │    ├ contact.scss // お問い合わせ（入力・確認・完了）
│   │    ----- SingleA -----
│   │    ├ about.scss // 私達について
│   │    └ news.scss // ニュース（一覧・詳細）
│   │
│   ├ [theme_colors] // 1ページ単位でのテーマカラー変更用のスタイル管理
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
├ [html]
   └ index.html
```

#### _reset.scss

ブラウザのデフォルトのスタイルをリセットするcssを定義する。
SCSSを扱う場合は、コンパイル時reset.cssファイルにまとめる。
使用するリセットCSS：[ress.css](https://github.com/filipelinhares/ress)

#### _base.scss

サイト構成の基盤となるスタイルを定義。基本的にHTMLタグ自体にスタイルを定義する。

#### _variable.scss

サイト全体で使う変数を管理。

#### _mixin.scss

サイト全体で使うmixinを管理。

#### header.scss

サイト全体で使うヘッダースタイル。

#### footer.scss

サイト全体で使うフッタースタイル。

#### main.scss

ヘッダー・フッター以外にサイト全体で使うスタイルで、ヘッダー、フッター以外のサイト全体スタイルを定義する場合に作成する。

#### [page]フォルダ内SCSS

`style.scss`：サイトTOPページ、メインコンテンツのスタイル。
`privacy.scss`：プライバシーポリシー用スタイル。
`contact.scss`：お問い合わせ（入力・確認・完了ページ）

#### ※スタンダードＡ用スタイル

シングルＡ作成時の場合不要。


## 2. マージン

- 上下間のマージン：`margin-bottom`で余白を統一して付ける。
- 左右間のマージン：`margin-right`で余白を統一して付ける。

## 3. インデント

HTML/CSS共に半角スペース4つで統一する。

## 4. 命名規則

(MindBEMding)[https://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/]を元に「Block」「Element」「module」に分けクラスを付ける。
※以前社内コーディング講習でBEM(MindBEMding)から更に独自のルールを決めていたが、一般的な規則に沿うものとする。

- クラス名に大文字は使用しない。
- CSSの指定セレクタはクラス名にし、HTMLタグを指定しないこと。
- なるべく2つ以上のクラス名にしないこと。（※例外：Javascriptの使用でidを付ける）
- CSSセレクタの優先度を一定に統一する。
- `!important`は使用しない。
- セマンティックなクラス名にする。
- 複数の英単語を繋げたクラス名にする時はスネークケースで単語を繋ぐ。

```css:CSS

Good
.text {}

Bad
p {}
#parent {}
p.parent {}
.parent .child {}
```

#### セマンティックなクラス名にする

クラス名は他の開発者が見て判断出来るよう役割に応じたクラス名にし、
使用する英単語はなるべく省略せず、クラス名を見てどこのパーツか、他の開発者にも伝わるよう命名する。

```css

Good // どのレイアウトのスタイルか、想像がつきやすい。
.company_card {}
.company_card__text {}
.company_card__text--red {}

Bad // Bootstrap上ではよく使われる「レイアウト」を定義する以下のクラス名は、理解するのに時間がかかる。
.col_xl_3 {}
```

#### 複数の英単語を繋げたクラス名にする時
スネークケースにする。
（英単語の繋ぎにアンダーバーを使用する。）

```css

Good
.company_card {}

Bad
.company-card {}
```

## 5. 再利用可能コンポーネント

ページが増加するにつれCSS管理が複雑になるため、原則再利用可能なコンポーネント（小さいボタンやブロック）を作らず、
なるべくページ単位でCSSの影響範囲を留める。


## 6. ファイルのモジュール化

SCSS,JS両方モジュール化する（まとめる）。


## 7. Javascript用クラスの付け方

どのクラスがJSイベントと連携しているか明らかにするため、クラス名頭に`.js`を付ける。
加えてCSS用のクラスと差別化を図り可読性向上のために英単語の繋ぎにハイフンを使用し、
`.js-`が付くクラスには原則CSSを付けない。


```html:HTML

Good
<div class="company_card js-drawer">
  <p class="company_card__text">TEXT</p>
</div>

Bad
<div class="company_card js_drawer">
  <p class="company_card__text">TEXT</p>
</div>
```


###  状態が変化するイベント用のクラス名

スクロール連動等で状態が変化する場合のJSクラス名は`.is-●●`を付ける。
原則`.is-●●`自体にCSSを定義せず、必ずそのパーツのクラスとJSイベント用クラスセットでCSSを付与する。


```html:HTML

Good // js-fade-inがイベント自体の発火クラス、is-activeで活性・非活性を切り替え
<div class="company_card js-fede-in is-active">
  <p class="company_card__text">TEXT</p>
</div>

Bad // ".company_card"自体にJSイベントを紐付けない。
<div class="company_card">
  <p class="company_card__text">TEXT</p>
</div>
```

```css:CSS
// 通常時
.company_card {
  color: black;
}

Good // 活性時
.company_card.is-active {
  color:red;
}

Bad
.is-active {
  // その他このクラス名が付いているHTMLも一緒に変化してしまう。
}
```