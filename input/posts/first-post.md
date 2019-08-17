Title: wyam ことはじめ
Published: 2019-08-17
Tags: wyam
---
ということで、またサイトを作りなおし。
[wyam](https://wyam.io/)を使ってみる。

## インストール

```
$ dotnet tool install -g Wyam.Tool
```

## 初期化する

```
$ mkdir site
$ cd site
$ wyam new --recipe blog
```

* config.wyam(siteの設定)
* input(記事置き場)
  * about.md
  * posts
    * first-post.md

### 設定ファイル

config.wyam がそれで、C# を Roslyn で処理するらしい。
おもしろい。

```
// config.wyam
#recipe Blog
#theme Phantom

// Customize your settings and add new ones here
Settings[Keys.Host] = "ousttrue.github.io";
Settings[BlogKeys.Title] = "三次元日誌";
Settings[BlogKeys.Description] = "programming とか";

// Add any pipeline customizations here
```

`#recipe Blog` がパイプライン設定で、 input フォルダの構成と処理を設定している。
設定ファイルに展開したものを記述することもできるみたい。

### gitignore

https://wyam.io/docs/advanced/what_to_exclude_from_source_control

```
#.gitignore
.vs/
output/
config.wyam.hash
config.wyam.dll
config.wyam.packages.xml
```

## 生成する

```
$ wyam
```

* output
  * index.html

`$ wyam --watch --preview` で更新を監視して livereload できる。

## テーマを変えてみる

* https://wyam.io/recipes/blog/themes/

コマンドラインに、 `--theme THEME_NAME` とするか config.wyam に

```
// config.wyam
#theme THEME_NAME
```

とすれば OK。

## appveyor で GitHub-Pages に展開

https://wyam.io/docs/deployment/appveyor
