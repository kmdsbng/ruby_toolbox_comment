! Amazon Web Service gems


FogとAWS sdkがダウンロード数が伸びてる。AWS sdkのほうが新し目。AWS sdkはamazonが作ってる。



!!! Fog
https://github.com/fog/fog

```
gem install fog
```

```
>> server = Compute[:aws].servers.create
ArgumentError: image_id is required for this operation
>> server = Compute[:aws].servers.create(:image_id => 'ami-5ee70037')
<Fog::AWS::EC2::Server [...]>
>> server.destroy # cleanup after yourself or regret it, trust metrue
```
インスタンスの作成、削除ができるらしい。

```
require'fog'

compute=Fog::Compute.new(
  :provider           =>'Rackspace',
  :rackspace_api_key  =>key,
  :rackspace_username=>username
) # boot a gentoo server (flavor 1 = 256, image 3 = gentoo 2008.0)
server=compute.servers.create(:flavor_id=>1,:image_id=>3,:name=>'my_server')
server.wait_for{ready?} # give server time to boot

# DO STUFF

server.destroy # cleanup after yourself or regret it, trust me
```

サーバ起動して処理させてサーバ破棄する例




!! aws-sdk
https://github.com/aws/aws-sdk-ruby

amazon製のgem

```
gem install aws-sdk
```

パッと使えるツール群ではなく、sdkみたい。
サーバの起動処理も見てみたけど、結構スクリプトが長い。
https://github.com/aws/aws-sdk-ruby/blob/master/samples/ec2/run_instance.rb


Fogで用が足りてるなら、Fog使うほうが簡単そう。
Fogでない機能を扱いたいなら、使用を検討してもいい。


