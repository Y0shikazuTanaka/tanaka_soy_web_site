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