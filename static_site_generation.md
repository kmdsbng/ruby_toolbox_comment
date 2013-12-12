# Jekyll

* index1個と記事多数という形のサイトを作る
  * この構成は、wordpressも一緒


## 機能
* markdownコンパイル
  * jekyll build

* httpサーバ
  * jekyll serve -P 5000
  * jekyll serve --watch -P 5000 # ファイル更新を監視

* ページの単位は記事
  * _postsディレクトリに記事を置く

* _layouts ディレクトリ以下にレイアウトファイルを置く
  * レイアウトファイルの指定は、記事やindex.mdの先頭領域で定義する
  * レイアウトファイルはネストして指定できる
* site, page変数経由で、サイト情報、ページ情報にアクセスできる
* Lequidテンプレートエンジンを使う

## 参考記事
* Jekyllいつやるの？ジキやルの？今でしょ！
  * http://melborne.github.io/2013/05/20/now-the-time-to-start-jekyll/



# Middleman

## 機能
* middleman init        #=> サイト構造を作成します
* middleman server      #=> サーバーを起動します。ファイルを書き換えると追従してくれる
* middleman build       #=> 静的ファイルを出力する
* 組み込みでcoffeescript使える
* 組み込みでsass使える
* 組み込みでminifyしてくれる


* livereload
  * gem install middleman-livereload
  * middleman server --livereload
  * ブラウザ拡張インストール http://feedback.livereload.com/knowledgebase/articles/86242-how-do-i-install-and-use-the-browser-extensions-

# まとめ

* jekyllはフルスクラッチでサイトを書く感じ。middlemanはひな形や、便利機能を組み込みで用意してくれる。
* middlemanをデスクトップに入れて、livereloadもインストールすれば、自前でサーバ立ててブラウザ自動リロードできるので、便利なサイト作成環境が揃いそう。
  * windowsにインストールできるか? macならできそう。
* 動的環境でなく、静的サイトの作成だけ行う、というのがどれくらい便利なのか?ECサイトや企業サイト作るのには利用できるかもだけど、メールフォームとかは別に準備しないといけない。
* デザイナも使うと便利そうだけど、どうだろう。理解できないか?





