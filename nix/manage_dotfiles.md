# Setup your home directory
Inspired by https://news.ycombinator.com/item?id=11070797

```
git init --bare $HOME/.myconf
alias config='/usr/bin/git --git-dir=$HOME/.myconf/ --work-tree=$HOME'
config config status.showUntrackedFiles no
```

Then normal commands work:
```
config status
config add .vimrc
config commit -m "Add vimrc"
config add .config/redshift.conf
config commit -m "Add redshift config"
config push
```

I **think** then you could sneakernet this to a new machine and then:
`git clone --separate-git-dir=~/.myconf /path/to/repo ~`
