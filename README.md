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

## SSH

```bash
mkdir -p ~/.ssh
chmod 700 ~/.ssh

cp ./HOME/.ssh/config ~/.ssh/config
chmod 600 ~/.ssh/config
```

Replace `Firstname.Lastname` in the [`~/.ssh/config`](~/.ssh/config) file with real name.


### Generate a new SSH key

Generate a [new ssh key](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

```bash
# Generate a new key:
ssh-keygen -t ed25519 -C "your@email.com ED25519 Device YYYY-MM-DD"

# Check ssh agent is running
eval "$(ssh-agent -s)"

# Pre OSX Monterey 12.0
ssh-add -K ~/.ssh/id_ed25519

# Post OSX Monterey 12.0
ssh-add --apple-use-keychain ~/.ssh/id_ed25519
```

## Git

Download and install [latest version of Git](https://git-scm.com/downloads)

```bash
# Copy git config & aliases
cp ./HOME/.gitconfig ~/.gitconfig

# Set username and email
git config --global user.name "YOUR NAME"
git config --global user.email "your@email.com"

# Verify username and email are set 
git config --global user.name
git config --global user.email
```


## GitHub

Install [GH CLI](https://cli.github.com/) and [login into GitHub](https://cli.github.com/manual/gh_auth_login)

```bash
# Mac insall using Brew
brew install gh 

# Authenticate with GitHub
gh auth login
```

If you haven't uploaded your SSH key to GitHub during the auth/login process, manually [add your SSH key to GitHub](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account) using the web or `gh` CLI command:

```bash
# Add SSH key to GitHub (provide decriptive label)
gh ssh-key add ~/.ssh/id_ed25519.pub --title "your@email.com ED25519 Device YYYY-MM-DD OPT_DESCRIPTION"
```

```bash
# Test ssh is working
ssh -T git@github.com
```