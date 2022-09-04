# wifi関連  

ここではwifi関連の問題について記載する  

wifiが接続できない場合，以下の解決策？がある  

- 接続するルータを変更する  

- wifiデーモンの起動  

以下は失敗したが，一応記載  

- nmcliコマンドを使用して，周囲のwifi確認  

## 接続するルータを変更する  
ルータの配置場所によっては携帯やPCはwifiが接続出来るのに，ultra96v2は出来ないといった場合がある  
その場合に一番早いのがルータを目の前まで移動させることである．  
実家暮らしの場合，それが出来ないためここでは携帯のテザリング方法を記載する．
> 注意 :  ここではiphoneでのテザリング方法の説明を行う．Androidは知らない  

### iphone-ultra96v2の有線接続    
まだ
### iphone-ultra96v2の無線接続  
まだ
## wifiデーモンの起動
今回使用するDebianはOS起動時にwifiデーモンが起動する  
wifiデーモンは一定時間wifiに接続できないとタイムアウトを発生させwifiデーモンを終了する  
その場合は以下のコマンドを実行し，wifiデーモン起動を行う  
なお，`ifup: interface wlan0 already configured`と表示される場合は既に起動している  
```bash
sudo ifup wlan0
```

## nmcliコマンドを使用して，周囲のwifi確認

失敗
nmcliコマンドをインストールするとwifiが接続できなくなる  
wifi接続デーモンが2つ以上動作し，競合するだめだと考えている  
<details>
<summary>開く</summary>

標準ではnmcliコマンドはインストールされていないため，
一度有線で接続し，以下を実行してインストールする 　

[参考サイト](https://tarufu.info/ubuntu-wifi-connect/#toc1)

```bash
sudo apt -y install network-manager  
```

次に，以下のコマンドを入力し，接続可能なwifiを確認する  

```bash
nmcli device wifi
```

</details>

