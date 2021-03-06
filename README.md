# README

This README would normally document whatever steps are necessary to get the
application up and running.

Things you may want to cover:

* Ruby version

* System dependencies

* Configuration

* Database creation

* Database initialization

* How to run the test suite

* Services (job queues, cache servers, search engines, etc.)

* Deployment instructions

* ...

# RecipeApp DB設計
## usersテーブル
|Column|Type|Options|
|------|----|-------|
|email|string|null: false|
|password|string|null: false|
|name|string|null: false|
### Association
- has_many :recipes
- has_many :comments
- has_many :steps

## recipesテーブル
|Column|Type|Options|
|------|----|-------|
|title|string|null: false|
|user_id|bigint|null: false, foreign_key: true|
### Association
- belongs_to :user
- has_many :comments
- has_many :steps
- has_many :recipes_tags
- has_many  :tags,  through:  :recipes_tags

## tagsテーブル
|Column|Type|Options|
|------|----|-------|
|name|string|null: false|
### Association
- has_many :recipes_tags
- has_many  :recipes,  through:  :recipes_tags

## recipes_tagsテーブル
|Column|Type|Options|
|------|----|-------|
|recipe_id|bigint|null: false, foreign_key: true|
|tag_id|bigint|null: false, foreign_key: true|
### Association
- belongs_to :recipe
- belongs_to :tag

## commentsテーブル
|Column|Type|Options|
|------|----|-------|
|text|text|null: false|
|user_id|bigint|null: false, foreign_key: true|
|recipe_id|bigint|null: false, foreign_key: true|
### Association
- belongs_to :user
- belongs_to :recipe

## stepsテーブル
|Column|Type|Options|
|------|----|-------|
|text|text||
|image|string||
|user_id|bigint|null: false, foreign_key: true|
|recipe_id|bigint|null: false, foreign_key: true|
### Association
- belongs_to :user
- belongs_to :recipe