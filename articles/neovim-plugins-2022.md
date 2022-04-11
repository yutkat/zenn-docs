---
title: "ワシの使っているNeovimプラグインは200個近くあるぞ"
emoji: "🎾"
type: "idea"
topics: ["neovim"]
published: true
---

昔はこういうの結構やられてた気がするけど最近あんまり見なくなったのでやってみました。

タイトルは
https://daisuzu.hatenablog.com/entry/2012/05/06/204019
から借用しました。

## 注意点

- プラグイン自体の説明はあまりするつもりはないので、GitHub の README を読むなり使ってみるなりしてみてください。
- 私は結構頻繁にプラグイン乗り換えるので 2022 春バージョンと思ってください。
- 私が言うのもあれですが、プラグインはいっぱい入れればいいというものではありません。ひとつひとつを使いこなすのが大事です。多ければそれだけ管理も大変です。
- 競合があるプラグインは比較して選定しているつもりですが、あくまでも私の趣味の範囲での選定となります。絶対的な指標があってこっちの方が優れているといった判断をしているわけではありません。

## 私の Neovim の使い方

使い方が違うと参考にならないことが多いため前提としてどういうふうに Neovim を使っているか書いておきます。

- Neovim を IDE のようにして使っています。（いわゆる Neovim IDE 派です）
- 用途は、コーディング、ドキュメント作成などほぼすべてで使っています。
- OS は Linux でタイル型の WM を使っています。
- Neovim は HEAD を使っています。
- 作業はだいたい、ターミナル（wezterm） + ブラウザ（Vivaldi）だけで行っています。
- 1 プロジェクト 1 Neovim で作業してます。別プロジェクトを開くときは wezterm のタブを新しく作ってそこで Neovim を開きます。
- プロジェクト内の作業は基本的にその Neovim 内で完結させます。ビルド等は Neovim の terminal をタスクランナーとして使っています。
- Neovim のタブはほとんど使いません。
- ほぼすべての作業の起点はファジーファインダーです。
- バッファ移動はファジーファインダーかバッファーラインを使います。

## 私のプラグイン選びの基本方針

- Linux+Neovim で動くものを入れている
- 基本的に同じ機能のプラグインは 2 つ入れない
- 管理する言語を増やしたくないので同じ機能のものがあったら多少機能が劣化してても Lua 製のものを入れる
- カスタマイズ性やシンプル性よりも、リッチな見た目、機能のものを好む
- 外部依存やリモートプラグインはなるべく減らす方向だが機能が良ければ入れることもある
- 新しいモダンなプラグインを採用する
- 世界的にメジャーなものを採用する（日本製かどうかは重視していない）
- あまり過度にカスタマイズしすぎないようにしている（別プラグインに乗り換えるのが大変になるため）
- 使いそうなものはとりあえずインストールしておく（LazyLoad にしておけば実害はないので）

## プラグイン一覧

カテゴリごとに名前: コメントの順で列挙していきます。コメントは機能の説明というよりは私の感想です。

カテゴリの種類は以前書いたものにだいたい整合しているはずです。
https://qiita.com/yutkat/items/f19b2a0a962a587db5cf

### パッケージマネージャー

1. [wbthomason/packer.nvim](https://github.com/wbthomason/packer.nvim): Neovim で一番シェアが高いパッケージマネージャー。設定の関係性がやや複雑だが遅延読み込みもできて便利。

https://github.com/wbthomason/packer.nvim

### Library

2. [tpope/vim-repeat](https://github.com/tpope/vim-repeat): ドットリピート対応するときに必要なやつ。

https://github.com/tpope/vim-repeat

3. [nvim-lua/popup.nvim](https://github.com/nvim-lua/popup.nvim): Lua 用のライブラリ。結構なプラグインが依存してるから入れておく。

https://github.com/nvim-lua/popup.nvim

4. [nvim-lua/plenary.nvim](https://github.com/nvim-lua/plenary.nvim): Lua 用のライブラリ。結構なプラグインが依存してるから入れておく。

https://github.com/nvim-lua/plenary.nvim

5. [tami5/sqlite.lua](https://github.com/tami5/sqlite.lua): Lua 用のライブラリ。sqlite を便利に使えるようになる。

https://github.com/tami5/sqlite.lua

6. [MunifTanjim/nui.nvim](https://github.com/MunifTanjim/nui.nvim): Lua 用のライブラリ。たまに必要なプラグインがあるからとりあえず入れておく。

https://github.com/MunifTanjim/nui.nvim

7. [kyazdani42/nvim-web-devicons](https://github.com/kyazdani42/nvim-web-devicons): devicon が表示できるライブラリ。リッチな見た目にしたいから入れておく。

https://github.com/kyazdani42/nvim-web-devicons

8. [rcarriga/nvim-notify](https://github.com/rcarriga/nvim-notify): 通知をおしゃれなポップアップ形式で出せるようになる。

https://github.com/rcarriga/nvim-notify

### Colorscheme

9. [EdenEast/nightfox.nvim](https://github.com/EdenEast/nightfox.nvim): 最近使ってる人が多い nord 系テーマ。

https://github.com/EdenEast/nightfox.nvim

### LSP と自動補完

#### 自動補完系

10. [hrsh7th/nvim-cmp](https://github.com/hrsh7th/nvim-cmp): 自動補完プラグイン。いろいろカスタマイズできて動作も速くて見た目もかっこいい。神。

https://github.com/hrsh7th/nvim-cmp

11. [onsails/lspkind-nvim](https://github.com/onsails/lspkind-nvim): cmp で補完の種類におしゃれなアイコン出せるようになる。

https://github.com/onsails/lspkind-nvim

12. [hrsh7th/cmp-nvim-lsp](https://github.com/hrsh7th/cmp-nvim-lsp): lsp 用の補完ソース。

https://github.com/hrsh7th/cmp-nvim-lsp

13. [hrsh7th/cmp-nvim-lsp-signature-help](https://github.com/hrsh7th/cmp-nvim-lsp-signature-help): lsp 用の補完ソース。

https://github.com/hrsh7th/cmp-nvim-lsp-signature-help

14. [hrsh7th/cmp-nvim-lsp-document-symbol](https://github.com/hrsh7th/cmp-nvim-lsp-document-symbol): lsp 用の補完ソース。

https://github.com/hrsh7th/cmp-nvim-lsp-document-symbol

15. [hrsh7th/cmp-buffer](https://github.com/hrsh7th/cmp-buffer): バッファ補完用の補完ソース。

https://github.com/hrsh7th/cmp-buffer

16. [hrsh7th/cmp-path](https://github.com/hrsh7th/cmp-path): パス補完用の補完ソース。

https://github.com/hrsh7th/cmp-path

17. [hrsh7th/cmp-omni](https://github.com/hrsh7th/cmp-omni): オムニ補完用の補完ソース。正直あんまり使ってない。

https://github.com/hrsh7th/cmp-omni

18. [hrsh7th/cmp-nvim-lua](https://github.com/hrsh7th/cmp-nvim-lua): Lua 用の補完ソース。

https://github.com/hrsh7th/cmp-nvim-lua

19. [zbirenbaum/copilot-cmp](https://github.com/zbirenbaum/copilot-cmp): copilot 用の補完ソース。

https://github.com/zbirenbaum/copilot-cmp

20. [hrsh7th/cmp-emoji](https://github.com/hrsh7th/cmp-emoji): emoji 用の補完ソース。

https://github.com/hrsh7th/cmp-emoji

21. [hrsh7th/cmp-calc](https://github.com/hrsh7th/cmp-calc): 補完で簡単な計算してくれるようになるソース。

https://github.com/hrsh7th/cmp-calc

22. [f3fora/cmp-spell](https://github.com/f3fora/cmp-spell): Vim の spell 機能から補完してくれるようになるソース。

https://github.com/f3fora/cmp-spell

23. [yutkat/cmp-mocword](https://github.com/yutkat/cmp-mocword): mocword（次の英単語を予測してくれる）用の補完ソース。

https://github.com/yutkat/cmp-mocword

24. [uga-rosa/cmp-dictionary](https://github.com/uga-rosa/cmp-dictionary): 辞書補完してくれるためのソース。

https://github.com/uga-rosa/cmp-dictionary

25. [saadparwaiz1/cmp_luasnip](https://github.com/saadparwaiz1/cmp_luasnip): LuaSnip 用の補完ソース。

https://github.com/saadparwaiz1/cmp_luasnip

26. [tzachar/cmp-tabnine](https://github.com/tzachar/cmp-tabnine): TabNine 用の補完ソース。

https://github.com/tzachar/cmp-tabnine

27. [ray-x/cmp-treesitter](https://github.com/ray-x/cmp-treesitter): Treesitter 用の補完ソース。

https://github.com/ray-x/cmp-treesitter

28. [hrsh7th/cmp-cmdline](https://github.com/hrsh7th/cmp-cmdline): コマンドラインでも補完してくれるようになる。これで wilder.nvim を使わなくなった。

https://github.com/hrsh7th/cmp-cmdline

#### LSP 関連

29. [neovim/nvim-lspconfig](https://github.com/neovim/nvim-lspconfig): nvim-lsp 用の設定。Neovim のネイティブ lsp 使うなら必須。

https://github.com/neovim/nvim-lspconfig

30. [williamboman/nvim-lsp-installer](https://github.com/williamboman/nvim-lsp-installer): nvim-lsp じゃ LSP をインストールしてくれないので必須。

https://github.com/williamboman/nvim-lsp-installer

31. [tamago324/nlsp-settings.nvim](https://github.com/tamago324/nlsp-settings.nvim): プロジェクト固有の LSP の設定を定義できる。

https://github.com/tamago324/nlsp-settings.nvim

32. [weilbith/nvim-lsp-smag](https://github.com/weilbith/nvim-lsp-smag): LSP と tagfunc をつないでくれる。

https://github.com/weilbith/nvim-lsp-smag

#### LSP 用の UI

33. [tami5/lspsaga.nvim](https://github.com/tami5/lspsaga.nvim): LSP 関連の足りない UI だったりコマンドだったりを追加してくれる。他にも ray-x/navigator.lua とかもあるけどよく比較できていない。

https://github.com/tami5/lspsaga.nvim

34. [folke/lsp-colors.nvim](https://github.com/folke/lsp-colors.nvim): LSP 用の足りない色定義を追加してくれる。

https://github.com/folke/lsp-colors.nvim

35. [folke/trouble.nvim](https://github.com/folke/trouble.nvim): Diagnostics とか定義ジャンプとかを便利にしてくれる UI を提供してくれる。

https://github.com/folke/trouble.nvim

36. [EthanJWright/toolwindow.nvim](https://github.com/EthanJWright/toolwindow.nvim): trouble.nvim をさらに拡張してリッチにしてくれる。正直そんなに使ってない気がする・・・

https://github.com/EthanJWright/toolwindow.nvim

37. [j-hui/fidget.nvim](https://github.com/j-hui/fidget.nvim): むっちゃかっこいい感じで LSP の状態を表示してくれる。こういうおしゃれなの好き。

https://github.com/j-hui/fidget.nvim

#### AI 補完

38. [github/copilot.vim](https://github.com/github/copilot.vim): Neovim で Copilot する。

https://github.com/github/copilot.vim

39. [zbirenbaum/copilot.lua](https://github.com/zbirenbaum/copilot.lua): copilot.vim を Lua 移植したものだけどまだ copilot.vim が必要らしい。

https://github.com/zbirenbaum/copilot.lua

### ファジーファインダー

40. [nvim-telescope/telescope.nvim](https://github.com/nvim-telescope/telescope.nvim): たぶん Neovim で一番シェアが高いファジーファインダー。これがないと作業できないレベル。

https://github.com/nvim-telescope/telescope.nvim

41. [nvim-telescope/telescope-frecency.nvim](https://github.com/nvim-telescope/telescope-frecency.nvim): いい感じによく使うファイル順で表示してくれる FF ソース。一番使っている。

https://github.com/nvim-telescope/telescope-frecency.nvim

42. [nvim-telescope/telescope-packer.nvim](https://github.com/nvim-telescope/telescope-packer.nvim): 今 packer で入れてるプラグインを表示してくれる。

https://github.com/nvim-telescope/telescope-packer.nvim

43. [nvim-telescope/telescope-symbols.nvim](https://github.com/nvim-telescope/telescope-symbols.nvim): 絵文字とかのシンボルを FF 検索できる。nvim-cmp の補完でだいたい事足りるので利用頻度は低め。

https://github.com/nvim-telescope/telescope-symbols.nvim

44. [nvim-telescope/telescope-github.nvim](https://github.com/nvim-telescope/telescope-github.nvim): telescope から gh を使えるようになる（あまり使ってないけど）

https://github.com/nvim-telescope/telescope-github.nvim

45. [nvim-telescope/telescope-fzf-writer.nvim](https://github.com/nvim-telescope/telescope-fzf-writer.nvim): live_grep を速くしたやつ。使ってないけど一応入れてる。

https://github.com/nvim-telescope/telescope-fzf-writer.nvim

46. [nvim-telescope/telescope-smart-history.nvim](https://github.com/nvim-telescope/telescope-smart-history.nvim): コマンドヒストリーから FF で絞り込める。あまり使ってない。

https://github.com/nvim-telescope/telescope-smart-history.nvim

47. [nvim-telescope/telescope-media-files.nvim](https://github.com/nvim-telescope/telescope-media-files.nvim): 画像をプレビューしながら表示してくれる。正直まったく使ってないけど面白いから入れてる。

https://github.com/nvim-telescope/telescope-media-files.nvim

48. [LinArcX/telescope-command-palette.nvim](https://github.com/LinArcX/telescope-command-palette.nvim): コマンドよく忘れるかもだから一応入れてるけどそんなに忘れないことがわかった。（なおマッピングはよく忘れる）

https://github.com/LinArcX/telescope-command-palette.nvim

### Treesitter

49. [nvim-treesitter/nvim-treesitter](https://github.com/nvim-treesitter/nvim-treesitter): treesitter 本体。これがないと世界が色付き始めない。

https://github.com/nvim-treesitter/nvim-treesitter

50. [yioneko/nvim-yati](https://github.com/yioneko/nvim-yati): tresitter 本体の indent はバグっているのでこっちを使ったほうがいい。

https://github.com/yioneko/nvim-yati

51. [romgrk/nvim-treesitter-context](https://github.com/romgrk/nvim-treesitter-context): 画面に収まりきらない長い関数とかの関数名とかを上部に表示してくれる。レガシーなコードとか読むときに便利だったりするときもある。

https://github.com/romgrk/nvim-treesitter-context

52. [p00f/nvim-ts-rainbow](https://github.com/p00f/nvim-ts-rainbow): 対応する括弧の色を変えてくれる。ちょっと重いので行数でリミットかけるとよい。

https://github.com/p00f/nvim-ts-rainbow

53. [JoosepAlviste/nvim-ts-context-commentstring](https://github.com/JoosepAlviste/nvim-ts-context-commentstring): treesitter で解析して commentstring をいい感じに設定してくれる。svelte みたいに 1 ファイルに複数のコメントスタイルが混ざる時にとても便利。

https://github.com/JoosepAlviste/nvim-ts-context-commentstring

54. [haringsrob/nvim_context_vt](https://github.com/haringsrob/nvim_context_vt): 閉じ括弧部分に virtual text でどの括弧に対応するか教えてくれる。

https://github.com/haringsrob/nvim_context_vt

55. [nvim-treesitter/nvim-treesitter-refactor](https://github.com/nvim-treesitter/nvim-treesitter-refactor): treesitter を使ってリネームとかできる。普通は LSP の方を使うのでほぼ使うことがない。

https://github.com/nvim-treesitter/nvim-treesitter-refactor

56. [nvim-treesitter/nvim-tree-docs](https://github.com/nvim-treesitter/nvim-tree-docs): コードコメントを treesitter から生成してくれるらしい。使いこなせていない。

https://github.com/nvim-treesitter/nvim-tree-docs

57. [vigoux/architext.nvim](https://github.com/vigoux/architext.nvim): treesitter の構文から置換したりできるらしい。まったく使いこなせてない。

https://github.com/vigoux/architext.nvim

58. [m-demare/hlargs.nvim](https://github.com/m-demare/hlargs.nvim): 引数の変数だけ色を変えてくれる。

https://github.com/m-demare/hlargs.nvim

#### Treesitter textobj & operator

59. [nvim-treesitter/nvim-treesitter-textobjects](https://github.com/nvim-treesitter/nvim-treesitter-textobjects): treesitter で textobject できる。

https://github.com/nvim-treesitter/nvim-treesitter-textobjects

60. [RRethy/nvim-treesitter-textsubjects](https://github.com/RRethy/nvim-treesitter-textsubjects): textsubject として新しい textobject を定義する。

https://github.com/RRethy/nvim-treesitter-textsubjects

61. [mfussenegger/nvim-ts-hint-textobject](https://github.com/mfussenegger/nvim-ts-hint-textobject): easymotion みたいな感じで textobject を選択できる。どれにマップしてたかよく忘れる人には便利。

https://github.com/mfussenegger/nvim-ts-hint-textobject

62. [David-Kunz/treesitter-unit](https://github.com/David-Kunz/treesitter-unit): 今カーソルがある場所に紐づく領域を unit として textobject で扱える。雑にコピーしたいときとかに便利。これと nvim-ts-hint-textobject で sandwich 以外の textobject を使わなくなった。

https://github.com/David-Kunz/treesitter-unit

63. [mizlan/iswap.nvim](https://github.com/mizlan/iswap.nvim): treesitter 版の vim-swap。

https://github.com/mizlan/iswap.nvim

### 見た目関連

#### ステータスライン

64. [nvim-lualine/lualine.nvim](https://github.com/nvim-lualine/lualine.nvim): たぶんいちばんシェアが高いステータスライン。設定が短く済んで便利。

https://github.com/nvim-lualine/lualine.nvim

65. [SmiteshP/nvim-gps](https://github.com/SmiteshP/nvim-gps): ステータスライン上に今いる関数名を表示するプラグイン。treesitter を使ってる。

https://github.com/SmiteshP/nvim-gps

#### バッファーライン

66. [akinsho/bufferline.nvim](https://github.com/akinsho/bufferline.nvim): バッファーライン。作者が akinsho さんで安心できる。

https://github.com/akinsho/bufferline.nvim

#### ハイライト系

67. [RRethy/vim-illuminate](https://github.com/RRethy/vim-illuminate): カーソルが当たった単語を光らせる。なにげに LSP とかに対応してる。

https://github.com/RRethy/vim-illuminate

68. [norcalli/nvim-colorizer.lua](https://github.com/norcalli/nvim-colorizer.lua): 色コード部分に色を付けてくれる。

https://github.com/norcalli/nvim-colorizer.lua

69. [t9md/vim-quickhl](https://github.com/t9md/vim-quickhl): 今のカーソル下の単語に色を付けてくれる。コードリーディングするときにとても便利。Vim 時代からずっとお世話になっている。

https://github.com/t9md/vim-quickhl

70. [Pocco81/HighStr.nvim](https://github.com/Pocco81/HighStr.nvim): 指定箇所に好きな色を塗れる。全然使ってないがどこかで使いたい。

https://github.com/Pocco81/HighStr.nvim

71. [folke/todo-comments.nvim](https://github.com/folke/todo-comments.nvim): TODO などの文字を目立たせてくれる。

https://github.com/folke/todo-comments.nvim

72. [mvllow/modes.nvim](https://github.com/mvllow/modes.nvim): モードが行数の色でわかるようになる。正直あんまりモードがわからなくなることがないが、かっこいいから入れている。

https://github.com/mvllow/modes.nvim

#### レイアウト系

73. [myusuf3/numbers.vim](https://github.com/myusuf3/numbers.vim): InsertMode のときに相対行を絶対行に切り替えてくれる。

https://github.com/myusuf3/numbers.vim

#### サイドバー

74. [GustavoKatel/sidebar.nvim](https://github.com/GustavoKatel/sidebar.nvim): Git の状態とか Diagnostics とかファイル一覧とかが表示されてるサイドバーを表示する。

https://github.com/GustavoKatel/sidebar.nvim

#### メニュー

75. [sunjon/stylish.nvim](https://github.com/sunjon/stylish.nvim): むちゃくちゃかっこいいいろんな UI パーツが入っている。メニューもある。

https://github.com/sunjon/stylish.nvim

#### スタートアップ画面

76. [goolord/alpha-nvim](https://github.com/goolord/alpha-nvim): 起動時にファイル名の引数なしで起動した場合に表示するスタートアップ画面を設定できる。

https://github.com/goolord/alpha-nvim

#### スクロールバー

77. [petertriho/nvim-scrollbar](https://github.com/petertriho/nvim-scrollbar): スクロールバーを表示する。hlslens と組み合わせれば検索したワードがどこらへんにあるかもわかるようになる。革命

https://github.com/petertriho/nvim-scrollbar

#### カーソル

78. [edluffy/specs.nvim](https://github.com/edluffy/specs.nvim): カーソルが大きく移動したときにエフェクトを発生させる。かっこいい。ただそれだけ。入れてるけど基本無効にして飛び道具披露したいときにオンにする。

https://github.com/edluffy/specs.nvim

### 移動系

#### 選択移動

79. [phaazon/hop.nvim](https://github.com/phaazon/hop.nvim): Easymotion のようにラベルを指定してジャンプする。離れた特定の単語に飛ぶときによく使っている。高速に動作するところが ○

https://github.com/phaazon/hop.nvim

#### 縦方向移動

80. [unblevable/quick-scope](https://github.com/unblevable/quick-scope): 今いる行の f で一発（または二発）で飛べる単語をハイライトしてくれる

https://github.com/unblevable/quick-scope

81. [ggandor/lightspeed.nvim](https://github.com/ggandor/lightspeed.nvim): f 移動をカスタマイズしてくれる。私は clever-f の代替としてしか使っていないが、hop.nvim 的な機能もある。

https://github.com/ggandor/lightspeed.nvim

#### 縦方向移動

82. [haya14busa/vim-edgemotion](https://github.com/haya14busa/vim-edgemotion): 縦方向のいい感じの区切りの位置にジャンプ移動してくれる。

https://github.com/haya14busa/vim-edgemotion

83. [machakann/vim-columnmove](https://github.com/machakann/vim-columnmove): 縦方向で文字があるところまで移動してくれる。

https://github.com/machakann/vim-columnmove

#### 単語移動

84. [justinmk/vim-ipmotion](https://github.com/justinmk/vim-ipmotion): {}での移動をカスタマイズできる。

https://github.com/justinmk/vim-ipmotion

85. [bkad/CamelCaseMotion](https://github.com/bkad/CamelCaseMotion): w での移動などを Camel case 区切りで移動できるようになる。

https://github.com/bkad/CamelCaseMotion

86. [yutkat/wb-only-current-line.vim](https://github.com/yutkat/wb-only-current-line.vim): w や b の移動が行をまたがなくなる。

https://github.com/yutkat/wb-only-current-line.vim

#### 移動履歴ジャンプ

87. [osyo-manga/vim-milfeulle](https://github.com/osyo-manga/vim-milfeulle): jumplist と違い 1 バッファー内のみでの変更履歴にジャンプできる。

https://github.com/osyo-manga/vim-milfeulle

88. [Bakudankun/BackAndForward.vim](https://github.com/Bakudankun/BackAndForward.vim): 戻る進むの挙動をブラウザっぽくしてくれる。

https://github.com/Bakudankun/BackAndForward.vim

### 編集支援系

#### 選択

89. [terryma/vim-expand-region](https://github.com/terryma/vim-expand-region): 選択領域を徐々に広げることができる。treesitter でも一応同じことができる。

https://github.com/terryma/vim-expand-region

90. [terryma/vim-multiple-cursors](https://github.com/terryma/vim-multiple-cursors): マルチカーソル。あまり活用できていない。

https://github.com/terryma/vim-multiple-cursors

91. [kana/vim-niceblock](https://github.com/kana/vim-niceblock): ビジュアルモードでの動作を改善してくれる。

https://github.com/kana/vim-niceblock

#### 編集サポート

92. [junegunn/vim-easy-align](https://github.com/junegunn/vim-easy-align): 指定のスタイルにコードを整形できる。フォーマッターを使うのが普通になってきたのであまり使うことがなくなってきた。

https://github.com/junegunn/vim-easy-align

93. [thinca/vim-partedit](https://github.com/thinca/vim-partedit): 選択範囲を別のバッファーに切り出すことができる。

https://github.com/thinca/vim-partedit

94. [yutkat/delete-word-to-chars.vim](https://github.com/yutkat/delete-word-to-chars.vim): ctrl-w のときだけ単語区切り文字（iskeyword）を変更する。

https://github.com/yutkat/delete-word-to-chars.vim

#### Textobject

Treesitter のものを使っている

#### Operator

95. [mopp/vim-operator-convert-case](https://github.com/mopp/vim-operator-convert-case): camel case や snake case を簡単に切り替えられる。地味にすごく便利。

https://github.com/mopp/vim-operator-convert-case

96. [gbprod/substitute.nvim](https://github.com/gbprod/substitute.nvim): vim-operator-replace の Lua 版。

https://github.com/gbprod/substitute.nvim

97. [machakann/vim-sandwich](https://github.com/machakann/vim-sandwich): 括弧とかの部分をあれこれできる。個人的には textobj-sandwich の方が利用頻度高い。唯一神。

https://github.com/machakann/vim-sandwich

#### Join

98. [AckslD/nvim-revJ.lua](https://github.com/AckslD/nvim-revJ.lua): 行の方法分割を指定できる。

https://github.com/AckslD/nvim-revJ.lua

#### 値の加算・減算

99. [deris/vim-rengbang](https://github.com/deris/vim-rengbang): 連番生成が便利になる。

https://github.com/deris/vim-rengbang

100. [monaqa/dial.nvim](https://github.com/monaqa/dial.nvim): 数字や時刻などを加算、減算してくれる

https://github.com/monaqa/dial.nvim

#### ヤンク

101. [gbprod/yanky.nvim](https://github.com/gbprod/yanky.nvim): yankring みたいにヤンクした履歴を順番に貼り付けられる。

https://github.com/gbprod/yanky.nvim

102. [AckslD/nvim-neoclip.lua](https://github.com/AckslD/nvim-neoclip.lua): ヤンクした結果をファジーファインダーで探すことができる。

https://github.com/AckslD/nvim-neoclip.lua

103. [yutkat/save-clipboard-on-exit.vim](https://github.com/yutkat/save-clipboard-on-exit.vim): Linux だと Neovim を終了させたあとクリップボードがクリアされるので強制的にヤンクしたものを入れる。

https://github.com/yutkat/save-clipboard-on-exit.vim

#### ペースト

104. [yutkat/auto-paste-mode.vim](https://github.com/yutkat/auto-paste-mode.vim): 中央クリックでペーストした際に自動で paste mode になる。

https://github.com/yutkat/auto-paste-mode.vim

105. [tversteeg/registers.nvim](https://github.com/tversteeg/registers.nvim): レジスタに登録されてるものを floating window で一覧表示する。

https://github.com/tversteeg/registers.nvim

106. [AckslD/nvim-anywise-reg.lua](https://github.com/AckslD/nvim-anywise-reg.lua): treesitter を使って変な位置でペーストしてもいい感じの位置にペーストしてくれる。

https://github.com/AckslD/nvim-anywise-reg.lua

### 検索系

#### 検索

107. [kevinhwang91/nvim-hlslens](https://github.com/kevinhwang91/nvim-hlslens): 検索時に今のカーソルの隣に何個目のマッチしたものかを floating で表示してくれる。とても便利。

https://github.com/kevinhwang91/nvim-hlslens

108. [haya14busa/vim-asterisk](https://github.com/haya14busa/vim-asterisk): \*で今の単語を検索したときに動かなくしたりだとか、検索したときのカーソル位置を覚えてくれてたりとかする。必須。というか本体の挙動にして欲しいレベル。

https://github.com/haya14busa/vim-asterisk

#### 置換

109. [lambdalisue/reword.vim](https://github.com/lambdalisue/reword.vim): camel case とか snake case とか気にせずに一括置換できる。正直使ったことがないが、いつかのために入れてある。

https://github.com/lambdalisue/reword.vim

110. [haya14busa/vim-metarepeat](https://github.com/haya14busa/vim-metarepeat): cgn での置換が少し便利になる。

https://github.com/haya14busa/vim-metarepeat

#### Grep

111. [windwp/nvim-spectre](https://github.com/windwp/nvim-spectre): grep ツール。基本は telescope を使うが稀に正規表現したいときにこちらを使うこともある。

https://github.com/windwp/nvim-spectre

### ファイル操作系

#### ファイラー

112. [nvim-neo-tree/neo-tree.nvim](https://github.com/nvim-neo-tree/neo-tree.nvim): Lua 製の高機能ファイラー。開発が活発でよい。

https://github.com/nvim-neo-tree/neo-tree.nvim

#### バッファ操作

113. [wsdjeg/vim-fetch](https://github.com/wsdjeg/vim-fetch): `:e`とかで行数指定した形式でもファイルが開ける。

https://github.com/wsdjeg/vim-fetch

114. [famiu/bufdelete.nvim](https://github.com/famiu/bufdelete.nvim): バッファ削除でウィンドウが消えないようになる。

https://github.com/famiu/bufdelete.nvim

115. [stevearc/stickybuf.nvim](https://github.com/stevearc/stickybuf.nvim): 特定のファイルタイプのウィンドウでバッファが切り替わらなくなる

https://github.com/stevearc/stickybuf.nvim

#### ウィンドウ操作

116. [tkmpypy/chowcho.nvim](https://github.com/tkmpypy/chowcho.nvim): ウィンドウをラベルで選択できる（Easymotion みたいに）。あんまりウィンドウ開かない（多くても 4 つ）からそんない使ってはない。

https://github.com/tkmpypy/chowcho.nvim

117. [kwkarlwang/bufresize.nvim](https://github.com/kwkarlwang/bufresize.nvim): ウィンドウを閉じたときにいい感じにレイアウトを修正してくれる。

https://github.com/kwkarlwang/bufresize.nvim

### 標準機能拡張系

#### Undo

118. [simnalamburt/vim-mundo](https://github.com/simnalamburt/vim-mundo): undo 履歴をかっこよくグラフ的に表示してくれる。私はあまり使った記憶がないけど・・・

https://github.com/simnalamburt/vim-mundo

#### Diff

119. [AndrewRadev/linediff.vim](https://github.com/AndrewRadev/linediff.vim): 2 つの範囲選択した部分の差分を比較してくれる。重複コードとか調べるときとかも地味に便利。

https://github.com/AndrewRadev/linediff.vim

#### Mark

120. [chentau/marks.nvim](https://github.com/chentau/marks.nvim): mark があれば sign のエリアに表示してくれる。便利。

https://github.com/chentau/marks.nvim

#### Fold

121. [lambdalisue/readablefold.vim](https://github.com/lambdalisue/readablefold.vim): fold の表示をいい感じにしてくれる。fold は全く使わないけど一応入れている。

https://github.com/lambdalisue/readablefold.vim

#### Manual

122. [thinca/vim-ref](https://github.com/thinca/vim-ref): w3m などを使ってバッファー上にブラウザの結果をテキスト表示できる。英単語を調べたりするときはブラウザで調べるよりも速くて便利。

https://github.com/thinca/vim-ref

123. [folke/which-key.nvim](https://github.com/folke/which-key.nvim): よく忘れるマッピングを一覧をして表示できる。Leader とかプレフィックスとしてマップしてるキーに設定すると便利。

https://github.com/folke/which-key.nvim

#### Tag

124. [jsfaint/gen_tags.vim](https://github.com/jsfaint/gen_tags.vim): タグファイルを自動生成してくれる。LSP が出てきたおかげで利用頻度はかなり減った。

https://github.com/jsfaint/gen_tags.vim

#### Quickfix

125. [drmingdrmer/vim-toggle-quickfix](https://github.com/drmingdrmer/vim-toggle-quickfix): quickfix list と location list をトグルできるようになる。

https://github.com/drmingdrmer/vim-toggle-quickfix

126. [kevinhwang91/nvim-bqf](https://github.com/kevinhwang91/nvim-bqf): Quickfix が超絶使いやすくなる。特にプレビューはすごくいい。

https://github.com/kevinhwang91/nvim-bqf

127. [gabrielpoca/replacer.nvim](https://github.com/gabrielpoca/replacer.nvim): Quickfix 内で項目を編集できるようになって、それがバッファに反映されるようになる。

https://github.com/gabrielpoca/replacer.nvim

#### Session

128. [rmagatti/auto-session](https://github.com/rmagatti/auto-session): セッションを自動保存してくれる。これで終了してもすぐ同じ環境立ち上げられる。

https://github.com/rmagatti/auto-session

129. [rmagatti/session-lens](https://github.com/rmagatti/session-lens): セッション一覧を選択できる。私は 1 プロジェクト 1Neovim 派なので、セッションは起動時以外に切り替えることがないが一応入れておく。

https://github.com/rmagatti/session-lens

#### Macro

130. [zdcthomas/medit](https://github.com/zdcthomas/medit): マクロを簡単に編集できる。あまり使ってないがいざというときに必要な気もするので入れてある。

https://github.com/zdcthomas/medit

#### SpellCorrect

131. [Pocco81/AbbrevMan.nvim](https://github.com/Pocco81/AbbrevMan.nvim): 設定しておけばよくタイポする文字を自動修正してくれる。

https://github.com/Pocco81/AbbrevMan.nvim

#### Command

132. [tyru/capture.vim](https://github.com/tyru/capture.vim): コマンドの結果をバッファに書き込んでくれる。デバッグするときとかにとても便利。標準で入れて欲しいレベル。

https://github.com/tyru/capture.vim

133. [jghauser/mkdir.nvim](https://github.com/jghauser/mkdir.nvim): `:w` とかで新しくファイル作ろうとしたときにディレクトリがない場合は自動で作成してくれる。

https://github.com/jghauser/mkdir.nvim

134. [sQVe/sort.nvim](https://github.com/sQVe/sort.nvim): sort を拡張してくれる。

https://github.com/sQVe/sort.nvim

135. [yutkat/confirm-quit.nvim](https://github.com/yutkat/confirm-quit.nvim): 最後のウィンドウを閉じるときに確認ダイアログを出してくれる。

https://github.com/yutkat/confirm-quit.nvim

#### History

136. [yutkat/history-ignore.vim](https://github.com/yutkat/history-ignore.vim): 必要ないコマンドをコマンド履歴に登録しないようにする。

https://github.com/yutkat/history-ignore.vim

#### Terminal

137. [akinsho/toggleterm.nvim](https://github.com/akinsho/toggleterm.nvim): 標準のターミナルを使いやすくしたターミナル拡張。

https://github.com/akinsho/toggleterm.nvim

#### Backup

138. [aiya000/aho-bakaup.vim](https://github.com/aiya000/aho-bakaup.vim): バックアップを取ってくれる。あまりお世話になったことはないけど保険があることに越したことはない。

https://github.com/aiya000/aho-bakaup.vim

### 新規機能追加系

#### 翻訳

139. [voldikss/vim-translator](https://github.com/voldikss/vim-translator): Google 翻訳とかで翻訳できるようになる。

https://github.com/voldikss/vim-translator

#### スクリーンショット

140. [segeljakt/vim-silicon](https://github.com/segeljakt/vim-silicon): 選択した部分のコードを画像として出力することができる。

https://github.com/segeljakt/vim-silicon

#### コマンドパレット

141. [mrjones2014/legendary.nvim](https://github.com/mrjones2014/legendary.nvim): VS Code のコマンドパレットのようなものが使える。全然使ってないがいつか使いこなしたい。

https://github.com/mrjones2014/legendary.nvim

#### メモ

142. [renerocksai/telekasten.nvim](https://github.com/renerocksai/telekasten.nvim): zettelkasten スタイルのメモ管理ができる。外部コマンドに依存していないところがいい。

https://github.com/renerocksai/telekasten.nvim

#### バイナリエディタ

143. [Shougo/vinarise.vim](https://github.com/Shougo/vinarise.vim): Linux でまともなバイナリエディタがないので Linux アプリを含めてもこれしか選択肢がない。個人的には Vim プラグインという枠を飛び越えてる。新作の開発が着手されたという話なので期待したい。https://github.com/Shougo/ddx.vim

https://github.com/Shougo/vinarise.vim

#### ブラウザ連携

144. [tyru/open-browser.vim](https://github.com/tyru/open-browser.vim): ブラウザと連携することができる。

https://github.com/tyru/open-browser.vim

145. [tyru/open-browser-github.vim](https://github.com/tyru/open-browser-github.vim): さらに GitHub とも連携することができる。

https://github.com/tyru/open-browser-github.vim

#### テンプレートによる定型文生成

146. [mattn/vim-sonictemplate](https://github.com/mattn/vim-sonictemplate): Lua 製のものでも同じような機能のものがあるが、小回りが効かなかったのでこちらを使い続けている。

https://github.com/mattn/vim-sonictemplate

#### アクティビティ記録

147. [wakatime/vim-wakatime](https://github.com/wakatime/vim-wakatime): すべての自分の活動を記録したいデータ厨のために wakatime https://wakatime.com と連携できるようになる。ちなみに私は記録したいけど、特に見直さない派なのでたぶん設定したいだけ。

https://github.com/wakatime/vim-wakatime

### コーディング関連

#### ライティング支援

148. [zsugabubus/crazy8.nvim](https://github.com/zsugabubus/crazy8.nvim): `tabstop`, `shiftwidth`, `softtabstop`, `expandtab`をファイルから自動で設定してくれる。

https://github.com/zsugabubus/crazy8.nvim

149. [lfilho/cosco.vim](https://github.com/lfilho/cosco.vim): 行末のセミコロンを入力してくれるマッピングを提供してくれる。

https://github.com/lfilho/cosco.vim

#### リーディング支援

150. [lukas-reineke/indent-blankline.nvim](https://github.com/lukas-reineke/indent-blankline.nvim): インデントを見やすくしてくれる。

https://github.com/lukas-reineke/indent-blankline.nvim

151. [kristijanhusak/line-notes.nvim](https://github.com/kristijanhusak/line-notes.nvim): その行にメモを設置できる。

https://github.com/kristijanhusak/line-notes.nvim

#### コメント

152. [numToStr/Comment.nvim](https://github.com/numToStr/Comment.nvim): 機能が多いコメントアウトプラグイン。

https://github.com/numToStr/Comment.nvim

153. [s1n7ax/nvim-comment-frame](https://github.com/s1n7ax/nvim-comment-frame): ヘッダーコメントを作ってくれるプラグイン。けどいつも手打ちしちゃうのはなぜだろう・・・・？

https://github.com/s1n7ax/nvim-comment-frame

154. [LudoPinelli/comment-box.nvim](https://github.com/LudoPinelli/comment-box.nvim): かっこいい線でヘッダーコメントを作ってくれるプラグイン！

https://github.com/LudoPinelli/comment-box.nvim

155. [danymat/neogen](https://github.com/danymat/neogen): IDE みたいに関数ヘッダーにアノテーションを自動生成してくれる。Comment.nvim でもできるみたいだがどっちがいいのか評価中

https://github.com/danymat/neogen

#### 括弧

156. [andymass/vim-matchup](https://github.com/andymass/vim-matchup): treesitter にも対応している括弧をマッチさせるプラグインの決定版。

https://github.com/andymass/vim-matchup

157. [windwp/nvim-autopairs](https://github.com/windwp/nvim-autopairs): 括弧を自動で閉じてくれる。

https://github.com/windwp/nvim-autopairs

158. [windwp/nvim-ts-autotag](https://github.com/windwp/nvim-ts-autotag): HTML タグも自動で自動で閉じてくれる。

https://github.com/windwp/nvim-ts-autotag

#### コードジャンプ

159. [rgroli/other.nvim](https://github.com/rgroli/other.nvim): 条件に一致した複数のファイル間をジャンプできる。例えばコードとテストコード間のファイルを行き来するなど。

https://github.com/rgroli/other.nvim

#### テスト

160. [klen/nvim-test](https://github.com/klen/nvim-test): 複数の言語に対応しているテストランナー

https://github.com/klen/nvim-test

161. [michaelb/sniprun](https://github.com/michaelb/sniprun): コードの部分実行ができるランナー

https://github.com/michaelb/sniprun

#### タスクランナー

162. [yutkat/taskrun.nvim](https://github.com/yutkat/taskrun.nvim): シェルのコマンドを toggleterm で実行できるようにする。

https://github.com/yutkat/taskrun.nvim

#### Lint

163. [jose-elias-alvarez/null-ls.nvim](https://github.com/jose-elias-alvarez/null-ls.nvim): 機能が多い汎用 Language Server 。私は Linter, formatter としてしか使ってないが他にもいろいろできる。有名なのだと mattn/efm-langserver などがある。

https://github.com/jose-elias-alvarez/null-ls.nvim

#### Formatter

- フォーマッター自体は null-ls.nvim を使っている

164. [gpanders/editorconfig.nvim](https://github.com/gpanders/editorconfig.nvim): Editorconfig 用

https://github.com/gpanders/editorconfig.nvim

165. [ntpeters/vim-better-whitespace](https://github.com/ntpeters/vim-better-whitespace): 行末の空白スペースを削除してくれる。

https://github.com/ntpeters/vim-better-whitespace

#### コードアウトライン

166. [stevearc/aerial.nvim](https://github.com/stevearc/aerial.nvim): nvim-lsp を使ってコードアウトライン（そのファイルにあるクラスや関数の一覧）を作ってくれる。

https://github.com/stevearc/aerial.nvim

#### スニペット

167. [L3MON4D3/LuaSnip](https://github.com/L3MON4D3/LuaSnip): 設定が難しいがすごく高機能なスニペット。

https://github.com/L3MON4D3/LuaSnip

168. [kevinhwang91/nvim-hclipboard](https://github.com/kevinhwang91/nvim-hclipboard): スニペット使うと意図せずクリップボードが書き換わってしまうのを防いでくれる。

https://github.com/kevinhwang91/nvim-hclipboard

#### スニペット定義

169. [rafamadriz/friendly-snippets](https://github.com/rafamadriz/friendly-snippets): スニペット定義ファイル。

https://github.com/rafamadriz/friendly-snippets

#### プロジェクト

170. [ahmedkhalf/project.nvim](https://github.com/ahmedkhalf/project.nvim): プロジェクトを切り替えられる。私は 1 プロジェクト 1Neovim 派なのでプロジェクトルートの切り替えにしか使っていない。

https://github.com/ahmedkhalf/project.nvim

171. [klen/nvim-config-local](https://github.com/klen/nvim-config-local): プロジェクトローカルな設定ファイルを読み込むことができる。私は`.nvim`というディレクトリに格納するようにしている。

https://github.com/klen/nvim-config-local

#### Git

172. [TimUntersberger/neogit](https://github.com/TimUntersberger/neogit): 高機能 Git クライアント。

https://github.com/TimUntersberger/neogit

173. [sindrets/diffview.nvim](https://github.com/sindrets/diffview.nvim): neogit と連携するとかっこいい diff が表示できるようになる。

https://github.com/sindrets/diffview.nvim

174. [akinsho/git-conflict.nvim](https://github.com/akinsho/git-conflict.nvim): コンフリクトしたときの表示をわかりやすくする。

https://github.com/akinsho/git-conflict.nvim

175. [lewis6991/gitsigns.nvim](https://github.com/lewis6991/gitsigns.nvim): git の状態をかっこよく sign として表示する。

https://github.com/lewis6991/gitsigns.nvim

176. [yutkat/convert-git-url.vim](https://github.com/yutkat/convert-git-url.vim): git の URL 形式をgit@github.comとhttps://github.comとで相互に切り替える。

https://github.com/yutkat/convert-git-url.vim

#### Git コマンドからの連携

177. [rhysd/committia.vim](https://github.com/rhysd/committia.vim): シェルから`git commit`したときにかっこいい感じでコミット用にカスタマイズされた画面を起動してくれる。

https://github.com/rhysd/committia.vim

178. [hotwatermorning/auto-git-diff](https://github.com/hotwatermorning/auto-git-diff): シェルから `git rebase`したときにかっこいい感じでリベース用にカスタマイズされた画面を起動してくれる。

https://github.com/hotwatermorning/auto-git-diff

#### GitHub 連携

179. [pwntester/octo.nvim](https://github.com/pwntester/octo.nvim): gh コマンド的なことが Neovim 上でできるようになる。

https://github.com/pwntester/octo.nvim

#### デバッグ

180. [sentriz/vim-print-debug](https://github.com/sentriz/vim-print-debug): printf デバッグが捗る。

https://github.com/sentriz/vim-print-debug

#### デバッガー

181. [mfussenegger/nvim-dap](https://github.com/mfussenegger/nvim-dap): Neovim でも UI でデバッガーしたいってときに使う。思いの外ちゃんと動くが、DAP がちゃんと動いていることを確認できるまで多少がんばる必要がある。

https://github.com/mfussenegger/nvim-dap

182. [rcarriga/nvim-dap-ui](https://github.com/rcarriga/nvim-dap-ui): nvim-dap の UI をイケてる感じにしてくれる。

https://github.com/rcarriga/nvim-dap-ui

183. [theHamsta/nvim-dap-virtual-text](https://github.com/theHamsta/nvim-dap-virtual-text): DAP の結果を virtual text で表示してくれる。

https://github.com/theHamsta/nvim-dap-virtual-text

184. [nvim-telescope/telescope-dap.nvim](https://github.com/nvim-telescope/telescope-dap.nvim): DAP の telescope 連携。

https://github.com/nvim-telescope/telescope-dap.nvim

#### REPL

185. [hkupty/iron.nvim](https://github.com/hkupty/iron.nvim): Neovim 上で REPL することができる。REPL プラグインは実はたくさんあるが Lua 製だとこれがメジャーだと思われる。

https://github.com/hkupty/iron.nvim

### 言語固有プラグイン

treesitter や LSP 側に寄せているので言語固有のプラグインはそんなに必要ないが足りない部分を補ってくれるものは入れてある。

#### JavaScript

186. [vuki656/package-info.nvim](https://github.com/vuki656/package-info.nvim): package.json のパッケージが最新かどうかわかる。

https://github.com/vuki656/package-info.nvim

187. [bennypowers/nvim-regexplainer](https://github.com/bennypowers/nvim-regexplainer): ポップアップで正規表現を解説してくれる。

https://github.com/bennypowers/nvim-regexplainer

#### Rust

188. [simrat39/rust-tools.nvim](https://github.com/simrat39/rust-tools.nvim): Rust に特化したいくつかの機能が入っている。

https://github.com/simrat39/rust-tools.nvim

#### Markdown

189. [iamcco/markdown-preview.nvim](https://github.com/iamcco/markdown-preview.nvim): Markdown をブラウザ上でプレビューしてくれる。スクロールも追尾してくれる。

https://github.com/iamcco/markdown-preview.nvim

190. [SidOfc/mkdx](https://github.com/SidOfc/mkdx): markdown 用の便利な設定が詰まってる。正直あまり使いこなせておらずお節介なことも多いので結構なマッピングをオフにしてる。

https://github.com/SidOfc/mkdx

191. [dhruvasagar/vim-table-mode](https://github.com/dhruvasagar/vim-table-mode): テーブルを簡単に綺麗に作成できる。すごく便利。これがないとテーブル書けないレベル。

https://github.com/dhruvasagar/vim-table-mode

### SQL

192. [alcesleo/vim-uppercase-sql](https://github.com/alcesleo/vim-uppercase-sql): SQL を書いたら大文字にしてくれる。

https://github.com/alcesleo/vim-uppercase-sql

#### CSV

193. [chen244/csv-tools.lua](https://github.com/chen244/csv-tools.lua): CSV をカラムごとに色付けしてくれる。色付けする範囲も絞れるので重くなりにくい。

https://github.com/chen244/csv-tools.lua

#### Log

194. [MTDL9/vim-log-highlighting](https://github.com/MTDL9/vim-log-highlighting): 一般的なログファイルを色付けしてくれる。

https://github.com/MTDL9/vim-log-highlighting

#### Neovim Lua 開発用

195. [bfredl/nvim-luadev](https://github.com/bfredl/nvim-luadev): REPL のような感じで Neovim Lua を開発できる。一応入れている。

https://github.com/bfredl/nvim-luadev

196. [wadackel/nvim-syntax-info](https://github.com/wadackel/nvim-syntax-info): 今カーソルがある場所のシンタックス情報を virtual text で表示してくれる。

https://github.com/wadackel/nvim-syntax-info

## さいごに

ざっと紹介しましたが量が多くて、くぅ〜疲れました w （文章を書くというよりも連番振るのとリンク貼るの）

ちなみに 2022 年の春に使っていたものをまとめただけで今後更新するつもりはないので、**今** 私がなにを使っているか知りたい場合はこちらをご覧ください 🙇

https://github.com/yutkat/dotfiles/blob/master/.config/nvim/lua/rc/pluginlist.lua
