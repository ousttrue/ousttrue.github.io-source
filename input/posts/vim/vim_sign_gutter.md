+++
date = 2019-05-12T21:25:03+0900
tags = ['vim']
+++

# Vimのgutter表示

## 使い方

`piet` を定義して

```vim
:sign define piet text=>> texthl=Search
```

`piet` を `id=2` で配置する

```vim
:exe ":sign place 2 line=23 name=piet file=" . expand("%:p")
```

`id=2` を削除する

```vim
:exe ":sign unplace 2
```

