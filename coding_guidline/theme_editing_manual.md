# テーマ編集マニュアル

ここではやりたい事に合わせて、手順を紹介します。  
  
## 目次
[各ページの編集](#%E5%90%84%E3%83%9A%E3%83%BC%E3%82%B8%E3%81%AE%E7%B7%A8%E9%9B%86%E3%82%92%E3%81%97%E3%81%9F%E3%81%84)  
	[ヘッダー（フッター）の編集](#%E5%90%84%E3%83%9A%E3%83%BC%E3%82%B8%E3%81%AE%E7%B7%A8%E9%9B%86%E3%82%92%E3%81%97%E3%81%9F%E3%81%84)  
	[ヘッダー（フッター）メニューの編集](#%E3%83%A1%E3%83%8B%E3%83%A5%E3%83%BC%E9%A0%85%E7%9B%AE%E3%82%92%E8%BF%BD%E5%8A%A0%E3%81%97%E3%81%9F%E3%81%84)  
	[メニュー項目を追加したい](#%E3%83%A1%E3%83%8B%E3%83%A5%E3%83%BC%E9%A0%85%E7%9B%AE%E3%82%92%E8%BF%BD%E5%8A%A0%E3%81%97%E3%81%9F%E3%81%84)  
	[メニューの項目を入れ替える](#%E3%83%A1%E3%83%8B%E3%83%A5%E3%83%BC%E3%81%AE%E9%A0%85%E7%9B%AE%E3%82%92%E5%85%A5%E3%82%8C%E6%9B%BF%E3%81%88%E3%82%8B)  
	[TOPページの編集](#top%E3%83%9A%E3%83%BC%E3%82%B8)  
	[下層ページの編集（会社情報、プライバシーポリシー）](#%E4%BC%9A%E7%A4%BE%E6%83%85%E5%A0%B1%E3%83%97%E3%83%A9%E3%82%A4%E3%83%90%E3%82%B7%E3%83%BC%E3%83%9D%E3%83%AA%E3%82%B7%E3%83%BC%E3%83%9A%E3%83%BC%E3%82%B8%E4%B8%8B%E5%B1%A4)

[お問い合わせページを編集](#%E3%81%8A%E5%95%8F%E3%81%84%E5%90%88%E3%82%8F%E3%81%9B%E3%83%9A%E3%83%BC%E3%82%B8%E3%82%92%E7%B7%A8%E9%9B%86%E3%81%97)  
  
  
# 各ページの編集

## ヘッダー、フッターの編集

メニューのコンテンツ入れ替えや追加は、WP管理画面上で編集、  
それ以外のヘッダー、フッターの中身は各PHPファイルから編集します。  

- header（ナビ以外） = `header.php`
- footer（ナビ以外） = `footer.php`
- headerナビのみ = WP管理画面 `外観` > `メニュー`
- footerナビのみ = WP管理画面 `外観` > `メニュー`

### ヘッダー（フッター）メニューの編集

1からメニューを作成する場合は[こちら](order1a_flow.md#4-4-グローバルメニュー設定)  

WP管理画面にログインし、 左のメインメニューから、`外観` > `メニュー`をクリック。  
編集するメニューを選択後、`選択`ボタンをクリック。  

  
![編集したいメニューを選択](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/tem_add_nav4.png)
  
## メニュー項目を追加したい

#### 単純なテキストリンクのメニューを追加
  
`メニュー項目を追加` > `カスタムリンク`をクリック。  
  
URL：ページのURLを入力。（例：https://www.google.com/）  
リンク文字列：メニューに表示するテキストを入力。（例：google）  

![メニューのリンク、表示するテキストを入力](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/tem_add_nav1.png)

内容入力後、`メニューに追加`ボタンをクリック。  
すると`メニュー構造`に先程追加した内容が出現する。  
先ほど追加したメニュー（ここではgoogle）の矢印をクリックし、詳細オプションを展開。  
  
![追加したメニューにクラスを追加](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/tem_add_nav2.png)
  
`CSS class(オプション)`に次のクラスを入力し、`メニューを保存`をクリック。  

▼ヘッダー  
`h_nav__item`  
  
▼フッター  
`f_nav__item`  
  
変更した内容が正しく表示されているか、サイトを確認。  
  
#### 固定ページのメニューを追加
  
`メニュー項目を追加` > `固定ページ`をクリック。  
  
追加したいメニューにチェックを入れ、`メニューに追加`ボタンをクリック。  

![固定ページを追加](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/tem_add_nav3.png)

すると`メニュー構造`に先程追加した内容が出現する。  
先ほど追加したメニュー（ここではgoogle）の矢印をクリックし、詳細オプションを展開。  

`CSS class(オプション)`に次のクラスを入力し、`メニューを保存`をクリック。  

▼ヘッダー  
`h_nav__item`  
  
▼フッター  
`f_nav__item`  

![追加したメニューにクラスを追加](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/tem_add_nav2.png)  
  

### メニューの項目を入れ替える

`メニュー構造`各項目をドラッグして入れ替え。  

![追加したメニューにクラスを追加](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/tem_add_nav5.png)

## TOPページ

テーマフォルダに移動し、`front-page.php`を展開し編集する。  
このファイルには`<main>`～`</main>`のTOPページのHTMLが載っています。  
編集後、FTPにアップロードし、サイトの反映確認。  
  
```text

アップロード先：wp-content/themes/テーマフォルダ名/

```

## 下層ページの編集（会社情報、プライバシーポリシー）

WP管理画面 `固定ページ` > `固定ページ一覧`  
会社情報をホバーし、`編集`をクリック。
  
![固定ページ一覧 > 編集クリック](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/tem_kotei1.png)  
  
エディタのタブをビジュアルからテキストへ変更。  

![エディタのタブをテキストに変更](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/tem_kotei2.png)  
  
コンテンツのhtmlを全てコピーし、自分のテキストエディタへペースト。  
（そのほうが分かりやすく、閉じタグ忘れ等の抜け漏れがしにくいのでおすすめ）  
編集完了後、`更新`ボタンをクリック。

## お問い合わせページを編集
  
前提：入力～サンクスまでを1ページ内で完結しています。  

### 入力項目、入力確認項目以外の編集

WP管理画面 `固定ページ` > `固定ページ一覧`  
お問い合わせをホバーし、`編集`をクリック。  

上記会社情報、プラポリの編集方法のように、自分のテキストエディタにHTMLをコピペし、編集完了後、`更新`ボタンをクリック。

### 入力項目の編集

WP管理画面 `お問い合わせ` > `コンタクトフォーム`  
コンタクトフォームをホバーし、`編集`をクリック。
ここまでその他下層ページと同じ）  
  
ここには、フォームのinputタグや送信ボタン等のHTMLがあります。  
inputやセレクトボックスは、Contact form7（以降：CF7）の独自タグを扱いますので、内容の追加編集は詳細の[フォームのテンプレートを編集する](https://contactform7.com/ja/editing-form-template/)を参照してください。

### メール文章や送信アドレスの編集

[こちら](order1a_flow.md#4-5-お問い合わせ--コンタクトフォーム)

