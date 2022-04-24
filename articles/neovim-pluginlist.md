---
title: "Neovimプラグインをまともに選定できるリストを作った"
emoji: "📝"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["neovim"]
published: true
---

ちょっと前に自分の使っている Neovim プラグインをまとめましたが、

https://zenn.dev/yutakatay/articles/neovim-plugins-2022

他にもどういう競合プラグインがあるのか知りたい人もいると思いましたので、競合プラグインも一同に会した Neovim プラグインのリストをまとめてみました。

↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓

https://github.com/yutkat/my-neovim-pluginlist

↑ ↑ ↑ ↑ ↑ ↑ ↑ ↑ ↑ ↑ ↑ ↑ ↑ ↑ ↑ ↑ ↑ ↑ ↑ ↑ ↑ ↑ ↑ ↑ ↑ ↑ ↑ ↑ ↑ ↑ ↑ ↑

ちなみに目次だけでこの長さあります。

![Kooha-04-24-2022-17-43-09](https://user-images.githubusercontent.com/8683947/164968181-2d6a9949-7c52-4198-b5bb-c2892dc12325.gif)

## なんで awesome じゃダメだったの？

このリスト以外にも似たような用途として利用されるものに awesome があります。
neovim プラグインもまとめれられてるものがあり

https://github.com/rockerBOO/awesome-neovim

になります。

### Awesome の欠点

私も awesome を結構見るのですが、正直あんまり好きではないです。

理由は以下となります。

- 情報が羅列されているだけであまりカテゴリが整理されていない
- 結局どれがいいのか選ぶのに十分な情報がない
- 古いものやもう使わなくてもよいものなどが整理されない
- 公平性がある程度大事になってくるのでプラグイン選定が好きな人が追加する情報もそうでない人の情報も平等に扱われてしまう

### どういうふうに改善すればよいか

- 情報が羅列されているだけであまりカテゴリが整理されていない
  - → カテゴリ分けを充実させる。完全に競合なプラグインが 2 つ以上存在する場合は新規でカテゴリを作る。
- 結局どれがいいのか選ぶのに十分な情報がない
  - → 選定に有益な情報（スター数はアクティビティ）を追加する。
  - → 逆にプラグインの説明みたい必要のないものは削除する（だいたい速くて使いやすくてとかみたいな無駄な情報しか書いてないから）。
- 古いものやもう使わなくてもよいものなどが整理されない
  - → 最終更新日時を追加する。
  - → CI で archived になっているものを検出する。
- 公平性がある程度大事になってくるのでプラグイン選定が好きな人が追加する情報もそうでない人の情報も平等に扱われてしまう
  - → 自分のおすすめはカテゴリの一番上に持ってくる。

## だから自分専用のプラグインリストを作った

上の改善案を満たすように Markdown 上に shields.io のバッジを貼ったリストを作成しました。(もっといいやり方があるかもしれませんがとりあえず一番簡単だったので)

![auto-completion](https://user-images.githubusercontent.com/8683947/164970732-103e79db-a371-4df5-b232-3475588fe7f8.png)

自動補完部分を例として上げますが、一番スター数が多くて人気がありそうなのが nvim-cmp で勢いがあるのが coq_nvim だということがひと目でわかります。

現状 README に設置しているバッジは [shields.io](https://shields.io/) から直接参照しているので初回読み込みに時間がかかります。
GitHub Actions で 1 日 1 回更新して Markdown に吐き出す形式にするのがよいかもしれません。一応少しでも速く読み込めるようプラグイン数の多いカテゴリは別ファイルにしてます。

また更新がめんどくさくならないように運用負荷を最小にするようスニペット(LuaSnip)を活用してます。これを使えば見つけたプラグイン名を貼るだけ、ものの 5 秒で更新できます。

```lua
	s("badge_link", {
		t({ "- [" }),
		i(1, { "repo/name" }),
		f(function(args, snip)
			return string.format(
				"](https://github.com/%s) ![](https://img.shields.io/github/stars/%s) ![](https://img.shields.io/github/last-commit/%s) ![](https://img.shields.io/github/commit-activity/y/%s)",
				args[1][1],
				args[1][1],
				args[1][1],
				args[1][1]
			)
		end, { 1 }),
	}),

```

### 新着プラグイン情報を得る方法

リストだけだとどれが新しく追加されたプラグインなのかコミットログからいちいち判断する必要があり大変かと思います。
ですので新着プラグインでよさそうなものだけを抜粋して私が Twitter の #neovim_plugins のハッシュタグでつぶやいてます(日本語)。
よければチェックしてみてください。

https://twitter.com/hashtag/neovim_plugins

## そもそも他のエディタではどうやってるの？

Neovim 以外の他のエディタ(VS Code など)でも、同様のプラグインを選定するツラミは発生すると思いますが Neovim に比べると苦労は少ないはずです。
なぜかというとそれは**_マーケットプレイス_** があるからです。

https://marketplace.visualstudio.com/vscode

カテゴリもきちんと用意されており、評価を表す星があり、コメントも記入でき、ダウンロード数も見ることができます。
さらに最近勢いのあるプラグインや新着プラグインもわかってプラグイン選びには最高の環境ですね。

**_VS Code ユーザーはこの無償で与えられているこの仕組みにもっと感謝すべき！_**

ちなみに Neovim でもプラグインの標準仕様のフォーマットを決める動きが出てきてます。これが実現できればマーケットプレイス的なものが実装されるの日も来るかもしれません。

https://github.com/nvim-lua/nvim-package-specification

https://youtu.be/ctwNbfAMheM?t=189