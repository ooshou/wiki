# 作成ツール  

## 導入方法について  

以下のコマンドを実行し，~/.command以下にファイルを移動すると使用可能となる  

```bash
mkdir ~/.command
echo "PATH=${PATH}:~/.command" >> ~/.bashrc
source ~/.bashrc
```

## overlay
オーバーレイに必要なファイルの生成やオーバーレイを行ってくれるコマンド   

> 生成と実行は同時に出来ないようになっている  

```bash
# オーバーレイに必要なファイルをxapp_testディレクトリに"xapp"という名前でテンプレートを生成する（あくまでもテンプレートの作成なので編集する必要あり）
overlay -c -n xapp -d xapp_test  

# 上記で作成したファイルを用いてオーバーレイの実行  
overlay -d xapp_test

# xapp_testに複数のbitファイル等がある場合は以下を実行  
overlay -d xapp_test -n xapp
```
