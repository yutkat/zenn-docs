---
title: "超融合!時空を越えた絆 Neo Vim(VSCode)を試してみた"
emoji: "🌪"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["neovim", "vscode", "vim"]
published: true
---

## 2020年のエディタ・IDE界

2020年のエディタ・IDE界は、Vim vs Emacsとか言われていた時代も過去になり、昨今はVSCode１強になりつつあります[^1]。VSCodeはデフォルトの機能も必要十分ありますし、拡張機能のエコシステムが発達してますし、リリースサイクルも早くてすばらしいの一言ですね（あとやっぱりMSがバックにいるのが何気に強い）。2015年にリリースされてからまさに飛ぶ鳥を落とす勢いです。

他に有料だと[JetBrains](https://www.jetbrains.com/)のIDEとかはやっぱり出来がいいですね。あとVSCodeの拡張がそのまま使える[Eclipse Che](https://www.eclipse.org/che/)なんかも新興勢力として期待しています。

[^1]: 2020年のStackoverflowアンケートからエディタが抹消されていたので[2019年度分](https://insights.stackoverflow.com/survey/2019#technology-_-most-popular-development-environments)を参考

## 私について

世の中はいろいろ動いてますが、私はVimをかれこれ15年以上使ってます。2016年くらいにVimからNeovimに乗り換えましたが、今でもほぼ毎日使っています。
> 特に世界平均と比較した際に、Vimを愛する人の割合の多さが突出しています[^2]
 
との情報にもあるように日本は[vimコミュニティ](https://vim-jp.org/)の技術力が高く、また居心地もいいのでなかなか脱出できません。
[^2]: https://blog.jetbrains.com/ja/2020/10/24/deveco20worldvsjp/

何度かJetBrainsIDEやVSCodeを使ってみたり（調査しているだけで浮気ではない）したこともあるんですが、やはりVimに蓄積している資産(vimrc)には勝てず、新しいエディタを頑張って設定するのもストレスが溜まるため毎回出戻りしています。（それでもJavaを書くときなどはIntellijを使ったりします）
Vimは起動が速くていいですね（けれども最近は他も結構速い[^3]）。思ったとおりに動いてくれる。それに戻って来たときの我が家に帰ってきたような感覚は何事にも代えがたいです。

[^3]: ちなみに私の環境で起動時間を計測すると、設定頑張ったNeovim: 0.4秒、VSCode: 2秒、JetBrainsIDEのCLion: 8秒という感じでした。

### 私の開発環境

[![yutkat/dotfiles](https://github-link-card.s3.ap-northeast-1.amazonaws.com/yutkat/dotfiles.png =250x)](https://github.com/yutkat/dotfiles)

- ちょっとだけ設定がんばってる(Neo)Vimmer
- OSはArchLinux
- NeovimはCLI派。ターミナル(alacritty)上でさらにtmux上で使用している。
- vimrcの戦闘力は[スカウター](https://github.com/thinca/vim-scouter)で計測すると2792 (ナッパ戦の悟飯くらい)
- インストールしているVimプラグインの数は190以上 **(たくさん入れれば強いというものではないので注意!)**

## Neo Vim(VSCode)爆誕

Vimはカスタマイズがしやすくて使いこなせばすごい力になるよ！っていくら言っても、時代に逆らえるものではありません。LSP(Language Server Protocol)を使えば補完周りはだいぶIDEっぽくなってコーディングしやすくなりますが、VSCodeにはあってVimではうまく実現できてないところがいくつかあります。

そのVimで実現が難しいVSCodeの強みとは

- LiveShare
- Remote Develop
- .vscodeディレクトリによる開発の効率化
- デバッガー(DAP(vimspector等)を使えばVimでもきますが機能は少ないです)
- 画像等も扱えるプラグインの多様性
- マーケットプレイスによる簡単なプラグイン選択（拡張機能の星とダウンロード数)
などになります。

その一方Vim,Neovimの強みは

- カスタマイズの容易性
- 今まで大切に育ててきたvimrc資産
- マウス操作不要
- CLIツールとの連携のしやすさ
などだと思います。

VSCode上で[VSCodeVim](https://vim-jp.org/)を使うのもありかな。けど前に試したときは、使い勝手が・・・vimrcにある資産活用してくれるわけでもないし・・・(一応まだ実験的にですがvimrcの読み込みもサポートしています https://github.com/VSCodeVim/Vim)

『これからどうすればいいんだ・・・一体どっちを選べばいいんだ・・・未来が見えない。。。』
ってのが2020年のVimmerの悩みでもあるかと思います。

そんな人のために、VSCodeとVimを合体させることを提案します。
「またまた〜、どうせVSCodeVimみたいなVimエミュレーターでしょ？だいたいああいう系は私の求めてるVimじゃないんですよね〜」って人多いんじゃないでしょうか？？
違います。真に合体させます。
**1991年生まれのVimと、2015年生まれのVSCodeの、時空を超えた超融合です！！**

そう、

![1200px-Visual_Studio_Code_1 35_icon svg](https://user-images.githubusercontent.com/8683947/102637796-e86a1480-4199-11eb-82ad-3a83a2ee6981.png =160x)
*と*
![hg6qhdveqziyh3zlcpev](https://user-images.githubusercontent.com/8683947/102637798-e902ab00-4199-11eb-9d76-8e8dff0ef5ae.png =160x)
*を*
![cardgame_card_dasu](https://user-images.githubusercontent.com/8683947/102639247-19e3df80-419c-11eb-8f18-55f0bece8443.png =160x)
*ドン☆*
![fusion01](https://user-images.githubusercontent.com/8683947/102639214-0b95c380-419c-11eb-8bb2-daca55938218.png =160x)
*融合発動！！*

![Microsoft VisualStudio Services Icons](https://user-images.githubusercontent.com/8683947/102680961-a9bb7500-4200-11eb-9a31-eed9e2c9a01f.png)
*出でよ、Neo Vim(VS Code Neovim)！!*

***融合することで誕生する最強のエディターそれがNeo Vim(VS Code Neovim)だ！！！！！***

(名前が若干イケてない感があるのはご愛嬌・・・)

## Neo Vim(VS Code Neovim)の概要

名前は"Neo Vim"みたいです。本記事では紛らわしいのでNeo Vim(VS Code Neovim)に統一します。リポジトリ名はvscode-neovimです。Neovimとneovimとnvimは本物のNeovimになります。これから紹介するのはNeo Vimの方です。ちなみにNeoVimは今のところこの世にはありません。

リポジトリは↓↓↓になります。
https://github.com/asvetliakov/vscode-neovim/tree/3f45ff2a16ac76682d249ee48b55a8e42acbd957/vim

マーケットのページは↓↓↓です。
https://marketplace.visualstudio.com/items?itemName=asvetliakov.vscode-neovim

仕組みとしては、Neovimのインスタンスをバックエンドとして立ち上げてそれと通信することで、本物のNeovimとして動作させることに成功しています。
結局VSCodeVimやらのVimエミュレーションがなぜ挫折するかというと、使い勝手（特にマウス操作が増えたり）がかなり変わったり、乗り換えようとしているときにコソッと使ってる自分のvimrcと設定が乖離してくるからだったりするからです。
しかしこのNeo Vim (VS Code Neovim)は違います。なんと自分のvimrc(init.vim)を読み込んでくれるのです！しかもほとんどの設定がそのまま使えるらしいのです。なんたって後ろで本物のNeovimが動いてますからね！画期的。正直言って少し気持ち悪さすらあります。

## Neo Vim(VS Code Neovim)のインストール

インストールは最新のNeovimをインストールして、Neo Vim(VS Code Neovim)の拡張をインストールするだけです。とても簡単。
:::message
私の環境では `vscode-neovim.neovimExecutablePaths.linux` にnvimへのパスを記述しないとうまく動かなかったです。
:::

## Neo Vim(VS Code Neovim)を使ってみた

### さくっと起動して触る

インストールは簡単に終わったので使ってみることにします。

さらっとREADMEを読んでみると
> Important!: If you already have big & custom init.vim i'd recommend to wrap existing settings & plugins with if !exists('g:vscode') check to prevent potential breakings and problems. If you have any problems - try with empty init.vim first
 
とか書かれてますが、とりあえずそのままvimrcを読み込んでみます。その方が楽しそうじゃないですかw

有効にしてみると、

『なん..だと...戦闘力2792の俺のvimrcがエラーもなく動くだと・・・？！』

『ふん、どうせ読み飛ばしてるだけで誤魔化してるに過ぎん。ん？なんだこのアンダーラインと色がついてるところは・・・？』

![2020-12-19_18-06](https://user-images.githubusercontent.com/8683947/102685552-eac58080-4224-11eb-9a3a-ff06c290d546.png =600x)

『お前は・・・まさか・・・！[quick-scope](https://github.com/unblevable/quick-scope)！！？quick-scopeじゃないか・・・！』

![2020-12-19_18-08](https://user-images.githubusercontent.com/8683947/102685596-4132bf00-4225-11eb-9224-69e73deb218c.png =600x)
*Neovimの画面*

『自分のvimrcの設定だけでなく、Vimプラグインも動作しているのか！！！』

[clever-f](https://github.com/rhysd/clever-f.vim)なんかも普通に動きます。
![Peek 2020-12-19 18-13](https://user-images.githubusercontent.com/8683947/102685721-fa919480-4225-11eb-9cf6-ecac408a07ff.gif)
*clever-fの動作シーン*

*Vimプラグイン作者の人たちは驚くかも知れませんが、実はあなたのプラグインがもうすでにVSCode上で動いているかも知れませんよ・・・*

あと[vim-altercmd](https://github.com/kana/vim-altercmd)が内包されてる。kanaさんすごい。

### 細かく設定をチューニングしていく

ちなみに先に紹介しておくと、禁じ手がいくつかあるようなのでハマったら確認するとよいかもです。https://github.com/asvetliakov/vscode-neovim#important

#### vimrcを編集するための準備

vimrcをVSCodeでいじっていきます。そういえばvimrcをVim以外でいじったことはないので、なかなか違和感満載です。

デフォルトだと色がつかないので、vim scriptにシンタックスカラーを適用する拡張機能をインストールします。 https://marketplace.visualstudio.com/items?itemName=XadillaX.viml

あと、vimrcをいじったあと設定を読み込み直すショートカットをVSCode側で追加してあげると作業が捗ります。
私は、modifyOtherKeysがないと使えない系のマップ(<C-S->, <C-=>とか)は、Vimではマッピングしてないので、そこにVSCode特有の便利ショートカット用にしました。

```json
    {
        "key": "ctrl+shift+r",
        "command": "workbench.action.reloadWindow",
        "when": ""
    },
```

再起動したあと一瞬インサートモードになってしまう（Neo Vimが起動してない隙きが生まれる）ので注意が必要です。

ちなみに、Vimmerでも最低限覚えておいたほうがいいVSCodeショートカットはこれです。

|キー|説明|
|---|---|
|C-S-p|コマンドパレットを起動します。ここでコマンドを打ち込めば大抵のことはマウスを使わずにできます。|

#### 動かないmapやプラグインを分岐していく

ちょこちょこと試して見ましたがプラグインもそのまま動くものが多いです（floating windowを使っているものなどは置き換えが必要）。NeovimなのでLua製プラグインも動きました。

vimrcで動かないmapや壊れてるプラグインをif文でかわしていきます。NeovimとVimでvimrcを共用している人は

```vim
if has('nvim')
```

なイメージで

```vim
if !exists('g:vscode')
```

で分岐してあげればいいです。

:::message
ちなみに、動かないmapを動かした場合エラーが出たり、VSCodeが落ちたりすることはないですが、ちょっと数秒固まるような動作になります
:::

#### mapをカスタマイズする

##### map設定の原理

Neo Vim(VS Code Neovim)はmapのキーコードを直接拾っているわけではないく、VSCodeのショートカット設定から引き渡されて処理しています。
そのデフォルト設定がここにあります。 [package.jsonのkeybindings](https://github.com/asvetliakov/vscode-neovim/blob/6addadfe7d3d988266a2ff6ce26d9a1980500020/package.json#L367-L1075)

[Normal mode control keys](https://github.com/asvetliakov/vscode-neovim/blob/bdde8a200944b68e262491492c7a56191fce5978/README.md#normal-mode-control-keys)に書かれているキー以外を追加したい場合、

たとえば`<C-g>`に

```vim
nnoremap <silent> <C-g> <Cmd>call VSCodeNotify('workbench.action.nextEditor')<CR>
```

を追加したい場合があるとすると

```json:keybindings.json
{
  "command": "vscode-neovim.send",
  "key": "ctrl+g",
  "when": "editorTextFocus && neovim.init && neovim.mode != insert && neovim.ctrlKeysNormal",
  "args": "<C-g>"
},
```

を設定して、Neo Vim(VS Code Neovim)に伝えてあげる必要があります [詳しくはここ](https://github.com/asvetliakov/vscode-neovim/blob/bdde8a200944b68e262491492c7a56191fce5978/README.md#normal-mode-control-keys)。ちなみにwhen節でneovimの状態も制御できます。https://code.visualstudio.com/docs/getstarted/keybindings

##### map設定のやり方

keybindings.jsonとGUI両方開きながら編集したほうがやりやすかったです。
デフォルトのキーマップはここでVimスクリプトの形で定義されています。[https://github.com/asvetliakov/vscode-neovim/tree/master/vim](https://github.com/asvetliakov/vscode-neovim/tree/master/vim)

VSCodeの機能をVimスクリプト側でマップしたい場合は以下のようにやるとよいと思います。

```vim
<Cmd>Call VSCodeNotify('workbech.xxx')<CR>
```

VSCodeのデフォルトで提供されている機能の代表的なものはここにまとまってました。 https://vscode.readthedocs.io/en/latest/getstarted/keybindings/

必要なcommand名称（ID）はここからコピーできます。
![2020-12-13_20-30](https://user-images.githubusercontent.com/8683947/102010553-0e4e7e00-3d82-11eb-9b0b-09fab4e98019.png)

ただ正直、VSCodeのショートカットで設定しても同じなのでそちらでやってもよいでしょう。（そっちでやったほうがショートカットがNeo Vim(VS Code Neovim)まで伝わっていていないとか無駄なハマりはなくなる気もします）

#### 動かないプラグインを乗り換える

私は普段Neovimで開発しているときは
[fzf-preview.vim](https://github.com/yuki-ycino/fzf-preview.vim)
を多用して、バッファの移動やファイルの検索等を行っているのですが、floating windowを使っているためNeo Vim(VS Code Neovim)上では動きません。代替品を探す必要があります。
VSCodeのQuick Openを使って代用することにします。

```vim
nnoremap <silent> <Leader>p <Cmd>call VSCodeNotify('workbench.action.quickOpen')<CR>
```

![2020-12-19_20-37](https://user-images.githubusercontent.com/8683947/102688440-038c6100-423a-11eb-8a29-7619ad7cea9f.png =600x)

やってみましたが、クッ！プレビューが見えないのが痛い・・・
![2020-12-19_20-31](https://user-images.githubusercontent.com/8683947/102688285-2a966300-4239-11eb-8478-f281bf40fce1.png =600x)
*fzf-preview.vimのプレビュー画面*

##### その他乗り換えるべきプラグイン

- タスクランナー系 → VSCode本体機能
- デバッガー系 → VSCode本体機能
- ファイラー系 → VSCode本体機能

### VSCode用の設定をdotfilesで管理しよう

- `.vim/rc/vscode-neovim/mappings.vim`
- `.vim/rc/vscode-neovim/options.vim`

のようにファイルを分割して.vimrc(init.vim)のほうで`source`して読み込むようにして管理しています。

またkeybindings.jsonもdotfiles内で管理するようにしています。VSCodeのSettingsSync機能を使えば共有されると思いますが、設定の変更履歴をgitで管理したかったためにこのような構成にしました。

## ざっと有名どころのプラグインを試してみた

### 動く

- unblevable/quick-scope
- rhysd/clever-f.vim
- terryma/vim-expand-region
- haya14busa/vim-edgemotion
- machakann/vim-columnmove
- machakann/vim-sandwich
- コメント系プラグイン(試したのはnerdcomenter)
- textobj系プラグイン
- 数値を足したり引いたりするプラグイン(試したのはsyngan/vim-clurin)
- yankring系(試したのはnvim-miniyank)
- haya14busa/vim-asterisk
- t9md/vim-quickhl
- mhinz/vim-grepper
- AndrewRadev/linediff.vim
- mattn/vim-sonictemplate（引数補完が効かないのが使いづらい）
- thinca/vim-scouter
- treesitter系（ただしハイライトには使われてないので効果は不明。refactorとかは使える）
- andymass/vim-matchup
- cohama/lexima.vim
- Yggdroot/indentLine

### 動かない

明らかに動きそうにないやつは試してない(winresizerとか)

- カラースキーム（VSCode側のプラグインで設定する必要がある）
- coc系(裏で動いてはいる模様)
- floating windowを使う系
- バッファー操作系
- ウィンドウ操作系
- ファイラー系
- quickfix系
- easymotion(fork版を使えばいいらしい https://github.com/asvetliakov/vim-easymotion)
- mhinz/vim-startify
- machakann/vim-highlightedundo（こいつは動かないだけじゃなくたまにエラーを吐く）
- thinca/vim-ref
- liuchengxu/vim-which-key
- pechorin/any-jump.vim
- tyru/capture.vim
- metakirby5/codi.vim

### プラグイン作者の方へ

Neo Vim(VS Code Neovim)でVimプラグインは動きます。たぶん今度Neo Vim上で動かないんだけどというIssueが来るかもしれません。
そのときの対応は作者の方次第だと思いますが、Vim対応、Neovim対応の他にNeo Vim対応もあるということを心に止めておくとよいかも知れません。

## その他気になったところ

- GitHub Codespace上では動かなかった https://github.com/asvetliakov/vscode-neovim/issues/262
- コマンドラインがコマンドラインじゃない
![2020-12-13_20-50](https://user-images.githubusercontent.com/8683947/102010983-d5fc6f00-3d84-11eb-9d6f-efe972bf9534.png =600x)
- コマンドラインで補完は効くが、引数補完が効かない
![2020-12-19_19-06](https://user-images.githubusercontent.com/8683947/102686809-6297a900-422d-11eb-9247-6a2dbc0066b8.png =600x)
- コマンドの出力がちっさくてわかりにくい
![2020-12-19_21-05](https://user-images.githubusercontent.com/8683947/102688967-f8d3cb00-423d-11eb-90af-fde2b078c45a.png =600x)

## こういう人におすすめ

- vimrcにそこそこ資産が溜まっているけど、Vimに固執してない人
- 元Vimmerだけど職場でエディタハラスメント（主にLiveShareハラスメントな気がしますが）があってVSCodeを使わざるを得ない人
- モダンなものを使ってみたいけど今までできていたことができなくなって、ストレスを貯めたくない人、生産性を落としたくない人

## まとめ

- 中級者以上のVimmerであってもVSCodeVimよりもつらくはない
- Vimスクリプトが動くので、いざとなったらVimスクリプトを書いて問題を解決できる可能性がある
- そこそこのvimrcがあってもライトに試したり、乗り換えたりすることは可能(ただし、使いながらチューニングしていく必要はある)
- VimのプラグインもVSCodeのプラグインも動いていい感じ
- 補完とかはVSCodeがいい感じにやってくれるので強い
- Neo Vim(VS Code Neovim)は限りなくVimに近いが***これはVimではない***。要はマウス操作が必要だったり、コピペできないところがあったりする

個人的にはVimの資産を持っていない人であればVSCodeVimでも十分だと感じています。Vimの使い方がよくわからん・・・って人はぜひ覚えた方がいいです。コーディング速度が劇的に向上すること間違いないです。[Vimの思想を取り入れて開発速度を2倍に](https://note.com/navitime_tech/n/nf6cae399ae75)とかが参考になるかと思います。

最後に、これだけ紹介しておいて言いにくいのですが、この記事はNeovimで書いています💥

---

:::message
この記事は[Vim Advent Calendar 2020](https://qiita.com/advent-calendar/2020/vim)の19日目の記事になります
:::

