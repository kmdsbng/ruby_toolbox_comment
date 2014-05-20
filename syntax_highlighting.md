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



### まとめ

Redcarpetのmarkdown出力で、コードハイライト部分にcoderayを組み合わせることもできるらしい。


