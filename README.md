# dot-files
My dot-files, configs, rc files, etc..

## TODO

- [ ] [SSH](#ssh)
  - [ ] [Generate a new SSH key](#generate-a-new-ssh-key)
- [ ] [Git](#git) (set user name & email)
- [ ] [GitHub CLI](#github-cli)
- [ ] Clone this repo `git clone git@github.com:jancimajek/dot-files.git`
- [ ] [Git](#git) (everything again)
- [ ] [Signing git commits](#signing-git-commits)
- [ ] [ZSH](#zsh)
- [ ] [oh-my-zsh](#oh-my-zsh)
- [ ] [Starship](#starship-🚀)

## ZSH

Install [ZSH](https://github.com/ohmyzsh/ohmyzsh/wiki/Installing-ZSH) and make it default shell

```bash
# Install / update on Ubuntu
sudo apt install zsh

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

# Update
omz update
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


### Zsh (Mac & Linux)
```bash
# Install Starship
curl -sS https://starship.rs/install.sh | sh
```

Copy or link [`HOME/.config/starship.toml`](HOME/.config/starship.toml) to `~/.config/starship.toml`

```bash
# Create .config dir if it doesn't exist
mkdir -p ~/.config

# Backup current Starship config, just in case
mv ~/.config/starship.toml ~/.config/starship.toml.bak

# Copy Starship config
cp ./HOME/.config/starship.toml ~/.config/starship.toml

# Or link it
ln -s "$(pwd)/HOME/.config/starship.toml" ~/.config/starship.toml

# Reload zsh
exec zsh
```

### Powershell (Windows)

> *This may or may not work - probably won't 🤷‍♂️*


Best way is to [download and install via the MSI Installer](https://github.com/starship/starship/releases/latest)

```bash
# Install Starship (this may not work, use MSI Installer instead -- see above)
# scoop install starship
```

> *You will probably need to restart all terminals, Powershells and the entire VSCode for changes to take effect.*

Add the following at the end of `$HOME\Documents\WindowsPowerShell\Microsoft.PowerShell_profile.ps1` so that Starship starts automatically when Powershell is launched

```bash
Invoke-Expression (&starship init powershell)
```

Copy [`HOME/.config/starship.toml`](HOME/.config/starship.toml) to `$HOME\.config\starship.toml`

```bash
# Create .config dir if it doesn't exist
New-Item -ItemType Directory -Force $HOME\.config 
# or: mkdir -p ~/.config

# Backup current Starship config, just in case
Move-Item $HOME\.config\starship.toml $HOME\.config\starship.toml.bak 
# or: mv ~/.config/starship.toml ~/.config/starship.toml.bak

# Copy Starship config
Copy-Item .\HOME\.config\starship.toml $HOME\.config\starship.toml
# or: cp ./HOME/.config/starship.toml ~/.config/starship.toml

# Reload Powershell
. $profile
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

# Ubuntu
ssh-add ~/.ssh/id_ed25519
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

On Windows only, you should set [`#core.autocrlf`](https://www.git-scm.com/book/en/v2/Customizing-Git-Git-Configuration) to `true` (on Mac & Linux this is should stay configured as `input`)
```bash
# Windows ONLY - handle CRLF conversion correctly
git config --global core.autocrlf true
```


## GitHub CLI

Install [GH CLI](https://cli.github.com/) and [login into GitHub](https://cli.github.com/manual/gh_auth_login)

- [Linux installation guide](https://github.com/cli/cli/blob/trunk/docs/install_linux.md#debian-ubuntu-linux-raspberry-pi-os-apt)


```bash
# Mac install using Brew
brew install gh 

# Ubuntu - pre-install
type -p curl >/dev/null || sudo apt install curl -y
curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | sudo dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg \
&& sudo chmod go+r /usr/share/keyrings/githubcli-archive-keyring.gpg \
&& echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null

# Ubuntu - install & update
sudo apt update
sudo apt install gh

# Windows (this is flimsy, better install directly via MSI installer)
# scoop install gh
```

On Windows, it's better to [download and run the MSI installer](https://github.com/cli/cli/releases/latest) directly

Authenticate with GitHub & upload SSH key

```bash
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


## Signing git commits

Sign git commits and get [`Verified`](https://docs.github.com/en/authentication/managing-commit-signature-verification/about-commit-signature-verification) mark on GitHub

### Signing using SSH key

> *Note: This is fairly new, available since [`git v2.34`](https://github.blog/2021-11-15-highlights-from-git-2-34/#tidbits) and [GitHub](https://github.blog/changelog/2022-08-23-ssh-commit-verification-now-supported/) since Aug 2022. However, VSCode does not support this yet, so it only works with CLI commits. Use [GPG signing](#signing-using-gpg-key) until it is supported.*

#### Configure Git

[Configure Git](https://docs.github.com/en/authentication/managing-commit-signature-verification/telling-git-about-your-signing-key#telling-git-about-your-ssh-key) to use the SSH key from previous step to sign git commits

```bash
# Set signing format to ssh
git config --global gpg.format ssh

# Copy SSH public key (alternagtively, open in editor and copy content of the file manually)
pbcopy < ~/.ssh/id_ed25519.pub

# Set git signing key - enclose in single quotes and include all spaces
git config --global user.signingkey 'COPIED_FROM_CLIPBOARD'
```

#### Configure GitHub

In order for GitHub to be able to verify commits, you need to [add SSH public key to GitHub](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)

Add the GPG public key to [GitHub GPG keys](https://github.com/settings/ssh/new): 

- Use title `your@email.com ED25519 Device YYYY-MM-DD OPT_DESCRIPTION (SIGNING KEY)` and 
- ⚠ Key type **MUST BE SET TO** `Signing Key` ⚠



### Signing using GPG key

> *Note: See [SSH signing section](#signing-using-ssh-key) for signing commits using SSH keys (currently not yet supported by VSCode).*

#### Generate GPG key

[Generate a GPG key](https://docs.github.com/en/authentication/managing-commit-signature-verification/generating-a-new-gpg-key) and  [configure Git](https://docs.github.com/en/authentication/managing-commit-signature-verification/telling-git-about-your-signing-key) to use the GPG to sign git commits

```bash
# Generate a new GPG key (RSA 4096)
gpg --full-generate-key
```

#### Configure Git

```bash
# (Un)set GPG format
git config --global --unset gpg.format

# List available GPG keys to get GPG key ID (see below)
gpg --list-secret-keys --keyid-format=long

# Grab GPG key ID from the output, e.g.:
# sec   4096R/3AA5C34371567BD2 2016-03-10 [expires: 2017-03-10]
#             ^^^^^^^^^^^^^^^^
# ID in this case would be GPG_KEY_ID=3AA5C34371567BD2

git config --global user.signingkey 'GPG_KEY_ID'
```

#### Configure GitHub

In order for GitHub to be able to verify commits, [add GPG public key to GitHub](https://docs.github.com/en/authentication/managing-commit-signature-verification/adding-a-gpg-key-to-your-github-account).

```bash
# Print the GPG key ID, in ASCII armor format
gpg --armor --export GPG_KEY_ID
```

Copy your GPG public key, beginning with `-----BEGIN PGP PUBLIC KEY BLOCK-----` and ending with `-----END PGP PUBLIC KEY BLOCK-----`.

Add the GPG public key to [GitHub GPG keys](https://github.com/settings/gpg/new). Use title `your@email.com GPG-RSA-4096 Device YYYY-MM-DD OPT_DESCRIPTION`


### Test git signing

To test that git signing works, add a git commit and push it to GitHub. You should be able to see the `Verified` mark on GitHub


## Scoop (Windows)

> *Just don't bother, you'll waste just time and effort, age 5 years and it won't work at the end anyway. Use MSI installers where possible instead *


Install [scoop package manager for Windows](https://scoop.sh/)

```bash
# Optional: Needed to run a remote script the first time
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser

# Install scoop
iwr -useb get.scoop.sh | iex
```

