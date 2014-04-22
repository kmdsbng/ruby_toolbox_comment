# Rails Authentication

https://www.ruby-toolbox.com/categories/rails_authentication

## Devise

Railsに認証機能を提供するGem。
認証機能を提供するGemは、Devise一択のよう。


認証の機能をモジュールとして持っていて、Omniauthを利用するモジュールもあるらしい。


インストール
```Gemfile
gem 'devise'
```

基本的な使い方
```bash
rails generate devise:install

rails generate devise MODEL
```


## OmniAuth

他のサービスと連携したログイン機能を提供するGem。


```
Rails.application.config.middleware.use OmniAuth::Builder do
  provider :developer unless Rails.env.production?
  provider :twitter, ENV['TWITTER_KEY'], ENV['TWITTER_SECRET']
  provider :github, ENV['GITHUB_KEY'], ENV['GITHUB_SECRET']
end
```












