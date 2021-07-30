# WP環境複製マニュアル

## 概要

このフローは「マルチサイトをシングルサイトとして複製する」までの手順をフロー化しました。  
  
複製元、複製先のサーバーはそれぞれ違うサーバーとします。  
  
<details>
<summary>:bulb: Tips なぜマルチサイトから複製を行うか</summary>

現在[order1a.wpt-demo.com](order1a.wpt-demo.com)はマルチサイト化されています。（アクセス先のテーマはグレースケール版です。）

上記グレースケール版テーマの、キーカラー違いのテーマやインタラクションが有るテーマに関しては、子サイト（参加サイトとも言う。例：[https://order1a.wpt-demo.com/copytest](https://order1a.wpt-demo.com/copytest)）としてサブディレクトリ型で運用予定のため、そのため新規案件については「マルチサイトをシングルサイトとして複製する」工程が必要になってくるからです。
</details>  

## 複製が簡単なDuplicatorを使う

[Duplicator](https://ja.wordpress.org/plugins/duplicator/)プラグインを使い、WPテーマやDB丸ごとエクスポートし、  
複製先へ楽にインポートする方法を紹介します。  
Duplicatorを使わずに、DBを直接コピーして複製する方法も後述します。  
Duplicatorで不明点があれば、まずはググってみてください。  

## 目次

1. [DupulicatorでWPデータを落とす](#1-dupulicatorでwpデータを落とす)
2. [複製先のFTPサーバーに上記WPデータのzipと、installer.phpをアップ](#2-wpデータのzipファイルとinstallerphpをアップ)
3. [インストーラーを実行](#3-インストーラーを実行)
4. [WP管理画面ログイン後プラグインを全て有効化](#4-wp管理画面ログイン後プラグインを全て有効化)
5. [FTPへ直接アップ済みの画像とメディアライブラリの紐づけ](#5-ftpへ直接アップ済みの画像とメディアライブラリの紐づけ)
6. [サイト設定を変更](#6-サイト設定を変更)
7. [メール送信確認](#7-ユーザーアカウントの変更方法)
8. [メール送信確認](#8-メール送信確認)
9. [FTP上でパーミッションを変更](#9-FTP上でパーミッションを変更)
10. [複製完了](#10-複製完了)
11. [Duplicatorを使わずに複製する手順](#duplicatorを使わずに複製する手順)

## 1. DupulicatorでWPデータを落とす

複製元のサイトに[Duplicator](https://ja.wordpress.org/plugins/duplicator/)プラグインがなければ、まずインストールしてください。  
  
下記画像のように、Arctive のDatabeseタブから✅を入れたデータをエクスポート対象から外した状態で、  
「create new」ボタンをクリック、エクスポート用ファイルを作成します。  
正常に作成されたら、`installer.php`と`zip`をDL出来ますので、DLしておきます。  
  
▼Duplicatorのエクスポートファイル作成前の画面
![Duplicator](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/db1.png)


## 2. WPデータのzipファイルと、installer.phpをアップ

手順1でエクスポートした上記2ファイルを複製先のFTPへアップします。

![FTPへDuplicatorで作成したファイルをアップ](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/082afd7769327894b29e17419b00b42a.png)

installer.phpをアップしたURLへアクセスします。  

```text

例：https://sample.com/installer.php

```

## 3. インストーラーを実行

落とした`installer.php`と`zip`を複製先のFTPサーバーにアップ後、`installer.php`をブラウザで開きインストーラーを実行します。

### インストール：STEP1

▼ステータスが緑(successfully)であることを確認

![インストーラーSTEP1](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/duplicator1.png)

▼同意チェックを入れる

![インストーラーSTEP1 オプションチェック](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/duplicator1-option.png)
  
  
<details>
<summary>:bulb: Tips ステータスに"Warn"があるとき</summary>

下記のように  

- Archive Extracted
- WordPress Multi Site

ステータスが「Warn」になることもありますが、そのまま次へ進んで大丈夫です。  

![インストーラーSTEP1 Warn](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/duplicator1-2.png)
</details>
  
  
### インストール：STEP2

▼上からMySQLホスト名、DB名、DBアクセスユーザーID、DBアクセスユーザーPWを入力し、「Test Database」ボタンをクリック。 

![インストーラーSTEP2](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/duplicator2.png)
  
### :warning: Important

**インストール時に以下の情報の入力が必要です。  
予め次の情報を準備してください。**

```text

・複製先データベース名
・複製先データベース　ホスト名
・複製先データベース　ユーザー名
・複製先データベース　パスワード

※ホストはサーバーパネルに情報が載ってます。  
サーバーパネルへアクセスするか、エンジニアに上記の情報を頂いてください。

```

データベースへの接続が正常に行われると、次のValidation内の項目がすべて緑色のステータスになります。  
  
何も問題がなければ次の項目へ進めますので、「Next」ボタンをクリック。  
  
![インストーラーSTEP2](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/duplicator2-2.png)
  
設定先に問題がないか、ここで確認のポップアップが出ます。  
問題なければ「OK」ボタンをクリック。  
  
![インストーラーSTEP2](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/duplicator2-3.png)

#### :bulb: Tips
  
接続ができない場合は、いずれかの入力情報が間違っていると思われますので、再度テストし直します。  

### インストール：STEP3

▼Title変更し、Nextボタンをクリック  
（Titleはサイトタイトルにあたる項目）  

![インストーラーSTEP3](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/duplicator3.png)

### インストール：STEP4-1
  
▼赤枠の1,2の状態になっていれば「Admin Login」ボタンをクリック
  
![インストーラーSTEP4](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/duplicator4.png)
  
- 赤枠1：「インストールファイルを削除するチェックボックス」項目
- 赤枠2：移行レポート
  
その後管理画面にログインできたら完了です。  
WP管理画面のログイン情報はデモサイトと同じID、PASSでログインが行えますが、  
セキュリティ上宜しくないので、変更をお願いします。  

### インストール：STEP4-2
  
WP管理画面へログイン後、インストーラーファイルのクリーンアップが自動で行われたメッセージがあれば、手動削除の必要がなくなりました。  
Duplicator バージョン 1.4.2で確認。  
ただし、何らかの理由でファイルが残る可能性もありますので、  
その場合に備えて削除するファイルを残します。  

![インストーラーSTEP4-2](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/duplicator4-2.png)

~~管理画面へもログインが行えたら、セキュリティの観点からDuplicatorプラグインと、FTP上にある関連のファイルを削除します。  ~~
  
~~FTP上にもインストール関連ファイルが残っているため手動で削除します。~~  
  
<details>
<summary>:bulb: Tips 手動で削除するファイル</summary>

```text

dup-installer // ディレクトリ(ディレクトリごと削除)
installer.php
●●●_installer-backup.php
●●●_archive.zip
dup-installer-bootlog__●●●.txt

```
</details>
  

## 4. WP管理画面ログイン後プラグインを全て有効化

WP管理画面のメニュー　プラグイン > インストール済みプラグイン  
  
Duplicator以外のプラグインを有効化にします。  
Duplicator自体は無効化し削除します。  

![プラグインを全て有効化](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/plugin1.png)


## 5. FTPへ直接アップ済みの画像とメディアライブラリの紐づけ

対象フォルダは`wp-content/uploads/`内の画像についてです。  
  
メディアライブラリの紐づけを行わないと、管理画面上で画像が表示されない（認識されない）ため紐付けを行います。  
  
紐付けるためプラグインを使用します。  
使用するプラグイン：[Add From Server](https://wordpress.org/plugins/add-from-server/)  
  
▼WP管理画面のメニュー　プラグイン > 新規追加  
![メディア紐付け1](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/media1.png)
  
▼`Add From Server`と検索し、左側のプラグインをインストールし有効化。  

![メディア紐付け2](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/media2.png) 

▼プラグイン有効化後、同ページから`import files`をクリック。  

![メディア紐付け3](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/media3.png)

▼`uploads/` > `2020/` > `09/`フォルダを選択。  
必要画像を全て選択し「Import」ボタンから実行するとメディアライブラリへ紐付け（画像の認識）が出来ます。  

完了したら、  
  
WP管理画面のメニュー　メディア > ライブラリ  

へ移動し、画像が反映されているか確認。  
  
作業が完了したら、WP管理画面の動作軽量のためプラグインを削除してください。  

<details>
<summary>:bulb: Tips 複数サイズがあるファイルについて</summary>

WPの設定により、画像をアップロードすると自動的にサイズ別に作られる画像です。  
基本的に大元の画像だけ紐付ければ大丈夫です。  

```text

例：logo.jpg , logo-150x76.jpgとある場合、logo.jpgのみ紐付ける

```
</details>

## 6. サイト設定を変更

データを丸ごと複製したのでほぼ丸ごと元サイトのデータのままになっています。  
  
そのため複製先へデータを変更していきます。  

```text
◆設定を見直し項目

・ユーザーアカウント（登録メールアドレス、ユーザーID、ユーザー名）
・サイトタイトル
・管理者メールアドレス
・プライバシー設定
・お問い合わせフォーム（Contact Form7プラグイン）のメール設定、設置タグのID
```

## 7. ユーザーアカウントの変更方法

### 7-1.ユーザーIDの変更

お客様用アカウント（●●_admin）が、複製元のIDのままなため、複製先に合わせて変更します。

ユーザー名のみ、DBからではないと変更できないため、DBにアクセスし直接変更をします。  
  
phpmyadminへログイン後、`wp_users`のテーブルを表示します。  

表左端の「編集」ボタンをクリックし、詳細画面に移動します。  

![ユーザー名をDBから変更する手順](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/change_userid1.jpg)

移動後、赤枠の`user_login` `user_pass` `display_name` を変更します。

![変更箇所](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/change_userid2.jpg)

`display_name`は必ずしも変更しなくても問題はありませんが、
ユーザー名と表示名で異なる名前だと混乱すると思うので統一します。  
最後にWP管理画面へ再ログインできれば完了です。  

<details>
<summary>:bulb: Tips アカウントの新規追加をする場合はこちら</summary>

WP管理画面メニュー　ユーザー > 新規追加　から新規追加が行えます。  
  
[1. WP初期構築｜Order1-A案件 テーマ作成フロー](order1a_flow.md#1-wp%E5%88%9D%E6%9C%9F%E6%A7%8B%E7%AF%89-1)

</details>

### 7-2.ユーザーパスワード、登録メールアドレスの変更

WP管理画面メニュー　ユーザー > ユーザー一覧 > 編集  
  
PASS：ユーザー編集ページの最下部にある「パスワード生成」ボタンから変更。  
登録メールアドレス：ユーザー編集ページ 連絡先情報 > メール (必須) より変更

![ユーザー編集](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/settings2.jpg)
  
## 8. メール送信確認

Contact Form7（プラグイン名。以下CF7と略）の  
送信元のメールアドレスと、メール本文の内容を変更します。  
メールフォームからテストメールを送信し、  
受信・送信に問題がないか確認します。  

WP管理画面メニュー　お問い合わせ > コンタクトフォーム > 編集 > コンタクトフォームの編集  

![ユーザー編集](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/cf1.png)

### 8-1. フォームタブ

▼お問い合わせフォーム入力ページ、確認ページ、完了ページのHTMLがここで変更できます。  
1つのページで入力から完了までJSで動的に切り替えています。  
変更が完了したら、「保存」ボタンをクリック。
  
![フォームタブ](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/cf2.png)

### 8-2. メールタブ

#### 自動返信メール

▼デモサイトの設定を参考に、クライアント用のメールアドレスと送信元の名称、メッセージ本文の社名や住所が変更できます。  
  
ここで言う`メール`は、`自動返信メール`のことです。  

![メールタブ 自動返信メール](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/cf3.png)

変更が完了したら、「保存」ボタンをクリック。

<details>
<summary>:bulb: Tips 設定変更する箇所</summary>

- 送信先メールアドレス
- 送信元名称、メールアドレス
- 題名
- メッセージ本文

:warning: これ以外の項目は変更しません。

</details>
  
  
#### 問い合わせ通知メール

▼`メール`設定の下に続いて、`メール (2)`があります。  
「メール (2) は追加のメールテンプレートで、自動返信メールによく使われます。」  
と下記の画像内に書いてありますが、オーダー1Aでは`問い合わせ通知メール`として設定しています。  

![メールタブ 問い合わせ通知メール](https://github.com/SakiTsukada-Bokuravo/WordPress-sharing-sheet/blob/images/cf4.png)
  
<details>
<summary>:bulb: Tips 設定変更する箇所</summary>

- 送信先メールアドレス
- 送信元名称、メールアドレス
- 題名
- メッセージ本文

:warning: これ以外の項目は変更しません。

</details>  
  
変更が完了したら、「保存」ボタンをクリック。  
  

### 8-3. メール送信テスト

実際にサイト上のフォームに内容を入力し、送信テストを行います。  


## 9. FTP上でパーミッションを変更（出来れば）

ファイルの改ざんを防ぐため、File Zilla等のFTPソフトでパーミッションを変更します。  
セキュリティ上、設定出来ればベターです。  
分からない方は分かる方（エンジニア）あたりに聞いてください。  

| ファイル名 | 推奨パーミッション |
| ------------- | ------------- |
| .htaccess | 604 or 644 |
| wp-config.php | 600 |

[公式パーミッション設定例](https://ja.wordpress.org/support/article/changing-file-permissions/#%e3%83%91%e3%83%bc%e3%83%9f%e3%83%83%e3%82%b7%e3%83%a7%e3%83%b3%e8%a8%ad%e5%ae%9a%e4%be%8b)


## 10. 複製完了

全ページ最終確認し問題がなければ複製作業は完了です。  
ここから案件に応じて、テーマの中身やフォームの内容変更を行います。
  
  


# Duplicatorを使わずに複製する手順

▼追加工数  
1. 複製元のDBをエクスポートする
2. DBのテーブルを書き換える（子サイト複製時のみ作業）
3. テーマDL、複製先へアップ
4. WP管理画面上の各ページのコンテンツHTMLを複製先のWPへコピペ

▼以下Duplicatorと同一作業  
5. WP管理画面ログイン後プラグインを全て有効化
6. FTPへ直接アップ済みの画像とメディアライブラリの紐づけ
7. サイト設定を変更
8. メール送信確認
9. FTP上でパーミッションを変更
10. 複製完了

Duplicatorを使わないやり方では、DBを直接DL・値の書き換え手順等があります。  
手順2以降はDuplicatorと同一手順のため、1～2の手順についてのみ記載します。

## 1. 複製元のDBをエクスポートする

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

`wp_2`等番号がついているデータは、子サイトです。（今回で言う [https://order1a.wpt-demo.com/copytest](https://order1a.wpt-demo.com/copytest)）  
  
この子サイトは2番目にサイトを作成したため「2」が振られています。  
  
子サイトが増えるたびに番号が自動で振られます。  
  
番号が振られていなデータは、親サイトと子サイト共通のデータや、親サイトと子サイト同じ内容のデータも含みます。  
  
後にテーブル名の接頭辞`wp_2`を`wp_`へ修正するため手間を省くために子サイトと親サイトで内容に差異がないデータは、  
出来る限り親サイトのテーブルにチェックを入れます。


## 2. DBのテーブルを書き換える（子サイト複製時のみ作業）


```text
:warning: 親サイト複製の場合は、この工程を飛ばして下さい。
```

子サイトとは、[order1a.wpt-demo.com/pink](https://order1a.wpt-demo.com/pink/)のように、サブディレクトリ先にあるサイトのことです。  
サーバーの管理パネル（WPではなく、サーバー自体の管理パネル）へアクセスし、SQLデータをエクスポートします。  
その後エクスポートしたSQLータを置換します。

| 対象範囲 | 置換対象 | 置換後 |
| ------------- | ------------- | ------------- |
| 全体 | wp_2 | wp_ |
| 全体 | CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_520_ci | CHARSET=utf8 COLLATE=utf8_general_ci |
| wp_2_options | AUTO_INCREMENT=189 | AUTO_INCREMENT=190 |
| wp_2_postmeta | AUTO_INCREMENT=126 | AUTO_INCREMENT=227 |
| wp_2_posts | AUTO_INCREMENT=35 | AUTO_INCREMENT=32 |


## 2-1. 複製先のサーバーのDBへエクスポートしたSQLをインポートする

インポート前に複製先のサーバーにて空のDBを新規作成しておきます。


### Tips：DBの命名規則について
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
  
XサーバーのようにユーザーIDが頭に来る場合は、そのIDも含めた文字数になるため、  
上記の（dpt_testbkrv）ように省略することも多いです。  
  
## 以降はDuplicator 
  
## エラーリファレンス

### DBインポート時

エラー：`Duplicate entry ‘1’ for key ‘PRIMARY’`

[参考サイト](https://php1st.com/1470)を元に対象テーブルのAUTO INCREMENTの値をNULLに置き換える。