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



