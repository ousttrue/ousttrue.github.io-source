Title: wyam のテーマをカスタマイズする
Published: 2019-08-17 19:00
Tags: wyam
---
cssとかの調整。

## 調べる

* https://wyam.io/docs/
  * https://wyam.io/docs/extensibility/creating-a-theme
  * https://wyam.io/docs/extensibility/customizing-themes

ローカルにファイルを配置することでテーマをオーバーライドできると書いてあるのだが、
どのように配置するか正確なところがわからん。

試行錯誤したところ、

`input` にテーマのファイルを直接コピーしたら反映された。

`theme` フォルダでもよさそうなのだけど、 `input` しか `--watch` の対称にならないので、
`input` に入れてしまうのがよさそう。

```
input
  + assets
  + _Layout.cshtml
```

## レイアウトの構成

ASP.Net のtemplateエンジン、 [Razor](https://docs.microsoft.com/en-us/aspnet/core/mvc/views/razor?view=aspnetcore-2.2) で構成されていて拡張子は、 `cshtml` 。

レイアウトはBlog Recipeが規定している。

* https://github.com/Wyamio/Wyam/tree/develop/themes/Blog/BlogTemplate

サイトのルート(index), 各記事(post), 記事一覧(archive, tag), タグ一覧(tags)などがある。単純な例はこれ。

## テーマを作ってみる

* https://github.com/Wyamio/Wyam.git

をクローンして、`themes/Blog/BlogTemplate/*` を `input` にコピーする。
config.yml も `#theme BlogTemplate` とする。

前頁共通のレイアウトが `_Layout.cshtml` 。 その中の、 `@RenderBody()` にルート(_Index.cshtml), 記事(_PostIndex.cshtml), 記事一覧(_Archive.cshtml, Tag.cshtml), タグ一覧(_Tags.cshtml)がはめ込まれる様子。`_PostIndex.cshtml` だけ `_PostLayout.cshtml` にはめ込む。これは、命名規則で決まっていそう。`_PostLayout.cshtml` はさらに `_Layout.cshtml` にはめ込む記述があった。

日本語が文字化けするので、 `_Layout.cshtml` に `<meta charset="UTF-8">` だけ足す。
他とは、適当にやってみる。