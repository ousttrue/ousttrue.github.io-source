Title: wyam のテーマをカスタマイズする
Published: 2019-08-17 19:00+9
Tags: wyam
---
cssとかの調整。

## 調べる

* https://wyam.io/docs/
  * https://wyam.io/recipes/blog/themes/
  * https://wyam.io/docs/extensibility/creating-a-theme
  * https://wyam.io/docs/extensibility/customizing-themes

ローカルにファイルを配置することでテーマをオーバーライドできると書いてあるのだが、
どのように配置するか正確なところがわからん。

試行錯誤したところ、

`input` にテーマのファイルを直接コピーしたら反映された。

`theme` フォルダでもよさそうなのだけど、 `input` しか `--watch` の対象にならないので、
`input` に入れてしまうのがよさそう。

```
input
  + assets
  + _Layout.cshtml
```

## レイアウトの構成

ASP.Net のtemplateエンジン、 [Razor](https://docs.microsoft.com/en-us/aspnet/core/mvc/views/razor?view=aspnetcore-2.2) で構成されていて拡張子は、 `cshtml` 。

レイアウトはBlog Recipeが規定している。

サイトのルート(index), 各記事(post), 記事一覧(archive, tag), タグ一覧(tags)などがある。単純な例はこれ。

* https://github.com/Wyamio/Wyam/tree/develop/themes/Blog/BlogTemplate

## テーマを作ってみる

* https://github.com/Wyamio/Wyam.git

をクローンして、`themes/Blog/BlogTemplate/*` を `input` にコピーする。
config.yml も `#theme BlogTemplate` とする。

共通のレイアウトが `_Layout.cshtml` 。 その中の、 `@RenderBody()` にルート(_Index.cshtml), 記事(_PostLayout.cshtml), 記事一覧(_Archive.cshtml, _Tag.cshtml), タグ一覧(_Tags.cshtml)がはめ込まれる様子。

`_PostIndex.cshtml` は廃止された。

> - **[Breaking Change]**[Refactoring] Moved Blog recipe theme file `/_PostIndex.cshtml` to `/_Archive.cshtml`, no other changes should be needed to this file in themes other than to move it - sorry for the rename (again), the first name was kind of dumb, this one is better

日本語が文字化けするので、 `_Layout.cshtml` に `<meta charset="UTF-8">` だけ足す。
あとは適当にやってみる。

## cshtml からアクセスできる変数

* Model
* Context

```cshtml
<a href="@Context.GetLink(Context.String(BlogKeys.PostsPath))">Back To posts</a>
```

## 作業メモ

* scss(wyamが対応している)
* highlight.js (phantom themeからコピー)
* 記事内のTOC

### ToDo

* https://konpa.github.io/devicon/
* http://fizzed.com/oss/font-mfizz
