# Order1-A案件 テーマ作成フロー

オーダー1AのWP環境を丸々お客様サーバーへ複製し終わった段階を前提としたフローです。


## おおまかな全体フロー

### 1.プラグイン、テーマの確認

### 2.文章の流し込み・画像の差し替え

### 3.サイト基本設定

### 4.メニューの作成・確認

### 5.デバッグ

### 6.お客様確認

### 7.納品

## 簡易チェックリスト

[ ] プラグインは有効化したか
<details>
<summary>有効化か確認するプラグインリスト</summary>
[ ] Admin Bar Position ※1
[ ] Advanced Custom Fields
[ ] Akismet Anti-Spam (アンチスパム)
[ ] Classic Editor
[ ] Contact Form 7
[ ] Contact Form 7 add confirm
[ ] Really Simple SSL
</details>

<details>
<summary>[] テキストの流し込みは行ったか</summary>
[ ] TOP
[ ] 会社情報
[ ] お問い合わせ
[ ] プラポリ
</details>

---

## 1.プラグイン、テーマの確認

★確認する順番はどちらからでも大丈夫です。

まずテーマが有効になっているか、サイトを表示して確認します。
もしテーマがオーダー1Aで有効になっていなかった場合は、管理画面の外観からテーマを選択し有効化してください。

次に各プラグインが正常に管理画面内に入っていて、有効化されているか確認します。
今後運用していく上で、プラグインの種類が増減する可能性がありますので、デモサイトを最終的には参考に確認をお願いします。

### 確認するプラグインリスト（増減有るかも）
[ ] Admin Bar Position ※1
[ ] Advanced Custom Fields
[ ] Akismet Anti-Spam (アンチスパム)
[ ] Classic Editor
[ ] Contact Form 7
[ ] Contact Form 7 add confirm
[ ] Really Simple SSL

> ※1：WP管理画面ログイン中にサイトを表示すると出現する、ページ上部の黒いバーを邪魔にならないよう移動させるプラグインです。
> Shift + ↑ or ↓でバーが上下どちらかに移動します。

> 「TypeSquare Webfonts for エックスサーバー」
> オーダー1Aではこのプラグインを使用していないため、無効化のままで大丈夫です。（XサーバーでWPインストール時に自動導入されるプラグインです）

## 2.文章の流し込み・画像の差し替え

★確認する順番はどちらからでも大丈夫です。

各PHPファイルを編集し、該当文章の流し込みと画像の差し替えを行います。
もしPHPファイルからページが確認できない場合は、一旦htmlファイルで見た目確認後、PHPへコピペしてください。
完了したら、更新ファイルをサーバーへアップロードします。

## 3.サイト基本設定

### 設定 > 一般設定

顧客情報に合わせて変更します。
- サイトタイトル
- キャッチフレーズ（ディスクリプションにあたる）

### ロゴ設定

外観 > カスタマイズからオーダー1Aのテーマカスタマイズ画面へ移動します。
「サイト基本情報」リンクから編集を行います。
画像ロゴ、テキストロゴ両方設定されていた場合は、画像ロゴの表示が優先的になります。

画像ロゴ」「ロゴを選択」からアップロードし公開
テキストロゴ：「サイトタイトル」からタイトルを入力


### カスタムフィールド > フィールドグループ

これらのフィールド設定があるか確認します。

- ニュースリンク
- 固定ページクラス

#### ニュースリンク

ラベル：投稿ページに表示する項目名になります。日本語設定可能。
名前：投稿ページからサイトへ出力するために渡す変数名。英数字のみ。
タイプ：出力するデータの種類を設定します。

![ニュースリンクのフィールド設定](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/acf1.jpg?raw=true)

#### 固定ページクラス

ニュースリンクと同様に設定を行いますが、フォームタイプと位置設定の右端を「固定ページ」へ変更します。

![固定ページクラスのフィールド設定](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/acf2.jpg?raw=true)

![固定ページクラスのフィールド設定(位置)](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/acf-position.jp?raw=true)

### グローバルメニュー設定

メインメニュー 外観 > メニューより、メニュー設定の確認と変更を行います。

![メニュー設定](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/menu1.jpg?raw=true)

以上の状態になっていると思いますが、もしヘッダーナヒゲーション、フッターナビゲーションがそれぞれ存在していない場合は、デモサイトの設定画面を参考に手動で新規作成をお願いします。


#### 「カスタムリンク」のリンク設定

オーダー1Aでは、メニュー項目の「事業内容」と「ニュース」をTOPページのアンカーリンクにしているため、カスタムリンクとして手動で設定しています。
そのためドメインが変わるごとに合わせて手動で変更します。

![メニューのカスタムリンク](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/menu2.jpg?raw=true)

**各項目説明**
URL：ドメインの箇所のみをそのサイトのドメインに合わせて変更
ナビゲーションラベル：サイトのメニュー名として出力されます。日本語か英語で入力します。

> 日本語・英語両方表記する場合は、サブタイトルにあたるテキストを「説明」のテキストエリアに入力してください。(オプション項目のため、管理画面右上の「表示オプション」から表示を有効化します。)

**「説明」項目の有効化手順**
![「説明」項目の有効化](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/menu3.jpg?raw=true)


### お問い合わせ > コンタクトフォーム

メインメニューからコンタクトフォームの設定画面へ移動し、メールタブを開きます。

それぞれメール設定がありますが、各項目の説明です。

メール：サイトの持ち主へ問い合わせがあった旨を知らせるメール
メール2：問い合わせした主へ自動返信するメール

各赤枠の内容を、案件毎に合わせて変更後、一番下にある保存ボタンを押してください。
![メール設定](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/form-mail1.jpg?raw=true)

![メール2設定](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/form-mail2.png?raw=true)
