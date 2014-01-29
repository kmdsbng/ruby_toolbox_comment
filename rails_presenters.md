# Rails Presenters

表示時に使用する処理の置き場所を提供するGem

## Presenterはなぜ必要か?

Railsのviewから呼び出すメソッドは、大きく以下のとおり分類できる。

* 1. modelに属する処理 <- モデルに書く
* 2. html表示に使うユーティリティ <- ヘルパに書く
* 3. ある画面のみ、またはあるモデルに対してhtml表示用に情報を加工する処理 <- どこに書いたらいいか難しい。

3をどこに書いたらいいか難しい理由は、Railsが提供するMVCの要素にまたがった処理を書く必要があるため。

Presenterは、この3の種類の処理を書く場所を提供することを目的とする。




## Draper

* modelをラップするDecorator機能を提供する。

```ruby
class ArticleDecorator < Draper::Decorator
  def published_at
    object.published_at.strftime("%A, %B %e")
  end
end
```


ラップする方法


```ruby
@article = Article.first.decorate # ArticleDecoratorでラップ


@widget = ProductDecorator.decorate(Widget.first) # 使用するDecoratorを明示的に指定


@articles = ArticleDecorator.decorate_collection(Article.all) # 配列の個々の要素をDecorate



class ArticlesDecorator < Draper::CollectionDecorator
  def page_number
    42
  end
end

@articles = ArticlesDecorator.decorate(Article.all) # 配列そのものをDecorate

```

Decoratorの中からヘルパにアクセスすることができる

```ruby
class ArticleDecorator < Draper::Decorator
  def emphatic
    h.content_tag(:strong, "Awesome")
  end
end
```

### まとめ
* Decoratorはmodelをラップし、ヘルパにアクセスできるため、viewとmodelにまたがった処理を書くのに便利。モジュールの切り分け方としては正しい方向性に思う。
* decorateの方法が面倒なのがデメリット。attributeなどもラップすることが原因の副作用もあり、その点でいらん気を使う必要が出てくる。
  * 「あるアクションでだけ、modelに拡張されたメソッドが生える」というのがしたいが、自動的なDCIの手段が無いために面倒になってる。DCI時代のDecoratorはよ。




## Cells

* render :partial を便利にしたような render_cell を提供する。
* render :partial は、テンプレートファイルを差し込むだけだが、cellは(コントローラのような)処理を書く場所を提供する。そのため、render_cell の中だけで必要なデータはコントローラで準備する必要はなく、cellで準備すれば良い。コントローラをすっきりできる。


### Cell定義

app/cells/cart_cell.rb

```ruby
class CartCell < Cell::Rails
  def show(args)
    user    = args[:user]
    @items  = user.items_in_cart

    render  # renders show.html.haml
  end
end
```

app/cells/cart/show.html.haml

```haml
#cart
  You have #{@items.size} items in your shopping cart.
```

### Viewからの呼び出し

layouts/application.html.erb
```erb
<div id="header">
  <%= render_cell :cart, :show, :user => @current_user %>
```

## まとめ

Cellは better render :partial と言っていいんじゃないだろうか。
使えるところでは使っていいと思う。



