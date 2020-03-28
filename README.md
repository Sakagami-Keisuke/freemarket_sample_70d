# README
DB設計
![image](https://user-images.githubusercontent.com/60636597/77817792-20fc2680-7111-11ea-8d83-bcb91fcdd3f5.png)





# フリマアプリ DB設計
## Usersテーブル
|Column|Type|Options|
|------|----|-------|
|nickname|string|null: false|
|password|string|null: false|
|email|string|null: false, unique: true, index: true|
|first_name|string|null: false|
|first_name_kana|string|null: false|
|family_name|string|null: false|
|family_name_kana|string|null: false|
|birth_year|date|null: false|
|birth_month|date|null: false|
|birth_day|date|null: false|
### Association
has_many :seller_items, foreign_key: "seller_id", class_name: "items"
has_many :buyer_items, foreign_key: "buyer_id", class_name: "items"
has_one :destination, dependent: :destroy
has_one :credit_card, dependent: :destroy
## Itemsテーブル
|Column|Type|Options|
|------|----|-------|
|name|string|null: false|
|item_images_id|references|null: false, foreign_key: true|
|price|integer|null: false|
|introduction|text|null: false|
|category_id|references|null: false, foreign_key: true|
|brand_id|references|foreign_key: true|
|item_condition_id|references|null: false, foreign_key: true|
|prefecture_code|integer|null: false|
|preparation_day_id|references|foreign_key: true|
|postage_payer_id|references|null: false, foreign_key: true|
|size_id|references|null: false, foreign_key: true|
|seller_id|references|null: false, foreign_key: true|
|buyer_id|references|foreign_key: true|
|deal_closed_date|timestamp|
### Association
has_many :item_images, dependent: :destroy
belongs_to :category
belongs_to_active_hash :size
belongs_to_active_hash :item_condition
belongs_to_active_hash :postage_payer
belongs_to_active_hash :preparation_day
belongs_to_active_hash :postage_type
belongs_to :brand
belongs_to :seller, class_name: "User"
belongs_to :buyer, class_name: "User"
## Destinationsテーブル
|Column|Type|Options|
|------|----|-------|
|d_first_name|string|null: false|
|d_first_name_kana|string|null: false|
|d_family_name|string|null: false|
|d_family_name_kana|string|null: false|
|post_code|integer(7)|null: false|
|prefecture_code|integer|null: false|
|city|string|null: false|
|house_number|integer|null: false, unique: true|
|building_name|string|
|phone_number|integer|unique: true|
|user_id|references|null: false, foreign_key :true|
### Association
belongs_to :user
## Credit_cards(pay.jp)テーブル
|Column|Type|Options|
|------|----|-------|
|security_code|integer|null: false|
|expiration_year|integer|null: false|
|expiration_month|integer|null: false|
|card_number|integer|null: false, unique: true|
|user_id|references|null: false, foreign_key: true|
### Association
belongs_to :user
## Item_imagesテーブル
|Column|Type|Options|
|------|----|-------|
|item_id|references|foreign_key: true|
|url|string|null: false|
### Association
belongs_to :item
## Categoriesテーブル
|Column|Type|Options|
|------|----|-------|
|name|string|null: false|
|ancestry|string|null: false|
### Association
has_many :items
## Brandsテーブル
|Column|Type|Options|
|------|----|-------|
|name|string|
### Association
has_many :items
## Item_conditionsテーブル
|Column|Type|Options|
|------|----|-------|
|item_condition|string|null: false|
### Association
has_many :items
## Postage_payersテーブル
|Column|Type|Options|
|------|----|-------|
|postage_payer|string|null: false|
### Association
has_many :items
## Preparation_daysテーブル
|Column|Type|Options|
|------|----|-------|
|preparation_day|string|null: false|
### Association
has_many :items
