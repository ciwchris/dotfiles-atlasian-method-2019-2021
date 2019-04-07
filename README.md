# dotfile versioning

Strategy from [The best way to store your dotfiles: A bare Git
repository](https://www.atlassian.com/git/tutorials/dotfiles)

## Setup

```sh
git init --bare $HOME/.cfg
alias config='/usr/bin/git --git-dir=$HOME/.cfg/ --work-tree=$HOME'
config config --local status.showUntrackedFiles no
echo -e "# dotfile versioning\nalias config='/usr/bin/git --git-dir=$HOME/.cfg/ --work-tree=$HOME'" >> $HOME/.zshrc
```

It would be nice to have a README and LICENSE in the remote repository but not have them show up on
the computer the dotfiles are bening used. Therefore tell git to not pay attention to those files
and then remove them.

```sh
config update-index --assume-unchanged README.md
rm README.md
config update-index --assume-unchanged LICENSE
rm LICENSE
```

## To use on a new machine

```sh
alias config='/usr/bin/git --git-dir=$HOME/.cfg/ --work-tree=$HOME'
echo ".cfg" >> .gitignore
git clone --bare git@github.com:ciwchris/dotfiles.git $HOME/.cfg
alias config='/usr/bin/git --git-dir=$HOME/.cfg/ --work-tree=$HOME'
# Next command may fail because files may already exist. Either backup or remove them.
config checkout
config config --local status.showUntrackedFiles no
```
