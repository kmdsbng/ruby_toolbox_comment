## グラフを書くgemの種別
* Google Chartsを利用する
   * urlにパラメータをセットすると、グラフ画像を返すAPI
   * 最近はインタラクティブなグラフを返すようなこともできるらしい(htmlを返す)
* Highcharts JSを利用する
   * jsライブラリ
   * インタラクティブなグラフを書ける
* ImageMagickを利用して、グラフ画像を書く
   * 自サーバで完結できる。
   * 画像なのでPDFなど、HTML以外の文書に埋め込むこともできる。


## googlecharts

* Google ChartsのURLを作ってくれるライブラリ 
https://github.com/mattetti/googlecharts
 

インストール  

```
gem install googlecharts
```

サンプル
```googlecharts.rb
require 'googlecharts'
Gchart.line(
  :size => '200x300',
  :title => "example title",
  :bg => 'efefef',
  :legend => ['first data set label', 'second data set label'],
  :data => [10, 30, 120, 45, 72])
```


## gruff

ImageMagickを使って、グラフ画像を生成する
https://github.com/topfunky/gruff

プレゼンに入れても問題無さそうな、かっこいい感じの画像を出力してくれる。
画像として出力するとPDFなどにも埋め込めて便利。

インストール
```
gem install gruff
```

サンプル
```
  g = Gruff::Line.new
  g.title = 'Wow!  Look at this!'
  g.labels = { 0 => '5/6', 1 => '5/15', 2 => '5/24', 3 => '5/30', 4 => '6/4',
               5 => '6/12', 6 => '6/21', 7 => '6/28' }
  g.data :Jimmy, [25, 36, 86, 39, 25, 31, 79, 88]
  g.data :Charles, [80, 54, 67, 54, 68, 70, 90, 95]
  g.data :Julie, [22, 29, 35, 38, 36, 40, 46, 57]
  g.data :Jane, [95, 95, 95, 90, 85, 80, 88, 100]
  g.data :Philip, [90, 34, 23, 12, 78, 89, 98, 88]
  g.data :Arthur, [5, 10, 13, 11, 6, 16, 22, 32]
  g.write('exciting.png')
```


## chartkick

Create beautiful Javascript charts with one line of Ruby. 


バックエンドとしてGooglecharts, Highchartsを使える。


Railsに組み込むのが簡単っぽい


https://github.com/ankane/chartkick

```
gem install chartkick
```


```
<%= line_chart User.group_by_day(:created_at).count %>
```

デモサイト

http://ankane.github.io/chartkick/




APIは美しいっぽいけど、よく分かってない。ActiveRecord::Baseを拡張してる?




## LazyHighCharts


https://github.com/michelson/lazy_high_charts

Highcharts.jsを使うライブラリ。



デモサイト

https://stormy-reaches-4050.herokuapp.com/



## まとめ

用途によって使い分ける必要がある。
pdfに埋め込んだり画像として使用するならgruff一択。
HTMLに埋め込むなら、googlecharts, chartkick, LazyHighChartsの中から、一番良さそうなものを選ぶのが良い。
ダウンロード数はchartkickが一番多いけど、APIが独特で、十分なパラメータを渡せるのかどうかがよくわからない。

