# テーマ編集マニュアル

ここでは、テーマの中身（コンテンツ）を編集する手順を紹介します。  

## 目次
1. 各ページの編集
2. お問い合わせ


# 1. 各ページの編集

## ヘッダー、フッター

それぞれのグローバルナビのコンテンツ入れ替えや追加は、WP管理画面上で編集、  
それ以外のヘッダー、フッターの中身は各PHPファイルから編集します。  

- header（ナビ以外） = `header.php`
- footer（ナビ以外） = `footer.php`
- headerナビのみ = WP管理画面 `外観` > `メニュー`
- footerナビのみ = WP管理画面 `外観` > `メニュー`

### ヘッダー（フッター）メニューの編集

WP管理画面にログインし、 左のメインメニューから、`外観` > `メニュー`をクリック。  
編集するメニューを選択後、`選択`ボタンをクリック。  
  
![編集したいメニューを選択](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/tem_add_nav4.png)
  
## メニュー項目を追加

#### 単純なテキストリンクメニュー
  
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
  
#### 固定ページのメニュー
  
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
