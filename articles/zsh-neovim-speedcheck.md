---
title: "zshとNeovimの簡単な起動速度の測定方法"
emoji: "⏲️"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["zsh", "neovim"]
published: true
---

毎日使うシェルやエディタって起動速度気になりますよね？そこで簡単に測定する方法を紹介したいと思います！

以下のシェルスクリプトの関数を`.zshrc`に追加して使うだけで OK です。

## zsh

### 起動速度計測

```bash
function zsh-startuptime() {
  local total_msec=0
  local msec
  local i
  for i in $(seq 1 10); do
    msec=$((TIMEFMT='%mE'; time zsh -i -c exit) 2>/dev/stdout >/dev/null)
    msec=$(echo $msec | tr -d "ms")
    echo "${(l:2:)i}: ${msec} [ms]"
    total_msec=$(( $total_msec + $msec ))
  done
  local average_msec
  average_msec=$(( ${total_msec} / 10 ))
  echo "\naverage: ${average_msec} [ms]"
}
```

結局、起動速度はマシンスペックに依存したりするので、プレーンな状態の設定と比較したい場合はこちら

```bash
function zsh-startuptime-slower-than-default() {
  local time_rc
  time_rc=$((TIMEFMT="%mE"; time zsh -i -c exit) &> /dev/stdout)
  # time_norc=$((TIMEFMT="%mE"; time zsh -df -i -c exit) &> /dev/stdout)
  # compinit is slow
  local time_norc
  time_norc=$((TIMEFMT="%mE"; time zsh -df -i -c "autoload -Uz compinit && compinit -C; exit") &> /dev/stdout)
  echo "my zshrc: ${time_rc}\ndefault zsh: ${time_norc}\n"

  local result
  result=$(scale=3 echo "${time_rc%ms} / ${time_norc%ms}" | bc)
  echo "${result}x slower your zsh than the default."
}
```

### プロファイリング

測定するとどこが遅いのか気になりますよね？
プロファイリングは以下のようにすれば取得できます。

```bash: .zshrc
# .zshrcの一番始めに記載すること
if [ "$ZSHRC_PROFILE" != "" ]; then
  zmodload zsh/zprof && zprof > /dev/null
fi
```

```bash
function zsh-profiler() {
  ZSHRC_PROFILE=1 zsh -i -c zprof
}
```

## Neovim

### 起動速度計測

```bash
function nvim-startuptime() {
  local file=$1
  local total_msec=0
  local msec
  local i
  for i in $(seq 1 10); do
    msec=$({(TIMEFMT='%mE'; time nvim --headless -c q $file ) 2>&3;} 3>/dev/stdout >/dev/null)
    msec=$(echo $msec | tr -d "ms")
    echo "${(l:2:)i}: ${msec} [ms]"
    total_msec=$(( $total_msec + $msec ))
  done
  local average_msec
  average_msec=$(( ${total_msec} / 10 ))
  echo "\naverage: ${average_msec} [ms]"
}
```

```bash
function nvim-startuptime-slower-than-default() {
  local file=$1
  local time_file_rc
  time_file_rc=$(mktemp --suffix "_nvim_startuptime_rc.txt")
  local time_rc
  time_rc=$(nvim --headless --startuptime ${time_file_rc} -c "quit" $file > /dev/null && tail -n 1 ${time_file_rc} | cut -d " " -f1)

  local time_file_norc
  time_file_norc=$(mktemp --suffix "_nvim_startuptime_norc.txt")
  local time_norc
  time_norc=$(nvim --headless --noplugin -u NONE --startuptime ${time_file_norc} -c "quit" $file > /dev/null && tail -n 1 ${time_file_norc} | cut -d " " -f1)

  echo "my vimrc: ${time_rc}s\ndefault neovim: ${time_norc}s\n"
  local result
  result=$(scale=3 echo "${time_rc} / ${time_norc}" | bc)
  echo "${result}x slower your Neovim than the default."
}
```

### プロファイリング

```bash
function nvim-profiler() {
  local file=$1
  local time_file
  time_file=$(mktemp --suffix "_nvim_startuptime.txt")
  echo "output: $time_file"
  time nvim --headless --startuptime $time_file -c q $file
  tail -n 1 $time_file | cut -d " " -f1 | tr -d "\n" && echo " [ms]\n"
  cat $time_file | sort -n -k 2 | tail -n 20
}
```

## 私の測定結果

| 測定項目         | 対象                                   | 結果     |
| ---------------- | -------------------------------------- | -------- |
| 起動速度         | zsh                                    | 97 [ms]  |
| デフォルトとの差 | zsh                                    | 5 倍     |
| 起動速度         | Neovim 空バッファー                    | 107 [ms] |
| デフォルトとの差 | Neovim 空バッファー                    | 12 倍    |
| 起動速度         | Neovim: 20 行の text を開いた場合      | 114 [ms] |
| デフォルトとの差 | Neovim: 20 行の text を開いた場合      | 11 倍    |
| 起動速度         | Neovim: 100 行の Lua を開いた場合      | 124 [ms] |
| デフォルトとの差 | Neovim: 100 行の Lua を開いた場合      | 12 倍    |
| 起動速度         | Neovim: 100 行の Markdown を開いた場合 | 159 [ms] |
| デフォルトとの差 | Neovim: 100 行の Markdown を開いた場合 | 14 倍    |

私はそこそこチューンナップしてますが、まあ正直 zsh だと 200-300ms 以内、Neovim だと 500-600ms 以内に起動していれば使用感は問題ないと思います。
一生懸命数 ms を削るよりは別のことをしたほうが有益だったりもしますので適度に楽しむのをおすすめします。
