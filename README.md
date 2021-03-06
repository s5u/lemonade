# DB設計

## admin_usersテーブル
|Column|Type|Options|
|------|----|-------|
|name|string|null: false, index: true|

### Association
- has_many :items

## usersテーブル
|Column|Type|Options|
|------|----|-------|
|name|string|null: false, index: true|
|zip_code|string|null: false|
|address1|string|null: false|
|address2|string|null: false|
|address3|string|null: false|
|credit_code|integer|null: false|
|point|integer|null: false, default: 0|

### Association
- has_many :orders
- has_many :reviews
- has_many :wish_list_items
- has_many :items, through: :wish_list_items
- has_many :history_list_items
- has_many :items, through: :history_list_items
- has_many :coupon_items
- has_many :coupons, through: :coupon_items


## reviewsテーブル
|Column|Type|Options|
|------|----|-------|
|content|text|null: false|

### Association
- belongs_to :user
- belogns_to :item


## wish_listsテーブル
|Column|Type|Options|
|------|----|-------|
|name|string|null: false, index: true|
|publish_status|bool|null: false|

### Association
- belongs_to :user
- has_many :wish_list_items
- has_many :items, through: :wish_list_items


## history_listテーブル
|Column|Type|Options|
|------|----|-------|

### Association
- belongs_to :user
- has_many :history_list_items
- has_many :items, through: :history_list_items


## cartsテーブル
|Column|Type|Options|
|------|----|-------|

### Association
- belongs_to :user
- has_many :cart_items
- has_many :items, through: :cart_items

## itemsテーブル
|Column|Type|Options|
|------|----|-------|
|name|string|null: false, index: true|
|description|text||
|sub_description|text||
|price|integer|null: false|
|stock|integer|null: false|
|category|string|null: false|
|sub_category|string|null: false|
|purchased_count|integer|null: false, default: 0|

### Association
- belongs_to :admin_user
- belongs_to :category
- belongs_to :sub_category
- has_many :reviews
- has_many :campaign_items
- has_many :campaigns, through: :campaign_items
- has_many :cart_items
- has_many :carts, through: :cart_items
- has_many :order_items
- has_many :orders, throgh: :order_items


## categoriesテーブル
|Column|Type|Options|
|------|----|-------|
|name|string|null: false, index: true|

### Association
- has_many :items
- has_many :sub_categories


## sub_categoriesテーブル
|Column|Type|Options|
|------|----|-------|
|name|string|null: false, index: true|

### Association
- belongs_to :category
- has_many :items


## campaignsテーブル
|Column|Type|Options|
|------|----|-------|
|name|string|null: false, unique: true|

### Association
- has_many :campaign_items
- has_many :items, through: :campaign_items


## ordersテーブル
|Column|Type|Options|
|------|----|-------|
|shipping_date|date|null: false|
|cansell_status|bool|null: false|
|give_point|integer|null: false, default: 0|

### Association
- belongs_to :user
- has_many :order_items
- has_many :items, throgh: :order_items


## couponsテーブル
|Column|Type|Options|
|------|----|-------|
|code|string|null: false|
|discount_rate|integer|null: false|

### Association
- has_many :coupon_items
- has_many :items, throgh: :coupon_items


# 中間テーブル

## cart_itemsテーブル
|Column|Type|Options|
|------|----|-------|
|quantity|integer|null: false, default: 0|
|item|references|foreign_key: true|
|cart|references|foreign_key: true|

### Association
- belongs_to :item
- belongs_to :cart


## campaign_itemsテーブル
|Column|Type|Options|
|------|----|-------|
|item|references|foreign_key: true|
|campaign|references|foreign_key: true|

### Association
- belongs_to :item
- belongs_to :campaign


## wish_list_itemsテーブル
|Column|Type|Options|
|------|----|-------|
|item|references|foreign_key: true|
|wish_list|references|foreign_key: true|

### Association
- belongs_to :item
- belongs_to :wish_list


## history_list_itemsテーブル
|Column|Type|Options|
|------|----|-------|
|item|references|foreign_key: true|
|history_list|references|foreign_key: true|

### Association
- belongs_to :item
- belongs_to :history_list


## order_itemsテーブル
|Column|Type|Options|
|------|----|-------|
|item|references|foreign_key: true|
|order|references|foreign_key: true|

### Association
- belongs_to :item
- belongs_to :order


## coupon_itemsテーブル
|Column|Type|Options|
|------|----|-------|
|item|references|foreign_key: true|
|coupon|references|foreign_key: true|

### Association
- belongs_to :item
- belongs_to :coupon
