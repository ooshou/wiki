# 環境構築  

ultra96v2に回路のオーバーレイが可能なDebianのインストールを行う  

必要なものは以下の通り  

- ultra96v2  
- micro SDカード  
- ubuntu PC

## ubuntu PCの作業  

### 環境のダウンロード  

``` bash
git clone git://github.com/ikwzm/ZynqMP-FPGA-Linux
cd ZynqMP-FPGA-Linux
git checkout v2019.2.1
git lfs pull
```

</br>

### 書き込み  

``` bash
# マウント先の確認  
sudo fdisk -l

# ここでは，/dev/mmcblk0??にマウントされたとする  
mount /dev/XXXXXX1 /mnt/usb1
mount /dev/XXXXXX2 /mnt/usb2

# ブート パーティションの作成
cp target/Ultra96-V2/boot/* /mnt/usb1
rm /mnt/usb1/boot.bin
# 今使用している回路対応のboot.binを使用する
mv /mnt/usb1/boot_outer_shareable.bin mnt/usb1/boot.bin

# RootFS パーティションの作成
tar xfz debian10-rootfs-vanilla.tgz -C /mnt/usb2
# ドライバのコピー
mkdir /mnt/usb2/home/fpga/debian
cp linux-image-4.19.0-xlnx-v2019.1-zynqmp-fpga_4.19.0-xlnx-v2019.1-zynqmp-fpga-3_arm64.deb /mnt/usb2/home/fpga/debian
cp linux-headers-4.19.0-xlnx-v2019.1-zynqmp-fpga_4.19.0-xlnx-v2019.1-zynqmp-fpga-3_arm64.deb /mnt/usb2/home/fpga/debian
cp fclkcfg-4.19.0-xlnx-v2019.1-zynqmp-fpga_1.2.0-1_arm64.deb /mnt/usb2/home/fpga/debian
cp udmabuf-4.19.0-xlnx-v2019.1-zynqmp-fpga_1.4.2-0_arm64.deb  /mnt/usb2/home/fpga/debian
```

次は以下を/mnt/usb2/etc/fstabに追記する  

``` 
/dev/mmcblk0p1 /mnt/boot auto defaults 0 0
```

wifi のセットアップとして，**ssid**と**psk**を取得  

``` bash
wpa_passphrase ssssssss ppppppppp
network={
    ssid="ssssssss"
    #psk="ppppppppp"
    psk=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
}
```

`/mnt/usb2/etc/network/interfaces.d/wlan0`に**ssid**と**psk**を記載する  

```
auto  wlan0
iface wlan0 inet dhcp
    wpa-ssid ssssssss
	wpa-psk  xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

## ultra96v2の作業  

### ドライバのインストール  

### apt update & upgrade

### bootgenのインストール  

[参考サイト](https://qiita.com/ikwzm/items/97811fcff7876181209f)

``` bash
git clone https://github.com/Xilinx/bootgen
cd bootgen
make
cp bootgen /usr/local/bin
which bootgen  
```


### "sudo: unable to resolve host debian-fpga: Name or service not known"の止め方  

ultra96v2にて，以下を実行すると出なくなる  

```bash
sudo sh -c 'echo 127.0.1.1 $(hostname) >> /etc/hosts'
```