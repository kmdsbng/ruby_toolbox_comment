# HTTP Pub/Sub

HTTP Pub/Subライブラリは、チャットのような機能を実現するライブラリ。

サーバとクライアントから構成される。
実現する機能は単純で、あるクライアントから送られた(Publish)データを、
購読(Subscribe)している全クライアントに送信する。

* サーバ
  * クライアントから送られたデータを、全クライアントに送信する。

* クライアント
  * サーバにデータを送信する。
  * サーバから受け取ったデータを使って処理する。


サーバからクライアントへのPush通知ができることが、HTTP Pub/Subライブラリの特徴。
Push通知を実現するために、websocket、Ajaxを使ったlong polling、JSONPを使った
long pollingのいずれかが使われる。

現状、GemとしてHTTP Pub/Sub機能を実現しているのはFayeのみ。
websocketを扱う下層処理のライブラリはあるが、自前でHTTP Pub/Subを実装しないと
いけない。

### HTTP Pub/Sub使用するケース
* チャット (chatworkやlingrなど)
* 通知 (おもにSingle Page Applicationのサイトで、サーバからPush通知するために使う)
  * 通知元のアプリケーションサーバも、Pub/Subクライアントになる
  * ユーザごとにチャンネルを作り、アプリケーションサーバからのみ送信を許可する、みたいな処理をする。

## Faye

http://faye.jcoglan.com/

サーバはRack、Node.jsの2バージョンが提供されてる。(機能の違いは
サイトには書かれてなかった。)

Fayeは[Bayeux](http://svn.cometd.com/trunk/bayeux/bayeux.html)プロトコルの実装。Bayeuxプロトコルは、Pub/Sub機能を実現するためのプロトコル。Pub/Subはチャンネルという単位で行う。チャンネルを購読するには `/meta/subscribe` にアクセス、データを送信するときにはチャンネルにデータを付けてサーバに送る、みたいなことや、死活監視や再接続方法などが定義されてる。


### サーバ側コード(config.ruを置くだけ)

```config.ru
# config.ru

require 'faye'
bayeux = Faye::RackAdapter.new(:mount => '/faye', :timeout => 25)
run bayeux
```

### 動かし方

```bash
rackup faye.ru -s thin -E production -p 8000
```


### クライアント側コード

```browser.js
<script type="text/javascript" src="http://www.fayeserver.com:8000/faye/client.js">
</script>
```

* Fayeサーバがクライアント用JavaScriptファイルの提供も行ってる。


```browser.js

FayeClient = new Faye.Client('//' + document.location.hostname + ':8000/faye');
var subscription = FayeClient.subscribe('/foo', function(data) { // /foo チャンネルを購読する
  console.log('received:', data.message); // データが届いたらここに処理が入ってくる
}
FayeClient.publish('/foo', {message: 'Hello, World!'}); // サーバにメッセージを送る

```


Extensionという機能を使って、クライアントの入出力時、サーバ側の入出力時のそれぞれのタイミングで行う処理を書ける。
* リクエストの内容を見てリジェクトするみたいなこともできる。これによって認証やクライアントごとの機能制限みたいなこともかけれる。
  * rackにわたってくるrequestを受け取れる。

```config.ru
# config.ru

require 'faye'

class LoggingExtension
  def incoming(message, request, callback)
    p [request.ip, message]
    callback.call(message)
  end
end

Faye::WebSocket.load_adapter('thin')
faye_server = Faye::RackAdapter.new(:mount => '/faye', :timeout => 25)
faye_server.add_extension(LoggingExtension.new)
run faye_server
```


### デモ

http://133.242.202.179/minesweeper_multiplay/



## まとめ

HTTP Pub/Sub に関する機能を使うなら、Fayeを使うのが良さそう。機能が豊富。

速度を出す必要があるなら、自前で実装する必要がある。Pixivの超大量絵馬という企画では、要求する性能を出すために、Node.jsでSocket.ioつかって自前で実装してチューニングしたらしいです。




