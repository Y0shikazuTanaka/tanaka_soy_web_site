---
title: 'Intel AX210 WiFi&Bluetooth モジュール購入'
date: 2023-06-05T00:00:00+00:00
draft: false
tags:
  - blog
  - computer
---

ディスクトップPCでWiFiを利用したいため、[Intel AX210](https://www.amazon.co.jp/gp/product/B088NHCX46?tag=maftracking364812-22&linkCode=ure&creative=6339) WiFiカードを購入した。

{{< figure src="/images/post/blog/2023-06-05_04.jpg" alt="image" caption="" class="center" >}}

# WiFi Directは対応WiFiカードでしか使えない

WiFi Directを利用したいのは、Androidタブレットの画面をPCへ映したいからだ。  
今までディスクトップPCは有線LAN接続だったため、WiFiカードやUSBアダプタを搭載したことはなかった。  
しかし、Androidなどのモバイル端末との直接接続はWiFi Directを利用することが多く、ディスクトップでもWiFiカードを搭載しないとWindows標準機能でも利用できない機能が存在する。  

# Androidのワイヤレスディスプレイ(Miracast)を使ってPCへ画面を転送する

Android標準の画面キャスト機能、Miracastを使ってPCへタブレットやスマホの画面を転送する設定をする。  
MiracastはAndroid4.2から標準対応となっているが、使えるかどうかは端末次第らしい。  
私が持っている、激安スマホ「UMIDIGI A11」と13インチタブレットの「Lenovo Yoga Tab13」では使えた。  
使えない端末のほうが珍しいのでは？  

## Windows11側の設定

Windows11は標準でワイヤレスディスプレイに対応しているが、初期インストール状態ではソフトがインストールされていない。  
このため、追加でパッケージをインストールする必要がある。

### オプションの追加パッケージのインストール

Windows11の Settings → Apps → Optional features の画面まで行く。  
「Wireless Display」をインストールする。  

{{< figure src="/images/post/blog/2023-06-05_01.png" alt="image" caption="" class="center" >}}

「Wireless Display」の接続アプリが使えるようになるので、起動する。  

{{< figure src="/images/post/blog/2023-06-05_02.png" alt="image" caption="" class="center" >}}

## Android側の設定

設定の画面を開き、接続済みのデバイス → 接続の設定 → キャスト を開く。  
自身のWindows11のPC名が表示されるので、接続する。

{{< figure src="/images/post/blog/2023-06-05_03.png" alt="image" caption="" class="center" >}}

# まとめ

遅延はあるので、ゲームなどを遠隔操作するのは難しいかもしれないが、離れて暮らす親とかに設定を教えたりするのには便利だと思う。