---
title: "zshでもIDEみたいに自動補完したい！zsh-autocompleteの紹介"
emoji: "💨"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["zsh"]
published: true
---

シェルでも IDE みたいに Tab を押さなくてもインクリメンタルな自動補完して欲しいって思ったことないですか？
5 回に 1 回くらい気がついたら Tab を自然にタイプしているそこのあなたに朗報です。

この zsh-autocomplete を使えばなんと不要な Tab 打ちから解放されることができます 🎉
https://github.com/marlonrichert/zsh-autocomplete

![file-search](https://github.com/marlonrichert/zsh-autocomplete/blob/main/.img/file-search.gif?raw=true)

## 今までの方法との違い

実は昔から自動補完候補を出す zsh プラグインは存在しました。
[incr-0.2.zsh](https://mimosa-pudica.net/zsh-incremental.html や
https://github.com/hchbaw/auto-fu.zsh
になります（なぜか２つとも日本人作者）

しかしこの２つのプラグインとも古く、更新が止まっています。(2013 年が最終更新日)

他にも似たようなものでよく使われてるのが
https://github.com/zsh-users/zsh-autosuggestions
になりますが、こちらは自動補完はしてくれますが全候補ではなく 1 候補だけの表示となります。

そこで、2020 年にさっそうと現れたのが zsh-autocomplete となります。

## zsh-autocomplete の利点

- Tab を打たなくていいところ
- 項目が常に表示されるので本当に Tab を打つべきタイミングがわかること
- 非同期に処理してくれるのであまり入力の邪魔にならないところ
- 候補が多かった場合にうまく省略してくれるところ

## こういう人におすすめ

- Tab を打つのがうんざりしている人
- なんか動的にいっぱい表示されるリッチな画面が好きな人

## こういう人はやめておいた方がいいかも

- 補完設定をいろいろカスタマイズしていて zsh-autocomplete でもそれをやろうとする人
  - 補完カスタマイズするとうまく動かなくなってしまうことが多いので[公式の設定](https://github.com/marlonrichert/zsh-autocomplete/blob/main/.zshrc)の範囲だけをいじるようにしたほうがいいです。
- 見た目を変えたりや不要な機能を制限するのが好きな人
  - どちらかといえば作者の設定に従えタイプのプラグインとなります(こういう処理は副作用がいろいろ多いため下手にいじるとアップデートでよく壊れます)
- zsh プラグインいっぱい入れてるけどあまりメンテナンスはしなくない人
  - 副作用が強いので他のプラグインとの起動順などうまく調整する必要があります。

## 設定する上での注意点

プラグインを読み込む前に設定するパラメーターと読み込み後に設定するパラメーターに分かれています。 [分岐点はここ](https://github.com/marlonrichert/zsh-autocomplete/blob/7ab87cb20ba6f155eb38e6199c970fefef49fb75/.zshrc#L58)
各種設定をする際は読み込むタイミングを間違えないでください。

zinit を使ってる場合は`atinit`と`atload`を使って制御すればよいです。

## 他の方法

ターミナルの機能として補完機能を具備しているものもあります。
https://github.com/Inlustra/hyper-autocomplete
https://github.com/withfig/fig

ちょっと変わった手法だとコマンドを実行したあとに独自プロンプトを表示して、その中でなら自動補完をポップアップできるみたいなツールもあります(これの補完は git だけになりますが)
https://github.com/chriswalz/bit

## 個人的な感想

個人的にはどこにおいても自動補完処理は必須なので、プラグインではなくてシェル側とターミナル側でうまくやってくれるような未来になることを期待してます。。。

こういうシェルが欲しいです

- デフォルトでそこそこリッチな表示(git prompt とか色とか)
- 補完が IDE みたいな感じ
- 各所で FuzzyFinder っぽい絞り込みができる
- GitHub からパッケージをインストールできる
- ちゃんとした言語のシェルスクリプト
- 補完定義が書きやすい
- 各イベントでフックしやすい
