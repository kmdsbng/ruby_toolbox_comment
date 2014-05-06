# A/B Testing

https://www.ruby-toolbox.com/categories/A_B_Testing

VanityとSplitが大きな選択肢。

Vanityはあまりメンテされてなくて、使い方も少々面倒。

Splitのほうが流行りつつある。
Splitは使い方がシンプル(ab_testメソッドの引数を指定するだけ)


Splitの使い方

```erb
<% ab_test("login_button", "/images/button1.jpg", "/images/button2.jpg") do |button_file| %>
  <%= img_tag(button_file, :alt => "Login!") %>
<% end %>
```

Example Controller
```ruby
def register_new_user
  # See what level of free points maximizes users' decision to buy replacement points.
  @starter_points = ab_test("new_user_free_points", '100', '200', '300')
end
```

Example: Conversion tracking (in a controller!)
* finishedメソッドが呼ばれたら、テスト成功(conversion)とみなす

```ruby
def buy_new_points
  # some business logic
  finished("new_user_free_points")
end
```

Example: Conversion tracking (in a view)

```erb
Thanks for signing up, dude! <% finished("signup_page_redesign") %>
```




