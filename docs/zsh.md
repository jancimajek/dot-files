
- [ZSH](#zsh)
- [oh-my-zsh](#oh-my-zsh)
  - [zsh-autosuggestions](#zsh-autosuggestions)
  - [history-substring-search](#history-substring-search)
  - [zsh-syntax-highlighting](#zsh-syntax-highlighting)
- [Starship 🚀](#starship-)
  - [Zsh (Mac & Linux)](#zsh-mac--linux)


# ZSH

Install [ZSH](https://github.com/ohmyzsh/ohmyzsh/wiki/Installing-ZSH) and make it default shell

Install / update on Ubuntu
```bash
sudo apt install zsh
```

Check that zsh is installed
```bash
zsh --version
```

Check what is the current default shell
```bash
echo $SHELL
```

Make zsh default shell
```bash
chsh -s $(which zsh)
```

Reload / open new terminal or log off and back on. Verify the shell is zsh: `echo $SHELL`


# oh-my-zsh
Install [oh-my-zsh](https://github.com/ohmyzsh/ohmyzsh/wiki)

cURL
```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

wget (alternative)
```bash
sh -c "$(wget -O- https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

Update
```bash
omz update
```

Copy or link [`HOME/.zshrc`](../HOME/.zshrc) to `~/.zshrc`

Backup current zshrc, just in case
```bash
mv ~/.zshrc ~/.zshrc.bak
```

Copy config
```bash
cp ./HOME/.zshrc ~/.zshrc
```

Or link
```bash
ln -s "$(pwd)/HOME/.zshrc" ~/.zshrc
```

Reload zsh
```bash
exec zsh
```

Install custom `oh-my-zsh` plugins:


## zsh-autosuggestions

Install [zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions/blob/master/INSTALL.md#oh-my-zsh)

```bash
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```


## history-substring-search

Install [history-substring-search](https://github.com/zsh-users/zsh-history-substring-search#install)

```bash
git clone https://github.com/zsh-users/zsh-history-substring-search ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-history-substring-search
```


## zsh-syntax-highlighting

Install [zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting/blob/master/INSTALL.md#oh-my-zsh)

```bash
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

Reload zsh/omz after installing plugins for changes to take effect:

Reload zsh/omz
```bash
omz reload
```

Or
```bash
exec zsh
```


# Starship 🚀

- Install [Nerd fonts](https://www.nerdfonts.com/)
- Install [Starship](https://starship.rs/#install-latest-version)


## Zsh (Mac & Linux)

> *For configuring Starship for Windows Powershell, see [Windows guide](./windows.md#starship-🚀)*

Install Starship
```bash
curl -sS https://starship.rs/install.sh | sh
```

Copy or link [`HOME/.config/starship.toml`](../HOME/.config/starship.toml) to `~/.config/starship.toml`

Create .config dir if it doesn't exist
```bash
mkdir -p ~/.config
```

Backup current Starship config, just in case
```bash
mv ~/.config/starship.toml ~/.config/starship.toml.bak
```

Copy Starship config
```bash
cp ./HOME/.config/starship.toml ~/.config/starship.toml
```

Or link it
```bash
ln -s "$(pwd)/HOME/.config/starship.toml" ~/.config/starship.toml
```

Reload zsh
```bash
exec zsh
```
