---
title: "alacritty+tmuxもいいけど、weztermがすごい件"
emoji: "😎"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["cli", "terminal"]
published: true
---

私はターミナルが大好きなので毎日使っているんですが、永らく alacritty + tmux を愛用してました。(といってもさっき見たら alacritty 使ってたのは 1 年ちょっとだったらしい・・・)
しかし最近 wezterm というターミナルの話を Reddit とかでちょくちょく聞くようになってたので 2022 年個人開発環境大変革[^1]に合わせて試してみることにしました。

[^1]: なぜかいろいろ乗り換えるタイミングが重なった（Linux の WM を i3 から sway に、Neovim の設定をすべて Lua に、Neovim の LSP を coc.nvim から nvim-lsp に、トラックボールを SlimBlade から Gameball に）

## wezterm とは？

wez さんが作った Rust 製の GPU-accelerated で cross-platform なターミナルです。自分の名前をプロダクトに入れるところに正直自信の表れを感じます w
https://github.com/wez/wezterm

wez さんは 2022 年現在 Facebook(meta)で働いているようです。
https://github.com/wez

まぁけど、Rust 製の GPU-accelerated で cross-platform なターミナルってそれ alacritty じゃんって思うかもしれないですが、次からすごいところを挙げて行きたいと思います。

## wezterm のすごいところ

### 1. カスタマイズ性がすごい

wezterm の設定ファイルはなんと Lua です。最近の設定ファイルは yaml や toml で書くことが多いと思いますけど、Lua はプログラミング言語なので if 文による変更や外部コマンド実行もできるため自由自在にカスタマイズできます。

例えば、今表示しているタブの内容（バッファ）を新しいタブとして Neovim で開くみたいなことができます。こうすればわざわざマウスでコピペせずに検索とか整形とかできて効率的だったりします。

```lua
local wezterm = require("wezterm")
wezterm.on("trigger-nvim-with-scrollback", function(window, pane)
	local scrollback = pane:get_lines_as_text()
	local name = os.tmpname()
	local f = io.open(name, "w+")
	f:write(scrollback)
	f:flush()
	f:close()
	window:perform_action(
		wezterm.action({ SpawnCommandInNewTab = {
			args = { "nvim", name },
		} }),
		pane
	)
	wezterm.sleep_ms(1000)
	os.remove(name)
end)

return {
  keys = {
    {key="E", mods="ALT", action=wezterm.action{EmitEvent="trigger-nvim-with-scrollback"}},
  }
}
```

ちょっと使ってみたくなりましたか？？
正直かなり遊べます。カスタマイズの感触としては tmux というよりも Vim/Neovim に近いです。

ターミナルは愚直に速く描画してくれればいいんだよ！って思ってた時期が私にもありました。。。

#### キーバインド変更

みんなよく使うキーバインド変更くらいなら Lua を知らなくても簡単に行うことができます。
以下はタブを新しく作成するキーバインドです。

```lua
{ key = "k", mods = "ALT", action = wezterm.action({ SpawnTab = "CurrentPaneDomain" }) },
```

https://wezfurlong.org/wezterm/config/keys.html

#### wezterm.on イベント

あるイベントが起こったら xxx をするというアクションは`wezterm.on`で実現することができます。

デフォルトのイベントも用意されていますので、好きなタイミングでフックして処理させることができます。
https://wezfurlong.org/wezterm/config/lua/window-events/index.html

EmitEvent を使うことでカスタムイベントを定義することもできます。（キー押したら xxx するなどが自由に定義できる）
https://wezfurlong.org/wezterm/config/lua/wezterm/on.html#custom-events

設定を動的に変更したいときなどは`set_config_overrides`が便利です。
https://wezfurlong.org/wezterm/config/lua/window/set_config_overrides.html

### 2. 標準でテーマがいっぱいあってすごい

「カスタマイズなんて興味ねぇよ、見た目が大事だろ！」っていうターミナルルッキズム派(そんな派閥があるかは知らない)の人にもおすすめできます。
標準で搭載されているテーマが無茶苦茶多いです。
https://wezfurlong.org/wezterm/colorschemes/index.html

もちろん、背景画像の設定や透過も普通にできます。
https://wezfurlong.org/wezterm/config/appearance.html

### 3. 気が利いてる機能が揃っててすごい

#### タブ, pane(ウィンドウ分割) 対応

高機能ターミナルにはだいたい付いてますが、urxvt や alacritty などシンプルさを売りにしてるターミナルは付いていないことが多いです。
新規作成も切り替えも tmux レベルでサクサク動きます(タブ, pane は tmux だと window, pane 相当になります)。

#### sixel 対応

alacritty では 2022/02/26 現在まだ対応していない sixel にも対応してます。sixel を使うとターミナルとこれまで相性が悪かった画像・動画が表示できるようになります。
![sixel](https://user-images.githubusercontent.com/8683947/155837143-ab945605-7165-473b-926d-7b9ff9de63e3.png)

ちなみに tmux は sixel に対応してないので wezterm 上で tmux を使った上で表示させようとしても表示されません。

#### リガチャ対応

私はリガチャフォントは使ってないですが、FiraCode とかのようなリガチャフォントにも対応してます。

#### QuickSelect

wezterm では、画面に表示されている文字をクイックにコピペする機能が標準で具備されています(tmux では[tmux-fingers](https://github.com/Morantron/tmux-fingers)相当)。
`QuickSelect`のキーバインドを設定したあと使用するとと描画されてるテキストの上にキーワード文字が表示されるので、その文字をタイプするとクリップボードに保存されます。

![quick-select](https://wezfurlong.org/wezterm/screenshots/wezterm-quick-select.png)
https://wezfurlong.org/wezterm/quickselect.html

#### CopyMode

tmux のコピーモードのようなこともできます。
https://wezfurlong.org/wezterm/copymode.html

ただし現時点ではコピーモードのキーバインドを変更することはできません。まあ Vim っぽいスタイルなので馴染む人も多いとは思います。
https://github.com/wez/wezterm/issues/993

### 4. ターミナルマルチプレクサ(tmux 相当)を内蔵しているのがすごい

wezterm の SSH domains という機能を使えば、ターミナルマルチプレクサをして wezterm を使えます。使い方は簡単で、リモート側に wezterm を入れて`wezterm connect`でつなぐだけです。セッションの保持もできるので、`wezterm connect` で起動したターミナルが途中で切れても、もう一度接続すると前の作業状態を復元することができます。
wezterm のインストールは [GitHub のリリース](https://github.com/wez/wezterm/releases)に各種バイナリあるので難しくありません。
https://wezfurlong.org/wezterm/multiplexing.html#ssh-domains

セッションの復元は不要だけど、ssh 先につないでいる状態で新しいタブを開いたら ssh 先にログインした状態でタブを開いて欲しいという要件だけだと`wezterm ssh` というコマンドが使えます。この機能だけだとリモート側で wezterm をインストールする必要はありません。
https://wezfurlong.org/wezterm/ssh.html

あとターミナルなので当たり前ですが tmux よりマウスフレンドリーです。
個人的には Issue のやりとりをいろいろ見て tmux 飲み込んで行くぜって気概を感じるところが好きです。

#### 具体的な tmux の機能との対比表

| 機能                                       | tmux                             | wezterm         |
| ------------------------------------------ | -------------------------------- | --------------- |
| セッション復元                             | 自動的に保持される               | wezterm connect |
| ssh 先でのタブ管理                         | ない（やる場合は独自実装が必要） | wezterm ssh     |
| セッション機能(タブをひとまとめにする機能) | session                          | ない            |
| タブ                                       | window                           | tab             |
| pane(タブ内を分割する)                     | pane                             | pane            |

### 5. ドキュメントの充実っぷりがすごい

公式ドキュメント開いてちょっと色々ページ開いてみてください。
https://wezfurlong.org/wezterm/

すごくないですか？？
なにがすごいかって言うと、

- ボリュームがすごい
- 適切に階層かされてて理解しやすい
- ちゃんと相互リンクもされてて
- 検索も使いやすい
- 例も載ってるので Lua わからなくてもコピペですぐ使える
- バージョン xx から導入されたみたいなのもわかりやすい

個人プロジェクトでここまでドキュメントが整備されているものはなかなか見ることはできません。

## wezterm がまだイマイチなところ(alacritty + tmux と比べて)

wezterm を持ち上げまくりましたが、alacritty + tmux を完全代用する上でまだ機能が足りてない部分は正直ちょこちょことあります。

### tmux の window, pane 切り替えのような操作ができない

tmux では`break-pane`や`join-pane`で簡単に window と pane を切り替えることができますが、現状 wezterm だとそれができません。
https://github.com/wez/wezterm/issues/1253

また個人的に結構使っていた tmux のポップアップ機能に相当する機能もまだ実装されてません。
https://github.com/wez/wezterm/issues/270
![2022-02-27_03-50](https://user-images.githubusercontent.com/8683947/155855522-0dd3b116-a88f-4e7d-bfc8-71a2c65f3949.png)
_fzf-tmux で ctrl-r を表示したりしてた_

### tmux のセッションに相当する機能がない

tmux には複数の pane, window をまとめるセッションが wezterm にはありません。やるとしたら新しくウィンドウを作るくらいしかないです。

### プラグインエコシステムがない

tmux では tpm を使ってプラグインをインストールすることができます(最近はあまり流行ってない気もしますが・・・)
wezterm ではプラグイン相当の機能がまだないため、いい機能ができたとしてもその人の Lua をコピペするしか手段がありません。

## wezterm はじめの一歩

長々と機能の紹介をしましたが、さくっと初めるためのインストール・設定方法を少しだけ紹介します。

### インストール

各種 OS のインストール情報はこちらになります。どこ OS でも複数やり方が提供されていてかなり充実していると思います。
https://wezfurlong.org/wezterm/installation.html

### 設定

alacritty 風に wezterm 始めるときの設定は日本人だとこんな感じになるかと思います。特に`use_ime`は大事です。

```lua: .config/wezterm/wezterm.lua
local wezterm = require 'wezterm';

return {
  font = wezterm.font("Cica"), -- 自分の好きなフォントいれる
  use_ime = true, -- wezは日本人じゃないのでこれがないとIME動かない
  font_size = 10.0,
  color_scheme = "OneHalfDark", -- 自分の好きなテーマ探す https://wezfurlong.org/wezterm/colorschemes/index.html
  hide_tab_bar_if_only_one_tab = true,
  adjust_window_size_when_changing_font_size = false,
}
```

あとデフォルトキーバインドなんてクソ喰らえだって人は
`disable_default_key_bindings = true,`
が必要です。

## 個人的に移行してみて

今のターミナルの見た目はこんな感じにしてます。tmux 風になるように一番下にタブバーをおいています。
![overview](https://user-images.githubusercontent.com/8683947/155835836-56cedf64-c24e-41bb-bfda-04f411261480.png)

設定はこちらです。
https://github.com/yutkat/dotfiles/tree/master/.config/wezterm

### 移行してよかったこと

- tmux のレイヤーを意識しなくてよくなった
  - キーシーケンスが吸われたりとか、キーコードが変わったりとかに対応しなくてよくなった
  - ssh 先で使っている場合、最新のバージョンの tmux が手に入らずビルドする必要から解放された
- tmux をインストールしたくないような環境でもタブを開くことができるようになった(wezterm ssh)
- 日本語表示は問題なかった
- パフォーマンスも特に気にならなかった
- sixel が使えるようになった(まだあまり活用できていない)

### 移行して気になってるところ

#### なんかたまに終了に失敗する

`exit` するとたまに以下のような画面が表示されて自動で閉じられないことが私の環境では起こっています。発生したときは Window ごと閉じるようにしてます。
![2022-02-27_03-38_1](https://user-images.githubusercontent.com/8683947/155855166-e3a73035-38dc-413b-a99b-769f19b8f77b.png)

#### Neovim 使用時に謎のスペース？

TUI プログラムによっては画面いっぱいに表示されない（1 行分くらい間があいてしまう）ことがあります。
フォントサイズによってはきっちりハマることもあります。
![謎のスペース](https://user-images.githubusercontent.com/8683947/155835835-63ce3b2d-21a3-4257-b95b-99a286b37577.png)

#### ウィンドウの変更にちょっと弱い

下にタブをおいた場合などウィンドウ変更にちょっと弱いです。
![取り残されたタブ](https://user-images.githubusercontent.com/8683947/155835832-17bdecb3-f6b9-4f35-9ae3-7cb74448a1fd.png)
ちなみに再描画(ReloadConfiguration)すればきれいになります。

#### ウィンドウがアクティブじゃない状態でマウスカーソルで選択しようとしたときの挙動がなんか変

https://github.com/wez/wezterm/issues/1540

### Tips

#### タブを tmux みたいに

タブを tmux みたいなプロセス名にしたい人は参考にしてみてください

```lua
wezterm.on("format-tab-title", function(tab, tabs, panes, config, hover, max_width)
	local title = wezterm.truncate_right(utils.basename(tab.active_pane.foreground_process_name), max_width)
	if title == "" then
		title = wezterm.truncate_right(
			utils.basename(utils.convert_home_dir(tab.active_pane.current_working_dir)),
			max_width
		)
	end
	return {
		{ Text = tab.tab_index + 1 .. ":" .. title },
	}
end)
```

#### デバッグの仕方

設定がプログラミング言語ということは負の側面もあって、まぁバグるんですよね。そしてどこがバグったか調べるために printf デバッグする必要があります。
デバッグの方法は簡単で、設定ファイルに以下みたいな感じで log を吐くようにすれば OK です。

https://wezfurlong.org/wezterm/config/lua/wezterm/log_error.html

```lua
local wezterm = require 'wezterm';
wezterm.log_error("Hello!");
```

ただ私はこれがどこに出力されるかわからなくて 10 分くらいさまよってしまいました（ログファイルとか一生懸命探して）。出力させるには別ターミナルで`wezterm` と実行してそちらのウィンドウに表示される stdout を見るというスタイルのようです。

## 最後に

wezterm は機能が多いためシンプルさを保っている alacritty と比べると細かい描画不具合等はありますが、もう十分に常用することが可能なターミナルになってると思います。
特に設定のカスタマイズ性とターミナルマルチプレクサは個人的にはかなり革命的でした。

春に向けて心機一転ターミナルの乗り換えを検討してみてはいかがでしょうか？？

---

:::message
ちなみにタイトルは昔よく参考にしていた [b4b4r07](https://qiita.com/b4b4r07)さんの記事のオマージュです
:::
