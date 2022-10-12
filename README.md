# dot-files
My dot-files, configs, rc files, etc..

## ZSH

Install [ZSH](https://github.com/ohmyzsh/ohmyzsh/wiki/Installing-ZSH) and make it default shell

```bash
# Check that zsh is installed
zsh --version

# Check what is the current default shell
echo $SHELL

# Make zsh default shell
chsh -s $(which zsh)
```

Reload / open new terminal or log off and back on. Verify the shell is zsh: `echo $SHELL`

## oh-my-zsh
Install [oh-my-zsh](https://github.com/ohmyzsh/ohmyzsh/wiki)

```bash
# curl
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

# wget (alternative)
sh -c "$(wget -O- https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

Copy or link [`HOME/.zshrc`](HOME/.zshrc) to `~/.zshrc`

```bash
# Backup current zshrc, just in case
mv ~/.zshrc ~/.zshrc.bak

# Copy
cp ./HOME/.zshrc ~/.zshrc

# Or link
ln -s "$(pwd)/HOME/.zshrc" ~/.zshrc

# Reload zsh
exec zsh
```

Install custom `oh-my-zsh` plugins:

### zsh-autosuggestions

Install [zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions/blob/master/INSTALL.md#oh-my-zsh)

```bash
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

### history-substring-search

Install [history-substring-search](https://github.com/zsh-users/zsh-history-substring-search#install)

```bash
git clone https://github.com/zsh-users/zsh-history-substring-search ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-history-substring-search
```

### zsh-syntax-highlighting

Install [zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting/blob/master/INSTALL.md#oh-my-zsh)

```bash
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

Reload zsh/omz after installing plugins for changes to take effect:

```bash
# Reload zsh/omz
omz reload

# Or
exec zsh
```

## Starship 🚀

- Install [Nerd fonts](https://www.nerdfonts.com/)
- Install [Starship](https://starship.rs/#install-latest-version)

```bash
curl -sS https://starship.rs/install.sh | sh
```

Copy or link [`HOME/.config/starship.toml`](HOME/.config/starship.toml) to `~/.config/starship.toml`

```bash
# Create .config dir if it doesn't exist
mkdir -p ~/.config

# Backup current zshrc, just in case
mv ~/.config/starship.toml ~/.config/starship.toml.bak

# Copy
cp ./HOME/.config/starship.toml ~/.config/starship.toml

# Or link
ln -s "$(pwd)/HOME/.config/starship.toml" ~/.config/starship.toml

# Reload zsh
exec zsh
```
