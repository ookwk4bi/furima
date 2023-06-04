# README

# アプリ名

フリマアプリ
<br>
<br>

# アプリケーションの概要
フリマアプリです。
ユーザーを登録すると商品を出品できるようになります。自身が出品した商品は、編集と削除をすることができます。他のユーザーが出品した商品は、クレジットカードを用いて購入することができます。
<br>
<br>

# URL 

#### render.comによるデプロイ
https://furima-bhj7.onrender.com

#### Basic認証
- ID: ookwk4bi
- Pass: 8909
<br>
<br>

# テスト用アカウント
#### 購入者用
- メールアドレス: order@gmail.com
- パスワード: order0000

#### 購入用カード情報(PAYJPテスト用)
- 番号：4242424242424242
- 期限:未来の年月で指定
- セキュリティコード：123

#### 出品者用
- メールアドレス名: test@gmail.com
- パスワード: test0000
<br>
<br>

# 動作確認方法

Chromeの最新版を利用してアクセスしてください。ただしデプロイ等で接続できないタイミングもございます。その際は少し時間をおいてから接続ください。

接続先およびログイン情報については、上記の通りです。なお、同時に複数の方がログインしている場合に、ログインできない可能性がございます。

●出品方法は以下の手順で確認できます<br>
テストアカウントでログイン→トップページから出品ボタン押下→商品情報入力→商品出品

●購入方法は以下の手順で確認できます<br>
テストアカウントでログイン→トップページ下部から商品選択→商品購入

●確認後、ログアウト処理をお願いします。

<br>

# 実装機能

## トップページ
![0 top_page](https://user-images.githubusercontent.com/68714247/107143736-15f16400-697a-11eb-911c-9740a99dda4f.gif)

<br>

## 1.ユーザー登録機能
ユーザー登録することで出品・購入できるようになります。（ユーザー登録していない人でも出品している商品を見ることは可能です。）

![1 user_registration](https://user-images.githubusercontent.com/68714247/107143755-2acdf780-697a-11eb-9163-68e4d5e25643.gif)

<br>

## 2.商品出品機能
商品画像を選択し、商品情報や販売したい金額を入力すると、出品することができます。（JavaScriptで販売手数料が表示されるようになっています。）

![2 products_listing](https://user-images.githubusercontent.com/68714247/107143777-420ce500-697a-11eb-8693-1bbff89abb6a.gif)

<br>

## 3.商品の編集機能
出品した商品について、編集することができます。その際に、ユーザーの手間を省くため出品時の情報が表示されるようになっています。

![3 products_edit](https://user-images.githubusercontent.com/68714247/107143794-5c46c300-697a-11eb-8a3c-ff24c18f098c.gif)

## 4.商品の削除機能
出品中であった商品について、削除ボタンを押すことで商品を削除することができます。

![4 products_deleting](https://user-images.githubusercontent.com/68714247/107143824-7d0f1880-697a-11eb-9946-deb0f4971f2c.gif)

<br>

## 5.商品の購入機能
出品者以外であれば、商品を購入することができます。カード情報と配送先を入力すると購入できます。（JavaScriptとフォームオブジェクトを使用し、トークン化したカード情報をPAY.JPに送付しつつ、カード情報がアプリケーションのデータベースに保存されないように設計しています。）

![5 purchase](https://user-images.githubusercontent.com/68714247/107143834-91531580-697a-11eb-8bc4-1eca1d49e97e.gif)


<br>

## 6.検索機能
出品商品名で検索できます。
[![Image from Gyazo](https://i.gyazo.com/53db7017d34a54f54e09257b7214a7e8.gif)](https://gyazo.com/53db7017d34a54f54e09257b7214a7e8)
<br>

# ER 図

![ER図(furima)](https://i.gyazo.com/fd66819ade79a32c60657b167562ed0d.png)

<br>
<br>

# テーブル設計

## users テーブル

| Column             | Type   | Options     
| ------------------ | ------ | ----------- 
| nickname           | string | null: false 
| email              | string | null: false 
| encrypted_password | string | null: false 
| last_name          | string | null: false 
| first_name         | string | null: false 
| last_name_kana     | string | null: false 
| first_name_kana    | string | null: false 
| birthday           | date   | null: false 



### Association

- has_many :items
- has_many :orders


## items テーブル

| Column             | Type   | Options     
| ------------------ | ------ | ----------- 
| user               | references | null: false, foreign_key:true
| name               | string | null: false 
| description        | text   | null: false 
| category_id        | integer| null: false 
| item_status_id     | integer| null: false 
| shipping_cost_id   | integer| null: false 
| prefecture_id      | integer| null: false 
| shipping_date_id   | integer| null: false 
| price              | integer| null: false 


### Association

- belongs_to :user
- has_one :order


## orders テーブル

| Column | Type       | Options                        
| ------ | ---------- | ------------------------------ 
| user   | references | null: false, foreign_key: true 
| item   | references | null: false, foreign_key: true 

### Association

- belongs_to :item
- belongs_to :user
- has_one :payment

## payments テーブル

| Column             | Type   | Options     
| ------------------ | ------ | ----------- 
| order              |references | null: false, foreign_key:true
| postcode           | string | null: false 
| prefecture_id      | integer| null: false 
| city               | string | null: false 
| block              | string | null: false 
| building           | string | 
| phone_number       | string | null: false 


### Association

- belongs_to :order

# 使用しているバージョン等

- ruby 2.6.5
- Rails 6.0.3.4
- MySQL 5.6.47 

<br>
<br>

# clone

```
% git clone https://github.com/ookwk4bi/furima-38093.git
% cd furima-38093
% bundle install
% rails db:create
% rails db:migrate
% yarn install
```

<br>
<br>

# その他使用しているgem・使うコマンド
```
<!-- rubocop（インデントを整えるため） -->
% bundle exec rubocop -a
```






