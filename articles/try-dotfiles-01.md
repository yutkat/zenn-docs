---
title: "GitHubでスター数の多いdotfilesを使ってみた"
emoji: "⭐"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["dotfiles", "zsh", "tmux", "vim", "neovim"]
published: true
---

## 企画趣旨

vim-jpでは[vimrc読書会](https://vim-jp.org/reading-vimrc/)という試みが2012年から続いています（毎週土曜日23時からgitterでやってます！誰でも参加OK）。

これに習ってdotfilesでも、有名なdotfilesを勝手に使ってみようという企画です。vimrc読書会の方は毎回メンバーは違いますけどだいたい8人くらい集まってってます。今回のこの企画は残念ながら私一人でやります。

中身を読み出すときりがなくなるので、インストールして動作させてみて、いい点やオシャレポイントを見てみようと思います。

### ルール

- 外側から見た特徴、機能のみにフォーカスする
- 対象となるリポジトリは半年以内に更新があるものとする
- スター数が多いものから順に試す
- Linux(docker上)で動作すること（私がLinux環境しかないため）
- インストール等がうまくいかずに動かなかったときは動かなかった旨だけ記述
- ３個動くものが試せたらそこで終了
- 試すものは主に、シェル、tmuxのターミナルマルチプレクサ、エディタとする

## データ収集

データはGitHubのGraphQLを使って収集することにする。
https://developer.github.com/v4/explorer/

クエリはこんな感じ

```graphql

{
  search(query: """
    dotfiles
    stars:>50
    pushed:>=2020-06-01
    sort:stars
  """, type: REPOSITORY, first: 100) {
    edges {
      node {
        ... on Repository {
          nameWithOwner
          stargazerCount
          updatedAt
          url
          description
        }
      }
    }
    pageInfo {
      endCursor
      startCursor
    }
  }
}
```

簡単に調べるなら https://awesomeopensource.com/projects/dotfiles というサイトもある模様

## 調べてみた

出力された結果を一つずつ調べていく。作業内容としてはブラウザでGitHubを開いてREADMEを見ていく地味なもの。
スター数の多いものから列挙していく。

| url                                       | stars                                                                                  | comment                                                                                                                                                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| https://github.com/mathiasbynens/dotfiles | [![](https://img.shields.io/github/stars/mathiasbynens/dotfiles?label=%20&logo=%20)]() | Mac用                                                                                                                                                                                                                                                         |
| https://github.com/gpakosz/.tmux          | [![](https://img.shields.io/github/stars/gpakosz/.tmux?label=%20&logo=%20)]()          | Linuxで動きそうだけどtmuxの設定しかなかった                                                                                                                                                                                                                   |
| https://github.com/lewagon/dotfiles       | [![](https://img.shields.io/github/stars/lewagon/dotfiles?label=%20&logo=%20)]()       | install.shを見てみたらMac用みたい                                                                                                                                                                                                                             |
| https://github.com/skwp/dotfiles          | [![](https://img.shields.io/github/stars/skwp/dotfiles?label=%20&logo=%20)]()          | Mac用                                                                                                                                                                                                                                                         |
| https://github.com/thoughtbot/dotfiles    | [![](https://img.shields.io/github/stars/thoughtbot/dotfiles?label=%20&logo=%20)]()    | Mac用                                                                                                                                                                                                                                                         |
| https://github.com/holman/dotfiles        | [![](https://img.shields.io/github/stars/holman/dotfiles?label=%20&logo=%20)]()        | Mac用                                                                                                                                                                                                                                                         |
| https://github.com/paulirish/dotfiles     | [![](https://img.shields.io/github/stars/paulirish/dotfiles?label=%20&logo=%20)]()     | Mac用                                                                                                                                                                                                                                                         |
| https://github.com/jessfraz/dotfiles      | [![](https://img.shields.io/github/stars/paulirish/dotfiles?label=%20&logo=%20)]()     | ようやくLinuxで動くdotfilesにたどり着いた。OSの指定は特になかったのでArchLinuxのdocker上でインストールしてみる。[使用レポートはこちら](#jessfraz)                                                                                                            |
| https://github.com/elenapan/dotfiles      | [![](https://img.shields.io/github/stars/elenapan/dotfiles?label=%20&logo=%20)]()      | 調子良く２回連続でLinuxユーザーにあたった。dotfiles上位勢はMacが占めてるみたいなんで2000スターくらいからがLinuxユーザーが多いのかな？Linuxユーザーはあまりブログとか書かないからスターが増えないとか？（適当に邪推してる） [使用レポートはこちら](#elenapan) |
| https://github.com/nicknisi/dotfiles      | [![](https://img.shields.io/github/stars/nicknisi/dotfiles?label=%20&logo=%20)]()      | この人もLinuxで動きそうなので最後の評価dotfilesになりそう。シンプル目が多いのでド派手なのを期待したい。[使用レポートはこちら](#nicknisi)|


## 実際に使ってみた

### jessfraz

[jessfraz/dotfiles](https://github.com/jessfraz/dotfiles)

まず最初に思ったのが、フォントがリポジトリに同梱されてて重い・・・（350MBあった）。 `git clone` がなかなか終わらない・・・
インストールはmakeを使っている。インストール時にsystemdのサービスをreloadしようとして失敗する（ここはdocker環境のため）。無視して進める。

どうやらbashユーザーの模様。tmuxも設定がある。エディタはVSCodeを使ってるみたい（なのでdotfiles内には設定がなかった）

インストール時に各種パッケージはインストールしてくれてないのでtmux等は手動インストールが必要だった。
tmuxを起動してみたが最新の3.1-rc-1には対応してないみたいだ。エラーがでる。

全体はこんな感じ。
![386f2547-9b5b-015b-98f0-7d11dc12a810](https://user-images.githubusercontent.com/8683947/100546234-93766500-32a3-11eb-89b4-4f597c32c8c0.png)

シンプルな[starship](https://github.com/denysdovhan/spaceship-prompt) likeなプロンプトに最低限の情報が記述されてるスタイル。gitのブランチも表示されている。
ただ、コマンドの実行結果のコードはほしいところ。tmuxのプレフィックスはCtrl-zを使用してるみたい。なんかシェルの一時停止ができなくなりそうだけどいいのかな？？tmuxにあまり設定はしてないみたいなのでターミナルをヘビーに使うユーザーという感じではないみたい。
デスクトップ環境はi3だったのでそちらも見てみたが設定少なめなシンプルな感じだった。

全体的にはシンプルな感じでミニマルdotfilesとしてはいい感じだと思う。

### elenapan

[elenapan/dotfiles](https://github.com/elenapan/dotfiles)

READMEが結構しっかりしてる。スヌーピーがかわいい。ArchLinuxユーザーでNeovimユーザーでzshユーザーだ。私と同じ仲間。ウィンドウマネージャーはAwesomeWMらしい。
![fc2ff6e5-87da-7d8a-7398-9baee26669b8](https://user-images.githubusercontent.com/8683947/100546254-b99c0500-32a3-11eb-8584-2795773e729f.png)


インストール手順が結構複雑だ・・・５個もフォントが必須って一体・・・今回はミニマルで構成する。
dotfilesのインストーラーがなく適当にコピーしろって感じですかね。

zsh立ち上げるとoh-my-zshがないって怒られたのでインストールする。tmuxは使わなくてシェルもoh-my-zshのほぼデフォルトであまりカスタマイズしてない感じですね。zshのプラグインも入ってない。シンプル、悪く言えば面白くもない。。。

![d14418fd-5f1f-f76e-d194-3a5f6bd8f1ae](https://user-images.githubusercontent.com/8683947/100546271-cfa9c580-32a3-11eb-99da-dd47c4cbfacd.png)

せっかくneovimの設定もあるので立ち上げてみる

![1d6dcdfa-844d-70c9-627e-d17d22be77e4](https://user-images.githubusercontent.com/8683947/100546288-e8b27680-32a3-11eb-8e7a-cc50de930913.png)

プラグインも入ってない感じでシンプル。ちょっとシンプルすぎない？これで開発するのは相当しんどい気がするぞ・・・

### nicknisi

[nicknisi/dotfiles](https://github.com/nicknisi/dotfiles)

スクリーンショット的には結構カスタマイズしているみたいなので期待できる気もする。
![ba5f1230-f666-daf1-05fd-53350a78a09e](https://user-images.githubusercontent.com/8683947/100546301-fcf67380-32a3-11eb-9f1b-ba718b4d80a5.png)

！！！Dockerファイルがある！dockerでのセットアップ方法も書いてる。https://github.com/nicknisi/dotfiles#docker-setup
斬新だ。

インストーラーがかっけえ。シンプルが多かったから少し感動。
セットアップはhomebrew(Linux版)を使ってる。Ubuntuとかでも最新のバージョンのソフトが楽にインストールできて、設定も簡単だからいいですね。
![da783203-b904-cf07-3c26-3e8cbe74ff56](https://user-images.githubusercontent.com/8683947/100546310-0aabf900-32a4-11eb-81a4-62717eaad6e5.png)

gitのセットアップもしてくれる。
![4182ce2b-cd46-442c-a339-eee6b22b33a3](https://user-images.githubusercontent.com/8683947/100546322-18fa1500-32a4-11eb-8cf2-bf3b88b21d66.png)

zshを起動してみる。おお！プラグインを自動でインストールしてくれた。
プロンプトは[pure](https://github.com/sindresorhus/pure)っぽい見た目でシンプルでいい。補完はfzf補完を使っている模様。zshのプラグイン管理はzfetchっていう自前のものを使っていた。
![ee72235c-2838-2ac4-54a2-ca951f48ab66](https://user-images.githubusercontent.com/8683947/100546331-2ca57b80-32a4-11eb-902b-51c0c9a43a41.png)

tmuxはフォントがあってないせいか表示されてない文字がある。lsしたときに色がつかないのが少し気になる(tmuxじゃなくてもつかない)。
tmuxのステータスラインとシェルのテーマもあっていて素敵。紫基調な感じなのかな？
![1a2f43b8-717e-baa3-4bb1-8c642a230a2b](https://user-images.githubusercontent.com/8683947/100546342-45159600-32a4-11eb-9578-b2da7b4ac11c.png)

Neovimもおしゃれな見た目でプラグインも50個くらい入ってた。
![174d2cb9-e7c0-5755-4cc0-31e57e669cb4](https://user-images.githubusercontent.com/8683947/100546357-55c60c00-32a4-11eb-9479-c93768577f99.png)

## 全体的な総評

スター数が多いものはサンプル的なシンプルなものが多いみたいですね。100-1000スターあたりにもう少し濃ゆいdotfilesがありそうな気もするので、次はもう少し検索条件を見直して調査してみたいと思います。
あと、調べたもののREADMEを見て思ったのは、スター数が多いリポジトリがすごく凝っているかというとそうではなく、ブログやRedditなどでうまく紹介しているものが多いようですね(プロモーションがうまいということ)。

## さいごに

偉そうに寸評してるけどお前のはどうやねんって思ってる人もいるので一応貼っておきます。

[![yutkat/dotfiles](https://github-link-card.s3.ap-northeast-1.amazonaws.com/yutkat/dotfiles.png =250x)](https://github.com/yutkat/dotfiles)

ArchLinuxのdockerで
```bash
pacman -Sy
pacman -S git sudo
git clone https://github.com/yutkat/dotfiles.git
./dotfiles/.bin/dotinstall.sh install
```
すれば動くと思います。

