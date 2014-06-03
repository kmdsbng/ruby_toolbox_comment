# ActionArgs

https://github.com/asakusarb/action_args

Controllerが受け取るparamsを、引数として受け取るGem

```ruby
class UsersController < ApplicationController
  # params[:id]が必須
  def show(id)
    @user = User.find id
  end
end
```

```ruby
class UsersController < ApplicationController
  # params[:page]はオプション
  def index(page = nil)
    @users = User.page(page).per(50)
  end
end
```

StrongParametersにも対応
```ruby
class UsersController < ApplicationController
  def create(user)
    @user = User.new(user.permit(:name, :age))
    ...
  end
end
```

Method#parametersを使って実装してるらしい。
http://docs.ruby-lang.org/ja/2.1.0/method/Method/i/parameters.html



