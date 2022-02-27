---
title: "Neovimプラグインで不具合報告するのに便利な再現環境用minimal vimrcの作り方"
emoji: "🔹"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["neovim", "zsh", "bash"]
published: true
---

なんか Neovim のプラグインアップデートしたあと動作がおかしいなー。ん〜と、エラーメッセージと最近あった更新から推察するにこのプラグインがあやしいぞ!ってわかったあとの次の一手を紹介します。

## なにはともあれ Issue を探す

Neovim プラグイン使っている人はかなりの人が Daily でプラグインのアップデートをしているのでまずそのプラグインで類似の報告がないか探します。
Issue は発行したあともテンポよくレスポンスを返したり、追加の調査をしたりするのが大事なのでそれなりに労力を使います。
誰かが報告してくれているならそれに乗っかりましょう。`Same here!`しても通知がうざいだけなので控えめに 👍 のリアクションをするくらいがいいと思われます。

もし最初の Issue を発行した人が再現手順を書いていない場合や、そもそも Issue が挙がっていない場合は、以下のような minimal vimrc(init.vim or init.lua)を作成するのがいいと思います。

## 再現環境用 minimal vimrc の作成

再現環境作るためには環境作るようのシェルスクリプトの関数を`.bashrc`や`.zshrc`に作成しておくと便利です。

init.vim + vim-plug バージョンだとこちらになります。

```bash
function nvim-minimal-env() {
  cd "$(mktemp -d)"
  export HOME=$PWD
  export XDG_CONFIG_HOME=$HOME/.config
  export XDG_DATA_HOME=$HOME/.local/share
  export XDG_CACHE_HOME=$HOME/.cache
  sh -c 'curl -fLo "${XDG_DATA_HOME:-$HOME/.local/share}"/nvim/site/autoload/plug.vim --create-dirs \
       https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim'
  mkdir -p ~/.config/nvim
  cat << EOF > ~/.config/nvim/init.vim
syntax enable
filetype plugin indent on

call plug#begin(stdpath('data') . '/plugged')
" Plug ''
call plug#end()
EOF
  pwd
  ls -la
}
```

init.lua + packer.nvim バージョンだとこんな感じなります。

```bash
function nvim-minimal-env-packer() {
  cd "$(mktemp -d)"
  export HOME=$PWD
  export XDG_CONFIG_HOME=$HOME/.config
  export XDG_DATA_HOME=$HOME/.local/share
  export XDG_CACHE_HOME=$HOME/.cache
  sh -c 'curl -fLo "${XDG_DATA_HOME:-$HOME/.local/share}"/nvim/site/autoload/plug.vim --create-dirs \
       https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim'
  mkdir -p ~/.config/nvim
  cat << EOF > ~/.config/nvim/init.lua
vim.cmd [[syntax enable]]
vim.cmd [[filetype plugin indent on]]

local execute = vim.api.nvim_command
local install_path = vim.fn.stdpath('data')..'/site/pack/packer/opt/packer.nvim'

if vim.fn.empty(vim.fn.glob(install_path)) > 0 then
  execute('!git clone https://github.com/wbthomason/packer.nvim '..install_path)
end

vim.cmd [[packadd packer.nvim]]

return require('packer').startup(function()
  use {'wbthomason/packer.nvim', opt = true}
end)
EOF
--- do not write under this line because it was returned

  pwd
  ls -la
}
```

あとは`nvim-minimal-env` か `nvim-minimal-env-packer`をコマンドで起動してもらえれば再現環境が/tmp 下に作成されます。

その後、その環境で不具合が再現するような手順を構築します。必要があるなら自分の vimrc から設定をコピペしていきます。できるだけ最小の行数で再現するように組み立てます。

## ちなみに zsh プラグインだと

```bash
function zsh-minimal-env() {
  cd "$(mktemp -d)"
  ZDOTDIR=$PWD HOME=$PWD zsh -df
}
```

して対象のプラグインを`source`するのが手っ取り早いです。
