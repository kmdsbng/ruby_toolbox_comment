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



