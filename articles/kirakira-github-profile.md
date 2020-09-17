---
title: "GitHubProfileのページを可能な限りキラキラさせる方法"
emoji: "🌠"
type: "tech"
topics: ["github", "githubprofile", "githubactions"]
published: true
---

# GitHubProfileページとは

GitHubの自分のProfileページを自由にカスタマイズできるのご存知ですか？？
https://docs.github.com/en/github/setting-up-and-managing-your-github-profile/about-your-profile

↓↓↓こういうやつです↓↓↓
![](https://storage.googleapis.com/zenn-user-upload/nf057hszbpch06xn0pfih2xpu7zv)

---

イケてる？エンジニアは結構カスタマイズして公開してみてるみたいなんで、一度は目にしたことがあるかと思います。この流行に乗り遅れないようにちょっとでもキラキラにしてみたくないですか？？

結構いろんなことができるんで、[ゲームを公開している人](https://github.com/timburgan)や[今聞いてる音楽を教えてくれる人](https://github.com/codestackr)、[好きなアニメ・マンガを羅列している人](https://github.com/moepoi)など様々ですが、エンジニア的な情報だけを可能な限りビジュアライズしてくれるようにする方法を紹介したいと思います。


# 私のGitHubProfileを晒す

ここに私のProfileがありますので晒しておきます。
[![yutakatay profile](https://github-link-card.s3.ap-northeast-1.amazonaws.com/yutakatay/yutakatay.png =250x)](https://github.com/yutakatay/yutakatay)

全体をスクショしてみるとこんな感じです。
![](https://storage.googleapis.com/zenn-user-upload/ysqdchwr2k2ba4o9edbiawop8n4o)

画像やグラフが多めでなんかすごいエンジニアな感じがしますよね！**（なお実際の実力が伴っているわけではない）**
重複している情報もありますが、キラキラのためには仕方ありません。


# 作り方

## 1. 自分のユーザー名のリポジトリを作ってGitHubProfileに表示する

公式にやり方が載ってますのでそちらを参照して作ってください。正直クリックするだけです。
https://docs.github.com/ja/github/setting-up-and-managing-your-github-profile/managing-your-profile-readme

## 2. バッジ部分を作成する

![](https://storage.googleapis.com/zenn-user-upload/mjbbuigoc2lqh6swbuyab6ndsnqx)

内容は
- Profileページの閲覧カウンター数
- Twitterのアカウントフォロワー数
- GitHubのアカウントフォロワー数
- Redditのカルマ
- Stackoverflowの実績
- Qiitaのコントリビュート数
です。

ここのほとんどのバッジは、 [shields.io](https://shields.io/) の https://shields.io/category/social とかから作成しているだけです。
それ以外で使用しているのは、Profileの閲覧数は https://github.com/antonkomarev/github-profile-views-counter を、Qiitaのコントリビュート数は https://qiita.com/mikkame/items/f2c60d9caf8a8e38ec50 を利用させていただいています。

私の[README.md](https://raw.githubusercontent.com/yutakatay/yutakatay/master/README.md)の↓↓↓の部分のユーザー名部分を変えればいいと思います。

```html
<p align="left"> 
  <a href="https://github.com/yutakatay/yutakatay/">
    <img src="https://komarev.com/ghpvc/?username=yutakatay" alt="yutakatay" />
  </a>
  <a href="http://twitter.com/yutakatay">
    <img height="20" src="https://img.shields.io/twitter/follow/yutakatay?label=Twitter&logo=twitter&style=flat" />
  </a>
  <a href="https://github.com/yutakatay">
    <img height="20" src="https://img.shields.io/github/followers/yutakatay?label=follow&logo=github&style=flat" />
  </a>
  <a href="https://www.reddit.com/user/yutakatay">
    <img height="20" src="https://img.shields.io/reddit/user-karma/combined/yutakatay?label=Reddit&logo=reddit&style=flat" />
  </a>
  <a href="https://stackoverflow.com/users/5720201/yutakatay">
    <img height="20" src="https://img.shields.io/stackexchange/stackoverflow/r/5720201?label=StackOverflow&logo=stack-overflow&style=flat" />
  </a>
  <a href="http://qiita.com/yutakatay">
    <img height="20" src="https://qiita-badge.apiapi.app/s/yutakatay/posts.svg" />
  </a>
  <//qiita.com/yutakatay">
    <img height="20" src="https://qiita-badge.apiapi.app/s/yutakatay/contributions.svg" />
  </a>
</p>
```

## 3. 上の方のグラフ部分を作成する

![](https://storage.googleapis.com/zenn-user-upload/r2dmzwp2qwq7ryict6f721mi471f =400x)

ここでは３つのサービスを使って活動実績を表示してます。

### GitHubReadmeStats

たぶんGitHubProfileの中で一番よく見かける個人のGitHubの活動履歴からランクを作成してくれるものです。
- https://github.com/anuraghazra/github-readme-stats

完全に余談ですが、私はこのランクは幽☆遊☆白書の妖怪ランクと同じ定義と考えていて、S級妖怪（ランク）の人は手が付けられないので、あまり刺激しないほうがよいでしょう。

### トロフィー

[ryo-ma](https://github.com/ryo-ma)さんの作ったサービスを利用してます。Qiitaの記事にわかりやすく紹介されてるのでそちらを参考にすればよいと思います。
- Qiita: https://qiita.com/ryo-ma/items/c6298020098cb631f46e
- repository: https://github.com/ryo-ma/github-profile-trophy

### github-profile-summary-cards

- repository: https://github.com/vn7n24fzkq/github-profile-summary-cards

情報的にはGitHubReadmeStatsとあまり変わりませんが、こちらはGitHubActionsを使う必要があります。重複している情報も多いので必須ではないですが、privateコンテンツの情報が取れるのが強みです。


## 4. スキル一覧っぽいのを作成する

![](https://storage.googleapis.com/zenn-user-upload/et90qbryzjlf6cvm14n1qqax2w6y)

[GitHub Profile README Generator](https://rahuldkjain.github.io/gh-profile-readme-generator/) からアイコン部分だけをもらいました。
このサイトでそのまま作ってもいいんですが、結構ダサめに仕上がってキラキラ度が下がるので要注意です。


## 5. 下の統計データっぽいところを作成する

![](https://storage.googleapis.com/zenn-user-upload/c5plughose5hogi9vuk41r7phvki =400x)

### wakatime

統計データは [wakatime](https://wakatime.com/) を使って取得しますので、wakatimeに登録する必要があります。私もwakatimeはこのProfileを作るときに初めて触ったのですが、他の作業時間可視化ツールと比べて、どの言語、どのリポジトリをどれくらい触ったかがわかって、これだけでもとても楽しいです。
※作業を記録するためにはエディターにプラグインを入れる必要があります

無料版でも最新２週間のデータなら保存してくれます。（できれば有料版を使いたいくらいなんですが月9ドルはちょっと高いですよね。。。）

### Profile-Readme-WakaTime（統計情報のサマリー用）

何時間作業したかのサマリーをwakatimeから取得して画像化してくれるのが
https://github.com/avinal/Profile-Readme-WakaTime
です。画像は自分のリポジトリのimagesの下に作成されます。
このツールはGitHubActionsを使っています。基本的にREADMEに書いてあるものをコピペするだけなので難しくはないはずです。参考に私の設定のリンクを貼っておきます。 https://github.com/yutakatay/yutakatay/blob/master/.github/workflows/main.yml

本来はよく使われている
[waka-readme](https://github.com/athul/waka-readme)
を使いたいのですが、後述のwaka-readme-statsと埋め込みするときのキーワードがかぶっているため使えませんでした。（waka-readmeは悪くないwaka-readme-stats側がforkしていてそのまま同じキーワードで置換していることに問題がある）

### waka-readme-stats（統計情報の詳細用）

私のGitHubProfileで一番下の折りたたみ部分になっているところにある、wakatimeが集計した統計情報の詳細を公開するための部分です。
いつ作業してるか、何曜日に進捗が出てるか等々作業内容が丸裸です。

この情報を出すためにはこのリポジトリを使う必要があります。
- https://github.com/anmol098/waka-readme-stats

基本な使い方としてはwakatimeに登録して、APIキー、GitHubのアクセストークンを払い出し、GitHubActionsで動かすだけです。
また、自分のProfileの方のREADMEにはデータを埋め込む目印として
```
<!--START_SECTION:waka-->
<!--END_SECTION:waka-->
```
を記述する必要があります。

詳しくはREADMEを読んでみてください。（そんなに難しくない）


# もっと輝きたいあなたに

[awesome-github-profile](https://zzetao.github.io/awesome-github-profile/)
に超キラキライケてるProfileがいっぱい載ってます。もっとキラキラしたい方は参考にしてみてください。


# 最後に

GitHubProfileは最近カスタマイズできるようになったんで、これからもまだまだいろいろなサービス、試み、トレンドがでてくると思います。

**キラキラは一夜にしてならず！アンテナを張って、常に自分磨きの努力を続けていきましょう！！**
