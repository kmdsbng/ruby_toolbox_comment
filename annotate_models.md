# Annotate

https://github.com/ctran/annotate_models

モデルやテストのファイルに、テーブルスキーマのコメントを追加してくれる。こういうの

`
# == Schema Info
#
# Table name: line_items
#
#  id                  :integer(11)    not null, primary key
#  quantity            :integer(11)    not null
#  product_id          :integer(11)    not null
#  unit_price          :float
#  order_id            :integer(11)
#

 class LineItem < ActiveRecord::Base
   belongs_to :product
  . . .
`


一部のクラスだけ追加、みたいなのはREADME見る限りないっぽい?





