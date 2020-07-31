# Terminal

## Setup

To install `zsh` and `Oh My Zsh` run the following command:

```bash
sudo pacman -S zsh
```

Then:

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

## Spaceship

```bash
export ZSH_CUSTOM=~/.oh-my-zsh
git clone https://github.com/denysdovhan/spaceship-prompt.git "$ZSH_CUSTOM/themes/spaceship-prompt"
ln -s "$ZSH_CUSTOM/themes/spaceship-prompt/spaceship.zsh-theme" "$ZSH_CUSTOM/themes/spaceship.zsh-theme"
```

Add the following to the end of `~/.zshrc`:

```bash
ZSH_THEME="spaceship"

SPACESHIP_PROMPT_ADD_NEWLINE=false
SPACESHIP_CHAR_SYMBOL="❯"
SPACESHIP_CHAR_SUFFIX=" "
```

## Start zplugin

Run:

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/zdharma/zinit/master/doc/install.sh)"
```

Add the following to the end of `~./zshrc`:

```bash
source ~/.zplugin/bin/zplugin.zsh

autoload -Uz _zplugin
(( ${+_comps} )) && _comps[zplugin]=_zplugin
```

## zplugins

Add the following after initialize zplugin in `~./zshrc`:

```bash
zplugin light zsh-users/zsh-autosuggestions
zplugin light zsh-users/zsh-completions
zplugin light zdharma/fast-syntax-highlighting
```

## Other

```bash
unset zle_bracketed_paste
```


## Git

```bash
export GPG_TTY=$(tty)
```