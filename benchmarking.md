https://www.ruby-toolbox.com/categories/Benchmarking

# medhod_profiler

https://github.com/change/method_profiler

* 特定のクラスのどのメソッドが処理に時間がかかったかをテーブル形式で表示。
* どのクラスが時間がかかってるのわかってれば便利なのかも


# Rbench

```
report "Squeezing with #squeeze" do
  one { "abc//def//ghi//jkl".squeeze("/") }
  two { "abc///def///ghi///jkl".squeeze("/") }
end
```

Benchmark.bmでいい気がする。Benchmark.bmをちょっとDSLっぽく書けるようにした感じ?

# bench_press

https://github.com/sandro/bench_press

```
require 'bench_press'
extend BenchPress
```

スクリプトの先頭でextendすれば、レポートを出力してくれる。
便利そうと思ったけど、自作のスクリプトで動かしてみたらレポート出力部で例外が出てしまった。
バグがあるかもしれない。

# (参考)Benchmark.ips

https://github.com/evanphx/benchmark-ips

Benchmark.bm はX回を何秒で実行できるか計測するが、Benchmark.ips は1秒で何回実行できるか計測する。




