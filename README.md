# 必要なもの
choco install hugo
choco install hugo-extended
choco install go

# set up

```
hugo new site tanaka_soy
cd ./tanaka_soy/themes
git clone https://github.com/lxndrblz/anatole.git anatole
```

tanaka_soy/themes/anatole/exampleSite をtanaka_soyへ全コピ

```hugo server```

http://localhost:1313/

画像フォルダ
\tanaka_soy\static\images

# CSSエラー回避

https://stackoverflow.com/questions/65040931/hugo-failed-to-find-a-valid-digest-in-the-integrity-attribute-for-resource/65052963#65052963

\themes\anatole\layouts\partials\head.html

```
integrity="{{ $stylesheet.Data.Integrity }}"
# TO
integrity=""
```