---
title: "Vimにたくさんあるファジーファインダー系プラグインを比較してみる"
emoji: "🔍"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["vim", "neovim", "vimplugin"]
published: true
---

## ファジーファインダー系プラグインとは

fuzzy finder、 あいまいに検索することができるツールです。
完全一致検索のように絞り込むまでにタイプ数が必要だったり、正規表現検索のように小難しいこともなく、高速に絞り込みできることがメリットです。

コマンドラインツールとして有名なのは[fzf](https://github.com/junegunn/fzf)で、ディレクトリを移動したり、ファイルを選択したり、パイプとしてつなげてフィルターしたりといった用途で使われています。

## Vimにおけるファジーファインダー系プラグイン

Vim,Neovimではファジーファインダー機能はデフォルトで入っておらず、なんらかのプラグインをインストールする必要があります。（機能としてはないですが、vimには[matchfuzzy](https://github.com/vim/vim/pull/6932)という関数は最近追加されました）
ファジーファインダーはプログラミングをするときにかなり強力なので、ほとんどのVimmerがなんらかのプラグインをインストール（もしくは自作）していると思います。

しかし、Vimのファジーファインダー系プラグインは数が多く、選ぶのがとても大変です。ファジーファインダーの戦国時代です。有力なものだけで10個もあります(2020年現在)。個人的には乗り換え対象があるのはすばらしいことだと思いますけど、せめて3-4個にしていただきたいものですね。。。

ちなみに、次に有力なプラグインの数が多いカテゴリーは、プラグインマネージャー系プラグイン、タスクランナー系プラグイン、ファイラー系プラグイン、LSPクライアントと続きます。ここらへんもそのうち比較記事を書きたいと思っています(たぶん)。

#### (おまけ)なぜこんなに増えたのか

理由の１つにvim scriptの手軽さと、なんでも自前で作りたくなるVimmerの特性があると思われます。
https://vim-jp.org/slacklog/CLKR04BEF/2020/06/#ts-1593137484.466200
https://vim-jp.org/slacklog/CLKR04BEF/2020/07/#ts-1594714880.427700

## Vimにおけるファジーファインダー系プラグインの利用用途

Vimでファジーファインダーを使うのは、主に次のような用途をファジーファインダーで効率的するためです。

- 開いているファイル(バッファー)の切り替える
- 今いるディレクトリ以下のファイルを検索する(find,git ls-files相当)
- 今いるリポジトリから特定のワードで検索する(grep,rg相当)
- 今いるファイル内から検索する
- MRU(以前開いたファイルを開く)
- コマンドを入力する
- 編集した場所や過去に移動した場所、ブックマークした場所へ移動する

### ファジーファインダーのデータソース詳細

この記事では、ファジーファインダーが検索する対象をデータソースと呼ぶことにします（ものによってはリソースや、データプロバイダーと呼ばれています）。
データソースにはだいたい網羅すると以下のようなものがあります。

#### 最低限提供されていることが多いデータソース

- buffers
- files
- git files
- grep
- lines

#### vim系の機能のデータソース

- tags
- marks
- command
- command history
- search history
- yank
- quickfix
- loclist
- windows
- sessions
- maps
- help
- colorscheme
- filetype

#### 他と差別化しやすいデータソース

- MRU
- LSP
- Treesitter
- git commit/diff
- change list
- jump list
- snippet

## ファジーファインダー系プラグインの比較

### 主要なファジーファインダー系プラグイン一覧

順番は2020/09/22時点でのGitHubのスター数になっています。

**※ 数が多すぎるため私もすべてのプラグインをインストールして試したわけではありません。READMEとソースが主な情報源です。**


| 名前                                                             | 動作環境                         | 実装言語                                                                                                  | Stars                                                                                      |
| ------------------------------------------------                 | ----------                       | ------------------------------                                                                            | -----                                                                                      |
| [fzf.vim](https://github.com/junegunn/fzf.vim)                   | Vim/Neovim                       | Vim script + 外部バイナリ(fzf[Go製])                                                                      | [![](https://img.shields.io/github/stars/junegunn/fzf.vim?label=%20&logo=%20)]()           |
| [ctrlp.vim](https://github.com/ctrlpvim/ctrlp.vim)               | Vim/Neovim                       | Vim script                                                                                                | [![](https://img.shields.io/github/stars/ctrlpvim/ctrlp.vim?label=%20&logo=%20)]()         |
| [denite.nvim](https://github.com/Shougo/denite.nvim)             | Vim(別途プラグインが必要)/Neovim | Python製リモートプラグイン                                                                                | [![](https://img.shields.io/github/stars/Shougo/denite.nvim?label=%20&logo=%20)]()         |
| [vim-clap](https://github.com/liuchengxu/vim-clap)               | Vim/Neovim                       | [低速版] Vim script or [高速版] Vim script + 外部バイナリ(maple[Rust製])                                  | [![](https://img.shields.io/github/stars/liuchengxu/vim-clap?label=%20&logo=%20)]()        |
| [LeaderF](https://github.com/Yggdroot/LeaderF)                   | Vim/Neovim                       | Vim script + Pythonコマンド実行(Cのバイナリもインストールされる？)                                        | [![](https://img.shields.io/github/stars/Yggdroot/LeaderF?label=%20&logo=%20)]()           |
| [fzf-preview.vim](https://github.com/yuki-ycino/fzf-preview.vim) | Neovim/Vim([neovim](https://www.npmjs.com/package/neovim)が必要)       | TypeScript製リモートプラグイン or CocExtension                                                            | [![](https://img.shields.io/github/stars/yuki-ycino/fzf-preview.vim?label=%20&logo=%20)]() |
| [telescope.nvim](https://github.com/nvim-lua/telescope.nvim)     | Neovim                           | Lua                                                                                                       | [![](https://img.shields.io/github/stars/nvim-lua/telescope.nvim?label=%20&logo=%20)]()    |
| [CocList](https://github.com/neoclide/coc-lists)                 | Vim/Neovimのcocユーザー          | coc.nvimに内包されている(coc.nvim自体はTypeScript製で自前リモートプラグインで動いている) | [![](https://img.shields.io/github/stars/neoclide/coc-lists?label=%20&logo=%20)]()         |
| [skim.vim](https://github.com/lotabout/skim.vim)                 | Vim/Neovim                       | Vim script + 外部バイナリ(skim[Rust製])                                                                   | [![](https://img.shields.io/github/stars/lotabout/skim.vim?label=%20&logo=%20)]()          |
| [vim-fz](https://github.com/mattn/vim-fz)                        | Vim/Neovim                       | Vim script + 外部バイナリ(gof[Go製])                                                                      | [![](https://img.shields.io/github/stars/mattn/vim-fz?label=%20&logo=%20)]()               |

### 主要なファジーファインダー系プラグイン詳細

この章で各ファジーファインダーの詳細な特徴と所感を書いていきます。

**※ デフォルトの機能寄りの記載になっています。(例:xxxを使えば実はカスタマイズできてみたいなのを考慮していないということです)**
**※ なるべく公正になるように画像は公式のREADMEやIssue,PullRequestのものを使っております。**

#### 1. [fzf.vim](https://github.com/junegunn/fzf.vim) 

[![](https://user-images.githubusercontent.com/234774/81399159-2f3b5a80-9133-11ea-8e3c-4e0dd41dd8b5.png =600x)]()

作者は[fzf本体](https://github.com/junegunn/fzf)の作者でもあって、[vim-plug](https://github.com/junegunn/vim-plug)の作者としても有名。
私の観測範囲ではたぶんNo1シェアだと思われる。特に海外では人気が高い。fzf自体の動作が速いため高速に候補の絞り込みができ、最低限必要なデータソースをデフォルトで提供している。
floating windowにも対応しているので見た目もかなりおしゃれにできる。最近プレビュー機能もデフォルトで対応となったので、目的のファイルをさらに探しやすくなった。
拡張性も高く [https://github.com/junegunn/fzf/wiki/Examples-(vim)](https://github.com/junegunn/fzf/wiki/Examples-(vim))にやり方がいろいろ書いてある。

デメリットとしては、MRUやLSP向けのデータソースをデフォルトでは提供していないことと、イケてる感じで使おうとするとそこそこな規模のコードを自分のvimrcに書く必要が発生することなどである。

余談としては、fzf本体側になぜかVim plugin用のscriptがあり、fzf.vimはそれをwrapしてデータソースを提供している奇妙な作りをしている。おかげでIssueを検索するときfzf本体の方のバグが引っかかったりするので、とてもめんどくさい。


#### 2. [ctrlp.vim](https://github.com/ctrlpvim/ctrlp.vim)

[![](https://camo.githubusercontent.com/e15ac916ab9a14dd07135cb2d985cc7333200a38/687474703a2f2f692e696d6775722e636f6d2f614f63774877742e706e67 =600x)]()

Vimの中では老舗のファジーファインダー(2011年製)。Vimの結構古いバージョン(7系以上)でも動くようになっている。
MRUのデータソースもデフォルトで用意されている。他にあまりない変わった機能としては、Vimの正規表現も使える点、ファイルやディレクトリを作成することができる点などがある。
拡張性を利用して[https://github.com/ctrlpvim/ctrlp.vim/tree/extensions](https://github.com/ctrlpvim/ctrlp.vim/tree/extensions)関連するプラグインもいくつか作られている。

デメリットとしては、Vim script製なのでデータソースのデータが多いと絞り込みが遅くなる点が挙げられる。あと、popupとかfloating windowは使わない無骨なUIをどう受け取るか。


#### 3. [denite.nvim](https://github.com/Shougo/denite.nvim)

[![](https://user-images.githubusercontent.com/13142418/65154937-f002b100-da5e-11e9-8aef-723233e3704d.jpg =600x)]()


作者はDarkPoweredプラグインを数多く世に送り出してる暗黒美無王こと日本人のShougoさん。[Unite.vim](https://github.com/Shougo/unite.vim) を経て爆誕した。
Vim scriptでなくリモートプラグイン(Python)を使用しているためデータソースが多くても高速に動作する（Go,Rust等のバイナリを実行するものよりはさすがに遅い）。
拡張性が高く、データソースを様々な開発者が作るエコシステムができている。[https://github.com/Shougo/denite.nvim/wiki/External-Sources](https://github.com/Shougo/denite.nvim/wiki/External-Sources)

デメリットはVim初心者には複雑に感じて設定が難しいこと。

#### 4. [vim-clap](https://github.com/liuchengxu/vim-clap)

[![](https://user-images.githubusercontent.com/8850248/74818883-6cfdc380-533a-11ea-81fb-d09d90498c96.png =600x)]()

作者は[vista.vim](https://github.com/liuchengxu/vista.vim)や[vim-which-key](https://github.com/liuchengxu/vim-which-key)を作成している。
プレビュー機能がついていて、外部バイナリを使うと高速に絞り込みできる。他のプラグインと違いめずらしくVim scriptだけでも動作可能の模様。拡張性も高いので[https://github.com/topics/vim-clap](https://github.com/topics/vim-clap)に他の方が作ったデータソースが公開されている(なぜか日本人が多い)。

これといったデメリットはないように感じるが、取り立てて他のプラグインに対して優位なところもない印象。あと個人的には、CLI側でfzf等を使っていた場合、２つのファジーファインダーのプログラムがOS内にインストールされるところに少し違和感を感じる。

#### 5. [LeaderF](https://github.com/Yggdroot/LeaderF)

[![](https://github.com/Yggdroot/Images/raw/master/leaderf/leaderf_popup.gif =600x)]()

ctrlp.vimの次に古参のファジーファインダー。こちらも対応vim7.3以上で動くということで、ほぼ最新を必要とする他のファジーファインダーと比べて動作要件が緩い。絞り込みに正規表現も使えるしプレビューにも対応している。
ctrlp.vimとvim-clapの間のような印象。

#### 6. [fzf-preview.vim](https://github.com/yuki-ycino/fzf-preview.vim)

[![](https://user-images.githubusercontent.com/5423775/88540152-6e4fbc80-d04d-11ea-8d19-314ee5e4d294.gif =600x)]()

色付きプレビュー、ファイル名の色が付け、Deviconの表示、バッファの削除、Quickfixへのデータ受け渡しなど、機能盛りだくさんの見た目派手なオールインワンファジーファインダー。データソースもデフォルトで豊富にあって、なぜかgitの操作もプレビュー付きでできる。ファジーファインダー自体はfzfなので動作も高速。fzf.vimの足りないデータソースを追加して、設定の手間を削減して、いい感じにレイアウトしてくれるイメージ。
作者は日本人のycinoさん。よくvim-jp slackにいる。[vim-jp slackはこちら](https://vim-jp.org/docs/chat.html)

デメリットとしては高機能故に依存しているプラグインやプログラムが多いことが挙げられる。余計なものをいれたくないミニマリスト向けではない。あと、データソースとしてfzf.vimの機能に近いもの(コマンド検索やヘルプ検索等)に提供されてものもある。ここらへんのデータソースも使いたければfzf.vimやCocListを別途併用する必要がある。

ちなみに私はこれのcoc版を使っている（cocユーザーなので）。coc版はLSPの一部をデータソースとして使用できる（もちろんプレビュー付き）。

#### 7. [telescope.nvim](https://github.com/nvim-lua/telescope.nvim)

[![](https://raw.githubusercontent.com/tjdevries/media.repo/master/telescope.nvim/simple_rg_v1.gif =600x)]()

Neovimのコントリビューターで人気者の[TJ](https://github.com/tjdevries)さんがfzf-preview.vimにインスパイアされて作ったLua製のファジーファインダー。
Neovimでしか使えないが、Luaの高速な動作とリッチな機能が売り。fzf-preview.vimに影響を受けているだけあって、色付きプレビュー, Deviconなど機能盛りだくさん。
fzf-previewと差別化できる点としては、treesitterやNeovimLSPと連携できる点が挙げられる。Neovimコントリビューターが作っているだけあって本体と密接につながっていけるのは今後の成長を含めて強みだと考えられる。

デメリットは、MRUのデータソースがない(`:oldfiles`には対応しているので簡単なMRUとしては使える模様)などデフォルトで提供されているデータソースが少ないこと。また、拡張するにはLuaの知識が必要。

#### 8. [CocList](https://github.com/neoclide/coc-lists)

[![](https://pic2.zhimg.com/v2-1c31b5f8e7d89ed1b0ef1555b6559d13_b.webp =600x)]()

cocユーザーならデフォルトで使用できるファジーファインダー。デフォルトではデータソースが足りないので[https://github.com/neoclide/coc-lists](https://github.com/neoclide/coc-lists)を追加でインストールしたほうがよい。これでバッファ切り替えやファイル検索などの基本的になデータソースはひと通り揃う。coc-list自体がLSPの機能提供の一部となっているのでLSP由来のデータソースも検索できる。

デメリットとしては、作者があまり機能追加に乗り気ではないため、今度改善されていく可能性は少ない見込み。

この欠点を解決するためにcoc-listの機能をwrapして別のファジーファインダーにした 
- [coc-fzf](https://github.com/antoinemadec/coc-fzf)
- [coc-clap](https://github.com/vn-ki/coc-clap)
- [coc-denite](https://github.com/neoclide/coc-denite)
などの拡張機能もある。

#### 9. [skim.vim](https://github.com/lotabout/skim.vim)

skimというRust製のファジーファインダーをバックエンドとして使っている。CLIのファジーファインダーツールも含めてRust製にしたい人には選択肢に入るかもしれない。fzf.vimをcloneして作っているようなのでできることはよくも悪くもfzf.vimと同じかそれ以下になると思われる。


#### 10. [vim-fz](https://github.com/mattn/vim-fz)

[![](https://raw.githubusercontent.com/mattn/vim-fz/master/screenshot.gif =600x)]()

シンプルな作りになっているので理解しやすい。なんでも自分の手中に納めないと気がすまない人向け。

Windowsだと実行モジュールの起動に少し時間がかかるのが気になるとのこと（mattnさん[本人談](https://vim-jp.org/slacklog/CLKR04BEF/2020/09/#ts-1600057526.248200)）。Windowsでの実行モジュールの起動の遅さは、外部バイナリを呼び出す形式のものにはすべて当てはまるのでgof(vim-fzのバックエンド)がとりわけ起動が遅いというわけではない。


### プラグインを使わないやり方

一応プラグインを使わずにファジーファインダーを使う方法もあります。
例えば、`:terminal`でfzfを使う方法やtmuxのpaneを使ってファジーファインダーを起動してVim側に受け渡す方法などが挙げられます。


## ファジーファインダー系プラグインの選び方

ファジーファインダー選びはVimプラグインの選択の中でもかなり難しい選択になるかとは思いますが（機能が多くて把握するのが難しく、誤った選択をしたあとの乗り換えのコストが高いため）、一応判断する上で役に立ちそうな指針を書いておきます。

まずは自分のVimのスタイルと各種要件（Vimで使うかNeovimで使うか、リモートプラグインを許容するか等々）から絞るのがよいと思います。
主要なファジーファインダー系プラグイン一覧を利用して絞ってみてください。

そして、機能からさらに絞り込みます。
機能を軸にしたときの主な差別化要素は、
- 自分のよく使うデータソースが入っているか
- 速度(絞り込み、起動含む)
- プレビュー機能（選択されているファイルの内容を右側等に表示する機能）
- LSP連携
 
となると思います。
ファジーファインダーを使うことに慣れてくれば、5分に一回は確実に起動することになるかと思いますので、速度や体験は非常に大事になってきます。


検索を効率的に絞り込むファジーファインダーを絞り込むのにこんなに手間がかかるのは正直本末転倒な気もしますが、それもまたVimです。
ファジーファインダーを使いこなしてよいVimライフを送り、さらに生産性を高められることを願っています...

