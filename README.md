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

