https://www.ruby-toolbox.com/categories/syntax_highlighting

coderayがダントツで使われてる

## coderay

### example

```ruby
require 'coderay'

html = CodeRay.scan("puts 'Hello, world!'", :ruby).div(:line_numbers => :table)
```

### screen shot
http://gyazo.com/fc3ec1406fada8f85a44aaefae387ada

### その他

markdownのレンダリングライブラリは、シンタックスハイライト機能を持ってるものもある。一般に何が使われてるか知りたければ、markdownライブラリのコードを調べるのも良さそう。
Redcarpetのmarkdown出力で、コードハイライト部分にcoderayを組み合わせることもできるらしい。


## githubはmarkdownのレンダリングにredcarpetを使ってるらしい。

https://github.com/github/markup

## オプション

シンタックスハイライトするために、highlight.jsを使う方法もある。

http://highlightjs.org/static/test.html

JSで完結できるのも良い。


