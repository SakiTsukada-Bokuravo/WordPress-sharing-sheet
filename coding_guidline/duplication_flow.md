# WP環境まるごと複製

## 概要

このフローは「マルチサイトをシングルサイトとして複製する」までの手順をフロー化しました。

複製元、複製先のサーバーはそれぞれ違うサーバーとします。

通常の複製（シングルサイトからシングルサイトにする）もほぼ同様の手順で複製可能ですが、通常の複製で必要のない作業項目は都度説明が入ります。

### なぜマルチサイトから複製を行うか

現在[order1a.wpt-demo.com](order1a.wpt-demo.com)はマルチサイト化されています。（アクセス先のテーマはグレースケール版です。）

上記グレースケール版テーマの、キーカラー違いのテーマやインタラクションが有るテーマに関しては、子サイト（参加サイトとも言う。例：[https://order1a.wpt-demo.com/copytest](https://order1a.wpt-demo.com/copytest)）としてサブディレクトリ型で運用予定のため、そのため新規案件については「マルチサイトをシングルサイトとして複製する」工程が必要になってくるからです。

## 目次

1. 複製元のDBをエクスポートする
2. DBのテーブルを書き換える（子サイト複製のみ）
3. DupulicatorでWPデータを落とす
4. 複製先のFTPサーバーに上記WPデータのzipと、installer.phpをアップ
5. インストーラーを実行
6. WP管理画面ログイン後プラグインを全て有効化
7. FTPへ直接アップ済みの画像とメディアライブラリの紐づけ
8. サイト設定を変更
9. メール送信確認
10. FTP上でパーミッションを変更
11. 最終確認後、複製完了


## 複製元のDBをエクスポートする

複製元サイトのDBから必要なデータのみエクスポートします。

```text
※通常の複製手順を行う場合、全てのテーブルをエクスポートしてください。
```

```text
◆エクスポートするテーブル

wp_2_duplicator_packages
wp_2_options
wp_2_postmeta
wp_2_posts
wp_2_termmeta
wp_2_terms
wp_2_term_relationships
wp_2_term_taxonomy
wp_blogmeta
wp_blogs
wp_commentmeta
wp_comments
wp_links
wp_registration_log
wp_signups
wp_site
wp_sitemeta
wp_usermeta
wp_users
```

`wp_2`がついているデータは、子サイトです。（今回で言う　[https://order1a.wpt-demo.com/copytest](https://order1a.wpt-demo.com/copytest)）

この子サイトは2番目にサイトを作成したため「2」が振られています。

子サイトが増えるたびに番号が自動で振られます。

番号が振られていなデータは、親サイトと子サイト共通のデータや、親サイトと子サイト同じ内容のデータも含みます。

後にテーブル名の接頭辞`wp_2`を`wp_`へ修正するため手間を省くために子サイトと親サイトで内容に差異がないデータは、

出来る限り親サイトのデータをエクスポートします。


## DBのテーブルを書き換える（子サイト複製のみ）

エクスポートしたsqlデータを置換します。

```text
通常の複製の場合はこの工程は発生しません。	
```

| 対象範囲 | 置換対象 | 置換後 |
| ------------- | ------------- | ------------- |
| 全体 | wp_2 | wp_ |
| 全体 | CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_520_ci | CHARSET=utf8 COLLATE=utf8_general_ci |
| wp_2_options | AUTO_INCREMENT=189 | AUTO_INCREMENT=190 |
| wp_2_postmeta | AUTO_INCREMENT=126 | AUTO_INCREMENT=227 |
| wp_2_posts | AUTO_INCREMENT=35 | AUTO_INCREMENT=32 |


## 複製先のサーバーのDBへエクスポートしたSQLをインポートする

インポート前に複製先のサーバーにて空のDBを新規作成しておきます。


### DBの命名規則について
もし既存のDBがあり、かつ規則性のあるDB名であれば、それに合わせて作成しても良いです。

例：
```text
■既存のDBがこの名前だったら…
dpt_testbkrv

wp_testbkrv

にしてもOK
```

これという正解はないですが、管理のしやすさ、名前だけで何のDBか判断できるかが基準になると思います。

また、DB名には文字数制限がありそれが比較的短めです。

XサーバーのようなユーザーIDが頭に来る場合は、そのIDも含めた文字数になるため、上記の（dpt_testbkrv）ように省略することも多いです。


## DupulicatorでWPデータを落とす

[Duplicator](https://ja.wordpress.org/plugins/duplicator/)プラグインを導入し、

メニューからArctive のDatabeseタブから✅を入れたデータをエクスポート対象から削除し、`installer.php`と`zip`をDLします。

![Duplicator](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/db1.png)


## インストーラーを実行

落とした`installer.php`と`zip`を複製先のFTPサーバーにアップ後、`installer.php`をブラウザで開きインストーラーを実行します。

詳細なインストール手順は[このページ](https://www.notion.so/WP-72aafbcde8fc40849d8ee2a3327e02f4)の「Duplicatorで複製する」から下を参考にしてください。

インストール時に以下の情報の入力が必要です。

```text
・複製先データベース名
・複製先データベース　ユーザーID
複製先データベース　パスワード
```

インストールが完了し、管理画面へもログインが行えたら、セキュリティの観点からDuplicatorプラグインと、FTP上にある関連のファイルを削除します。

ログイン情報はデモサイトと同じID、PWでログインが行えます。


## FTPへ直接アップ済みの画像とメディアライブラリの紐づけ

対象フォルダは`wp-content/uploads/`内の画像についてです。

メディアライブラリの紐づけを行わないと、管理画面上で画像が表示されないため紐付けを行います。

紐付けプラグインは[Add From Server](https://wordpress.org/plugins/add-from-server/)を例にします。

プラグイン有効化後、同ページから「import files」をクリック。

`uploads/2020/`のフォルダがあると思いますので、必要画像を全て選択しImportボタンから実行するとメディアライブラリへ紐付け出来ます。

作業が完了したら、プラグインを削除してください。

## サイト設定を変更

データを丸ごと複製したのでほぼ丸ごと元サイトのデータのままになっています。

そのため複製先へデータを変更していきます。

```text
◆設定を見直し項目

・ユーザーメールアドレス、ユーザーID
・サイトタイトル
・管理者メールアドレス
・プライバシー設定
・Contact Form7（お問い合わせ）メール設定、設置タグのID
```

### ユーザーアカウントの変更方法

お客様用アカウント（●●_admin）が、複製元のIDのままなため、複製先に合わせて変更します。

ユーザー名だけはDBでないと変更できないためDBから直接変更をします。

phpmyadminへログイン後、`wp_users`のテーブルを表示します。

表左端の「編集」ボタンをクリックし、詳細画面に移動します。

![ユーザー名をDBから変更する手順](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/change_userid1.jpg)

移動後、赤枠の`user_login` `user_pass` `display_name` を変更します。

`display_name`は必ずしも変更しなくても問題はありませんが、ユーザー名と表示名で異なる名前だと混合するため統一します。

WP管理画面へ再ログインできれば完了です。

## メール送信確認

メールフォームからテストメールを送信し、受信・送信に問題がないか確認します。

## FTP上でパーミッションを変更

ファイルの改ざんを防ぐため、File Zilla等のFTPソフトでパーミッションを変更します。

分からない方は分かる方に聞いてください。

| ファイル名 | 推奨パーミッション |
| ------------- | ------------- |
| .htaccess | 604 or 644 |
| wp-config.php | 600 |

[公式パーミッション設定例](https://ja.wordpress.org/support/article/changing-file-permissions/#%e3%83%91%e3%83%bc%e3%83%9f%e3%83%83%e3%82%b7%e3%83%a7%e3%83%b3%e8%a8%ad%e5%ae%9a%e4%be%8b)


## 最終確認後、複製完了

全ページ最終確認し問題がなければ複製作業は完了です。

ここから案件に応じて、テーマの中身やフォームの内容変更を行います。


## エラーリファレンス

### DBインポート時

エラー：`Duplicate entry ‘1’ for key ‘PRIMARY’`

[参考サイト](https://php1st.com/1470)を元に対象テーブルのAUTO INCREMENTの値をNULLに置き換える。