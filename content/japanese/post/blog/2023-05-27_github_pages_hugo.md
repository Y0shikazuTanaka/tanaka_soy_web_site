---
title: '[健忘録] Github PagesとHugoで始める独自ドメインの静的Webサイト'
date: 2023-05-27T00:00:00+00:00
draft: false
tags:
  - blog
  - computer
---

Wordpressほど高機能は要らないけど、お金をかけずに自分のサイトが作れます。  
本サイトはHugoで作成した静的WebサイトデータとGithub Pagesで動いています。  
費用は独自ドメインの費用のみです。  

# Windows環境でHugoの環境構築

WindowsでHugoが動く環境を構築する

## 前提

Windowsのパッケージ管理ソフト、[Chocolatey](https://chocolatey.org/)がインストールされていること。  

## インストール

```
choco install hugo -y
choco install hugo-extended -y
choco install go -y
choco install git -y
```

## 確認

コマンドプロンプトで「hugo version」を実行し、以下のように表示されればOK。

```
PS C:\Users\yt\Develop\tanaka_soy_web_site> hugo version
hugo v0.112.3-ba6f74e40420d76f15fc8c2358be90f7aca98e0e+extended windows/amd64 BuildDate=2023-05-24T14:42:50Z VendorInfo=gohugoio
```

# Githubへサイト用のリポジトリを作成とローカルにCloneする

無料アカウントでGithub pagesを利用する場合、Publicリポジトリにする必要があります。  
適当な名前をつけて、公開リポジトリを作成します。  

## リポジトリのクローン

```
# git clone https://github.com/{user name}/{repo name}.git
git clone https://github.com/Y0shikazuTanaka/tanaka_soy_web_site.git
```

# Hugoで新しいサイトを作成する

## 新規プロジェクトの作成

```
# hugo new site {サイト名(英語)}
hugo new site tanaka_soy
```

## テーマの適応

```
cd ./tanaka_soy
# Other themes: https://themes.gohugo.io/
git submodule add https://github.com/lxndrblz/anatole.git themes/anatole
```

表示の検証のため、themes/anatole/exampleSite 内のフォルダ・ファイルをすべてコピーする。  

config.toml へテーマを適応

```
# ./config/_default/config.toml
theme = "anatole"
```

「hugo server」コマンドでWebサイトを確認する。  

```
hugo server
Start building sites …
hugo v0.112.3-ba6f74e40420d76f15fc8c2358be90f7aca98e0e+extended windows/amd64 BuildDate=2023-05-24T14:42:50Z VendorInfo=gohugoio

                   | JP | EN
-------------------+----+-----
  Pages            | 23 | 21
  Paginator pages  |  0 |  0
  Non-page files   |  0 |  0
  Static files     | 11 | 11
  Processed images |  0 |  0
  Aliases          | 10 |  9
  Sitemaps         |  2 |  1
  Cleaned          |  0 |  0

Built in 279 ms
Watching for changes in C:\Users\yt\Develop\tanaka_soy_web_site\{archetypes,assets,content,data,layouts,static,themes}
Watching for config changes in C:\Users\yt\Develop\tanaka_soy_web_site\hugo.toml, C:\Users\yt\Develop\tanaka_soy_web_site\config\_default
Environment: "development"
Serving pages from memory
Running in Fast Render Mode. For full rebuilds on change: hugo server --disableFastRender
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
Press Ctrl+C to stop
```

## CSSエラー回避

hugoコマンドでビルドし、htmlを出力したデータを開くと、表示が崩れ、ブラウザinspectを見るとCSSのエラーになる。  
Windowsでビルドした場合だけしか発生しないかもしれない。  

```
Failed to find a valid digest in the 'integrity' attribute for resource 'https://tanaka.soy/fontawesome/css/solid.min.35fc032da8ede6681675d20a2f862fb9e1045c1d512d495fcf862c054daffef2.css' with computed SHA-256 integrity 'VdgzNIGwegjgfPbzcxl1OitH6Z9MOVOUxXR7SLSVqps='. The resource has been blocked.
```

[stackoverflow](https://stackoverflow.com/questions/65040931/hugo-failed-to-find-a-valid-digest-in-the-integrity-attribute-for-resource/65052963#65052963)に解決策が載っていた。  

```
# themes\anatole\layouts\partials\head.html
integrity="{{ $style.Data.Integrity }}"
# TO
integrity=""
```

## ビルドしてリポジトリへPUSHする

hugoコマンドでビルドし、公開用のファイルを作成して、Gighubリポジトリへcommit & pushする。  

```
PS C:\Users\yt\Develop\tanaka_soy_web_site> hugo
Start building sites …
hugo v0.112.3-ba6f74e40420d76f15fc8c2358be90f7aca98e0e+extended windows/amd64 BuildDate=2023-05-24T14:42:50Z VendorInfo=gohugoio

                   | JP | EN
-------------------+----+-----
  Pages            | 23 | 21
  Paginator pages  |  0 |  0
  Non-page files   |  0 |  0
  Static files     | 12 | 12
  Processed images |  0 |  0
  Aliases          | 10 |  9
  Sitemaps         |  2 |  1
  Cleaned          |  0 |  0

Total in 226 ms
```

# 独自ドメインの設定

## config.toml へドメインとビルドの設定

baseURLへ独自ドメインを設定する。  
canonifyurlsをtrueにするとリソースのパスをいい感じにしてくれるらしい。  
Github pagesはdocsフォルダ内をWebサイトとして公開するため、ビルドファイルは「docs」を指定する。  

```
# ./config/_default/config.toml
publishDir = "docs"
canonifyurls = true
baseURL = "https://tanaka.soy/"
```

## 独自ドメインのDNS設定

私はさくらインターネットのメールボックスも運用しているので、独自ドメインの設定にメール設定も入っているが、GoogleDomainsの場合は以下のようになれば良い。  

{{< figure src="/images/post/blog/2023-05-27_095227.png" alt="image" caption="GoogleDomeins" class="center" >}}

## Github Pagesの設定

- Source
  - Deploy form a branch を選択
- Branch
  - master /docs を選択
- Custom domain
  - 自身のドメインを指定
- Enforce HTTPS チェックON

{{< figure src="/images/post/blog/2023-05-27_100029.png" alt="image" caption="GithubPages" class="center" >}}

# まとめ

CSSのエラーなど、ハマりポイントもあったが、個人ブログ程度であれば十分使える。  
また、静的サイトなので、表示も爆速である。