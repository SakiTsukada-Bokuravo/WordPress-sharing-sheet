# Order1-A案件 テーマ作成の概要

オーダー1AのWP環境を丸々お客様サーバーへ複製し終わった段階を前提としたフローです。


## おおまかな全体フロー

### 0. サーバー初期設定

### 1. WP初期構築

### 2. プラグイン、テーマの確認

### 3. 文章の流し込み・画像の差し替え

### 4. サイト基本設定

### 5. デバッグ

### 6. お客様確認

### 7. 納品

---

# 0. サーバー初期設定

フローチャートは[こちら](https://docs.google.com/spreadsheets/d/1vnjguUUQbdmg-3hvyj0N5llYH4ideWvkqBQC06L2CBs/edit#gid=920163801)に記載しています。  
不明点あれば、エンジニアに確認をお願いします。  

# 1. WP初期構築

WP初期インストール時に自社で管理・メンテナンスするためのアカウントと、お客様用アカウントを作成します。

アカウントはそれぞれ統一してください。

```text
◆自社用アカウント

ユーザー名：tech_admin
パスワード：登録時WP側でランダム生成される文字列


◆お客様用アカウント

ユーザー名：ドメイン名_admin
パスワード：登録時WP側でランダム生成される文字列
```

```text
WP環境を複製した場合、既存のアカウントIDと登録メールアドレスをDB上で直接操作してお客様アカウントにすることも可能です。
その場合、ユーザー登録完了メールが送信されないため、WPログイン情報等と一緒にメールで案内してください。
操作方法が不明な場合は次の「1-1. お客様用アカウントの作成」を行った後、
もともとある「order1a_admin」アカウントを削除してください。
```

## 1-1. お客様用アカウントの作成

自社用アカウントで管理画面にログイン後、メインメニューのユーザーから新規追加を選択します。

「新規ユーザーを追加」の項目にお客様用ユーザー名と、お客様のメールアドレスを入力し、権限グループを「管理者」にします。

「確認メールを省略」（※1）はチェックをし作成を行ってください。

正常に登録が完了すると、このようにユーザー登録が完了した旨のメールがお客様のメールアドレス宛に送られます。

![ユーザー登録完了メール例](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/user1.jpg?raw=true)

```text
（※1）：通常のサービスサイトのように、ユーザー登録の有効化を行うためのメール処理ですが、
最終的に登録完了後、お客様のメールアドレス宛に「ユーザー名」「パスワード」「ログインURL」が上記画像のように送信されるため、
お客様確認の手間を省く観点からチェックを入れるようにしています。
```

# 2. プラグイン、テーマの確認

確認する順番はどちらからでも大丈夫ですが、例ではテーマから確認していきます。

まずテーマが有効になっているか、サイトを表示して確認します。

もしテーマがオーダー1Aで有効になっていなかった場合は、管理画面の外観からテーマを選択し有効化してください。

次に各プラグインが正常に管理画面内に入っていて、有効化されているか確認します。

今後運用していく上で、プラグインの種類が増減する可能性がありますので、最終的にはデモサイトを参考にお願いします。

### 確認するプラグインリスト（増減有るかも）
```text
・ Advanced Custom Fields
・ Akismet Anti-Spam (アンチスパム)
・ Classic Editor
・ Contact Form 7
・ Contact Form 7 add confirm
・ Really Simple SSL
```

> 「TypeSquare Webfonts for エックスサーバー」
> オーダー1Aではこのプラグインを使用していないため、無効化のままで大丈夫です。（XサーバーでWPインストール時に自動導入されるプラグインです）

# 3. 文章の流し込み・画像の差し替え

各PHPファイルを編集し、該当文章の流し込みと画像の差し替えを行います。
もしPHPファイルからページが確認できない場合は、一旦htmlファイルで見た目確認後、PHPへコピペしてください。
完了したら、更新ファイルをサーバーへアップロードします。

### ★画像が不要な箇所がある場合

**例1：会社情報 代表挨拶写真**

クラス`msg__body`に対し、`msg__body--1col`を追加します。
`<figure class="msg__body_img"> ~ </figure>`の1文を削除またはコメントアウトしてください。

```html

<!-- 作業例 -->
<div class="msg__body msg__body--1col">
  <!--<figure class="msg__body_img"><img src="../image/about_msg.jpg" alt="代表写真"></figure> -->
  <div class="msg__body_dtl">
    <h3 class="msg__body_title">課題を発見し、<br class="sp_show">挑戦し続ける姿勢を大事に</h3>
    <p class="msg__body_text">ここには1行推奨30〜35文字のテキストが入ります。ここには1行推奨30〜35文字のテキストが入ります。ここには1行推奨30〜35文字のテキストが入ります。ここには1行推奨30〜35文字のテキストが入ります。ここには1行推奨30〜35文字のテキストが入ります。</p>
    <p class="msg__body_name"> <span class="msg__body_name--position">代表取締役社長</span>小田　一</p>
  </div>
</div>
```

# 4. サイト基本設定

## 4-1. 設定 > 一般設定

顧客情報に合わせて以下の変更をお願いします。
- サイトタイトル
- キャッチフレーズ（ディスクリプションにあたる）

## 4-2. ロゴ設定

外観 > カスタマイズからオーダー1Aのテーマカスタマイズ画面へ移動し、
「サイト基本情報」リンクから編集を行います。

「画像ロゴ」「ロゴを選択」からアップロードし公開
テキストロゴ：「サイトタイトル」からタイトルを入力

**※画像ロゴ、テキストロゴ両方設定されていた場合は、画像ロゴの表示が優先的になります。**


## 4-3. カスタムフィールド > フィールドグループ

これらのフィールド設定があるか確認します。

- ニュースリンク
- 固定ページクラス

### 4-3-1. ニュースリンク

ラベル：投稿ページに表示する項目名になります。日本語設定可能。
名前：投稿ページからサイトへ出力するために渡す変数名。英数字のみ。
タイプ：出力するデータの種類を設定します。

![ニュースリンクのフィールド設定](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/acf1.jpg?raw=true)

### 4-3-2. 固定ページクラス

ニュースリンクと同様に設定を行いますが、フォームタイプと位置設定の右端を「固定ページ」へ変更します。

![固定ページクラスのフィールド設定](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/acf2.jpg?raw=true)

![固定ページクラスのフィールド設定(位置)](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/acf-position.jpg?raw=true)

## 4-4. グローバルメニュー設定

メインメニュー 外観 > メニューより、メニュー設定の確認と変更を行います。

![メニュー設定](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/menu1.jpg?raw=true)

以上の状態（画像ではフッターナビ選択後の状態）になっていると思いますが、もしヘッダーナヒゲーション、フッターナビゲーションがそれぞれ存在していない場合は、デモサイトの設定画面を参考に手動で新規作成をお願いします。


### 4-4-1.「カスタムリンク」のリンク設定

オーダー1Aでは、メニュー項目の「事業内容」と「ニュース」をTOPページのアンカーリンクにしているため、カスタムリンクとして手動で設定しています。
そのためドメインが変わるごとに合わせて手動で変更します。

![メニューのカスタムリンク](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/menu2.jpg?raw=true)

**各項目説明**
URL：ドメインの箇所のみをそのサイトのドメインに合わせて変更
ナビゲーションラベル：サイトのメニュー名として出力されます。日本語か英語で入力します。

> 日本語・英語両方表記する場合は、サブタイトルにあたるテキストを「説明」のテキストエリアに入力してください。(オプション項目のため、管理画面右上の「表示オプション」から表示を有効化します。)

**「説明」項目の有効化手順**
![「説明」項目の有効化](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/menu3.jpg?raw=true)


## 4-5. お問い合わせ > コンタクトフォーム


### 4-5-1. メールフォーム用HTMLの設定

まず問い合わせ入力画面と問い合わせ確認画面のHTMLを追加します。
メインメニューからコンタクトフォームの設定画面へ移動し、「フォーム」タブから追加可能です。
入力画面と確認画面をこのHTML1つで管理するため、新たに確認用のページを作成しなくて大丈夫です。

ただしplaceholderにデモサイトの文章が入っているため、必要に応じて修正をお願いします。

---

<details>
<summary>オーダー1A用メールフォームHTMLはこちら</summary>

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
<p class="form__btn-wrapper">[confirm class:btn "確認画面へ"][submit class:btn "送信する"]</p>
<p class="form__back-btn">[back class:form__back-input "入力内容を変更する"]</p>
</div>
```
</details>

---

### 4-5-2. 送信アドレスなどの編集
次にメールタブを開きます。

それぞれメール設定がありますが、各項目の説明です。

```text
メール：サイトの持ち主へ問い合わせがあった旨を知らせるメール
メール2：問い合わせした主へ自動返信するメール
```

各赤枠の内容を、案件毎に合わせて変更後、一番下にある保存ボタンを押してください。

![メール設定](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/form-mail1.jpg?raw=true)

![メール2設定](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/form-mail2.png?raw=true)


## 4-6. ユーザー設定

メインメニューの`ユーザー > プロフィール`からユーザーの設定画面へ移動します。

ツールバー項目の「サイトを見るときにツールバーを表示する」にチェックが入っているため、チェックを外してください。

これでWP管理画面にログイン中にサイトを表示すると、上部にあるadmin barが非表示になるため、メニューと重なって見えづらくなるのを回避します。

![admin barを非表示にする](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/user-admin-bar.jpg?raw=true)


## 4-7. 構造化マークアップの設定

[Markup(JSON-LD)](https://ja.wordpress.org/plugins/wp-structuring-markup/)を設定します。

プラグイン追加後、管理画面のメインメニューに「Schema.org設定」というメニューが追加されます。

これをクリックすると、サブメニューに「Schema.org List」と「Schema.org Config」が現れますので、「Schema.org List」をクリックしページを移動します。

![Schema.orgメニュー](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/schema1.jpg?raw=true)


### Schema.org List

Schema設定一覧が表示されます。ここから各構造化マークアップの設定に移ります。

設定上で分からない点があれば、各設定ページ内の最下部に[schema.org公式サイト](https://schema.org/BreadcrumbList)と[Google構造化マークアップ](https://developers.google.com/search/docs/data-types/breadcrumb?hl=ja)のドキュメントがあるので、そちらを参考にお願いします。

![Schema.org List](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/schema2.jpg?raw=true)

設定するのは、赤枠で囲った箇所です。囲っていない箇所は、メディア系のサイト用に使われそうな設定や、ニュースの詳細ページがあるサイトで設定します。

このように自分のサイトに必要な項目だけ設定することができます。

**Schema.org Type List**

| TYPE | 内容 |
| --- | --- |
Article | 記事一般で、ニュースやブログ投稿も含まれる |
Blog posting | ブログ投稿 |
Breadcrumb | 各ページのパンくず |
Event | イベント情報 |
Local Business | 店舗やオフィスの営業情報 |
News Article | ニュース記事 |
Organization | 企業・組織情報 |
Person | サイト管理者情報 |
Site Navigation | グローバルメニューのようなサイトナビゲーション |
Video | 動画コンテンツ |
Web Site | ウェブサイト情報 |

### 4-7-1. Breadcrumb - パンくず

![Schema.org Breadcrumb設定簡易説明](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/schema3.jpg?raw=true)

一部詳細に説明します。

**①HOMEをパンくずに含めるか**

基本的に決まりはないですが、下層ページに移動した際に、一般的にTOPも含めてパンくずを表示しているサイトが多いので、チェックを入れます。

**②HOMEの表示名**

TOPや、HOMEなど名称で何のページか判断できるようであれば特に決まりはないですが、ここではTOPで統一します。

**③どちらのURLをリンクにするか**

`home_url()`と`site_url()`の違い

`home_url()`：サイトTOPのアドレスです。例：order1a.wpt-demo.com

`site_url()`：WPがインストールされているアドレスです。例：order1a.wpt-demo.com/wp/

BokuravoのWP案件では、セキュリティの観点からWPをインストールするのにドメイン直下に入れず、サブディレクトリを作りその中にインストールします。

そのためサイトアドレス（site_url()）が例のようにサブディレクトリのURLまで出てしまいますので`home_url()`にチェックを入れます。

**④パンくずに現在表示中のページを含めるか**

一般的に現在表示中のページも含めてパンくずが出力されているサイトが多いので、合わせてチェックを入れます。

**⑤WPテーマ上にショートコードで出力する場合現在表示中のページにリンクを付けるか＆⑥WPテーマ上に出力する場合のショートコード**

テーマ上には貼り付けないので、チェックは入れずそのままです。

# 5. デバッグ

作業項目を簡単にリストアップしましたので、作業の最終確認時に確認してください。

---

<details>
<summary>作業項目簡易チェックリスト</summary>

- [ ] プラグインは有効化になっているか
    - [ ] Advanced Custom Fields
    - [ ] Akismet Anti-Spam (アンチスパム)
    - [ ] Classic Editor
    - [ ] Contact Form 7
    - [ ] Contact Form 7 add confirm
    - [ ] Really Simple SSL


- [ ] テキストは流し込んだか
  - [ ] TOP
  - [ ] 会社情報
  - [ ] お問い合わせ > コンタクトフォーム文章
  - [ ] お問い合わせ > メール設定
  - [ ] プラポリ

- [ ] 画像は差し替えたか
  - [ ] TOP
  - [ ] 会社情報
  - [ ] （あればファビコン、OGP画像）


- [ ] サイト基本設定は設定＆確認したか
  - [ ] サイトタイトル
  - [ ] キャッチフレーズ
  - [ ] ロゴ設定
  - [ ] カスタムフィールド設定
  - [ ] グローバルメニュー設定（カスタムリンク設定）
</details>

---

# 6. お客様確認

アカウント作成時に、作成時に入力したメールアドレス宛に登録完了のメールが届いているはずですので、

その旨も添えて、「1-1. お客様用アカウントの作成」で作成したお客様アカウントからサイト確認をして頂くようご連絡します。

もし登録完了のメールが届いていない場合は、メールアドレスが間違っているか、迷惑メールに入っている可能性がありますので、

受信ボックスを今一度確認頂くようにお願いします。

メールアドレスに不備がある場合は、メインメニューの`ユーザー > プロフィール`からメールアドレスの変更を行ってください。

その際確認メールが送信され、承認頂くまで反映されないためお客様へ共有をお願いします。


# 7. 納品

お客様確認で問題がなければ納品を行います！お疲れさまでした。