---
title: "コメントを//で書くか;で書くか"
type: "post"
date: 2021-07-14
url: 2021-07-14/hsp3-comment-style
tags:
  - Hsp3
---

HSP3は `;` と `//` の2種類のコメントがあって、長いこと `//` を使ってきたけど、`;` に変えるかも……という話。(わりとどうでもいい話。)

<!--more-->

## HSP3のコメントの構文

HSP3には改行までのコメントアウトのために2種類の構文がある。

- `;` (BASIC風)
- `//` (C++風)

公式のスクリプトは `;` を使っていることがほとんどだと思う。

私がHSP3で `//` を使うようになったのはたしか10年ぐらい前から。当時C++を触りだして、`//` のほうが「一般的」だということを知ったからだったと思う。
ただ改めて思うと「一般的」というのは必ずしも事実でなかった。

コメントの記号は言語によって千差万別といってよく、人気のある言語だけでも `#` や `--` をよくみる。
`;` をコメントとするのも、アセンブリ風の言語や設定ファイル系の言語でよくみる。

そのため `//` を使うべき積極的な理由はない。
むしろ多数派の `;` を使うべき、ということに最近気づいた。

## VSCodeの拡張機能

これに気づいたきっかけはVSCodeの拡張機能だ。

VSCodeでは Ctrl+/ を使うと行のコメントアウトを切り替える機能がある。
この機能のため、拡張機能側でコメントの記号を選ぶ必要がある。

HSP3の拡張機能としてはおそらく language-hsp3 がもっとも使われていて、これは `;` をコメントにしている。
つまり Ctrl+/ を押すと行頭に `;` が挿入または除去される。

自作の拡張機能である `hsp3-vscode-syntax` では `//` を使うように設定してある。

## 影響

そういうわけで knowbug、hsp3-ginger、hsp3-modules などのコードベースで `//` から `;` への変更を行うかもしれない。
`hsp3-vscode-syntax` の次のメジャーバージョンではコメントの記号が `;` になるかもしれない。

----

## 余談: ifのカッコ

関連した話題として、ifの条件式をカッコで囲むかどうかというのがある。

C言語のif文の構文では、条件式全体をカッコで囲む必要がある。
一方HSP3では、条件全体をカッコで囲む必要はない。

```js
    // 条件式をカッコで囲むとき
    if (条件) { 本体 }

    // 囲まないとき
    if 条件 { 本体 }
```

私は以前まで「囲む」ように書いていた。そうし始めたのも、コメントを `//` にしたのと同じ時期で、理由も似たようなものだと思う。

他の言語をみてみると、たしかにifの条件式をカッコで囲むのが必須な言語は少なからずある。
しかしここ10年ぐらいに設計された言語では、C系の言語でも、ifの条件式は別にカッコで囲まなくてもよくなっている。Rust、Go、Swiftなど。
また、C言語の影響にないOCamlなどの言語では昔から `if 条件 then 本体` という構文であり、カッコはない。

HSP3の構文的に、条件式の周りのカッコは冗長なだけで、積極的に書く利点はない。
そういうわけで、ここ数年で書いたコード (例えばknowbugのコード) では、条件式をカッコで囲んでいない。