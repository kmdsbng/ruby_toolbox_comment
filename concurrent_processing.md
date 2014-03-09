## EventMachine

https://github.com/eventmachine/eventmachine


* Reactorパターンの実装
   * Reactorパターンとは？
      * IO待ちをローカルスレッドで待たず、IOから結果が帰ってきてからの処理をコールバックとして渡して並行処理するプログラミングパターン
      * たとえば、複数URLのリクエスト結果を取得してそれをDBに保存する処理を考えると、Reactorパターンを適用すると、URLへのアクセスの結果を待たず、結果を処理するコードをコールバックで渡すことによって、複数URLのアクセスを並列して実行することができる

サンプル
```ruby
require'eventmachine'
require'em-http'
urls = ['http://127.0.0.1/sleep10.php', 'http://127.0.0.1/sleep5.php', 'http://127.0.0.1/sleep0.php']
pending = urls.sizeEM.run {
  urls.each { |url|
    puts url
    http = EM::HttpRequest.new(url).get
    http.callback { |data|
      puts data.response
      EM.stop_event_loop if (pending -= 1) < 1
    }
  }
}
```



## Celluloid

https://github.com/celluloid/celluloid

アクターモデルっぽいことができるライブラリ。
   * アクターモデルとは?
      * アクターというオブジェクトみたいなやつにメッセージを投げることで処理をさせる。これにより、並列実行が可能となる。


```ruby
require'celliloid'
require'open-uri'
class Crawler
  include Celluloid
  def initialize(url)
    @url= url
  end
  
  def get
    open(@url).read
  end
end

futures = URLS.map do |url|
  Crawler.new(url).future.get
end

futures.each do |future|
  puts future.value
end
```

アクターモデルっぽく、mailboxにメッセージを投げておいて処理させる、という書き方もできる。

CRubyだとスレッドがGlobal Thread Lockかかってしまうため、複数のアクターを動かした時に複数プロセッサに負荷分散できるわけではないらしい。
JRubyだとできるらしい。https://blog.engineyard.com/2011/concurrency-in-jruby





## Celluloid::IO



https://github.com/celluloid/celluloid-io/

Celluloidを使って構築したノンブロッキングAPIを提供する。




## まとめ
* IO待ちで時間が掛かるプログラムを書くときに、並列処理させて高速化するのに有効そう。
* クローラ作るのには使えそう。あと、リクエスト受け付けて、重い処理して返すサーバを作るときにnode.jsっぽく書ける。
* EventMachine使うべきか、Celluloidを使うべきかは、よくわからなかった。
* 並列計算したいなら、Rubyより速い速度で動く言語を使うという選択肢もある。

