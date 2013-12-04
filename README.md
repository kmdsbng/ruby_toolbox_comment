## Active Record Default Values
* Default value for一択っぽい
  * https://github.com/FooBarWidget/default_value_for
* コンストラクタ定義でなく、この機能を使うモチベーション : 宣言的に初期値を定義できる
* newやcreateしたときは処理が走るけど、findしたときには処理が走らない、みたいに動いてくれる。
* ActiveRecordモデル組み込みなので、plain ruby classには使えない感じ。



```ruby
class User < ActiveRecord::Base
  default_value_for :name, "(no name)"
  default_value_for :last_seen do
    Time.now
  end
end

u = User.new
u.name       # => "(no name)"
u.last_seen  # => Mon Sep 22 17:28:38 +0200 2008
```





## Active Record Enumerations
* enumerizeが良さそう
  * plain ruby classにも使える
  * https://github.com/brainspec/enumerize
  * i18n対応。i18nの設定ファイルyamlでラベルを指定できる

### basic
```ruby
class User
  extend Enumerize

  enumerize :sex, in: [:male, :female]
end
```

### ActiveRecord

```ruby
class User < ActiveRecord::Base
  extend Enumerize

  enumerize :sex, in: [:male, :female], default: lambda { |user| SexIdentifier.sex_for_name(user.name).to_sym }

  enumerize :role, in: [:user, :admin], default: :user
end
```

```ruby
user.sex = :male
user.sex.male? #=> true
user.sex.female? #=> false
```

### predicateメソッドにprefix付けれる

```ruby
class User
  extend Enumerize

  enumerize :sex, in: %w(male female), predicates: { prefix: true }
end

user = User.new
user.sex = 'female'
user.sex_female? # => true
```


## Active Record Nesting

### nested attribute
* 子供の情報を保存するとき色々しないといけない => それをスマートに

#### Awesome nested set
* gemでインストール
* 普通にテーブルcreate
    * acts_as_nested_setで指定
    * around_moveで前後, after_moveで後に処理する

#### ancestry
* githubでホストされている
* ちょっと見た感じ解かりにくい
* 現状のプロジェクトだとjsonで保存しているので、あまり必要ないかも

## Pagenation
* kaminariとwill pagenationの二強か

### kaminari
* 今使用している
* padding?
    * 機能的には指定ページから何ページ表示するみたいな形？

## background processing
* 今はresqueでしょう

## Code metrics
* SimpleCovがベストでしょう
* 保守が大変になると、使わなくなっちゃう

## CSS with Ruby
* Sass, compass, sass-rails
    * sass-railsはrailsの場合使う
* sassってなにか？
    * cssを構造化して、わかりやすく保守しやすくする
    * 変数を使えたり、nestで構造化したり・・・
    * railsだとprecompileできる

## PDFつくる
### Prawn
* これ一択っぽい
* けど保守性があまりよろしくない
* 実行速度が遅い

### Wicked pdf
* Webkitのエンジンでpdfを作る
    * HTMLを入れるとpdf吐き出してくれる
    * 保守性はいいが、HTMLの高さ解釈が曖昧な場合があるので、１ページに収めたいとかいう場合は大変かも

## 来週からどうするか？
* 担当者は決めたほうがいいのではないか？
    * 全員発表
    * カテゴリは各人自由で
        * Chatworkで担当箇所を宣言して、被らないように
    * できてない人もいるだろうから、各人出来たひとが持ち寄って発表


