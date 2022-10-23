
- [Git](#git)
- [GitHub CLI](#github-cli)
- [Signing git commits](#signing-git-commits)
  - [GPG signing](#gpg-signing)
    - [Installation](#installation)
    - [Configure GPG Agent](#configure-gpg-agent)
    - [Generate GPG key](#generate-gpg-key)
    - [Configure Git](#configure-git)
    - [Configure GitHub](#configure-github)
    - [Test signing](#test-signing)
  - [SSH signing](#ssh-signing)
    - [Configure Git](#configure-git-1)
    - [Configure GitHub](#configure-github-1)


# Git

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


# GitHub CLI

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


# Signing git commits

Sign git commits and get [`Verified`](https://docs.github.com/en/authentication/managing-commit-signature-verification/about-commit-signature-verification) mark on GitHub

## GPG signing

> *Note: See [SSH signing section](#signing-using-ssh-key) for signing commits using SSH keys (currently not yet supported by VSCode).*

### Installation

```bash
# Check if gpg is installed
gpg --version
# Should be version 2
```

If needed, install from [GnuPG website](https://www.gnupg.org/download/). For Windows, download and install [Gpg4win](https://gpg4win.org/download.html) with Kleopatra.


```bash
# Check if GPG Agent is running
gpg-agent
# Expected output: gpg-agent[25800]: gpg-agent running and available

# Start GPG Agent if it's not running
gpgconf --launch gpg-agent
```

On Windows, you can [configure `Task Scheduler` to start GPG Agent](https://stackoverflow.com/a/51407128/192331) on login / computer start


### Configure GPG Agent

Copy [`HOME/.gnupg/gpg-agent.conf`](./HOME/.gnupg/gpg-agent.conf) for to `~/.gnupg/gpg-agent.conf`

```bash
# Create .gnupg dir if it doesn't exist
mkdir -p ~/.gnupg

# Backup current GPG Agent config, just in case
mv ~/.gnupg/gpg-agent.conf ~/.gnupg/gpg-agent.conf.bak

# Copy GPG Agent config
cp ./HOME/.gnupg/gpg-agent.conf ~/.gnupg/gpg-agent.conf
```

### Generate GPG key

[Generate a GPG key](https://docs.github.com/en/authentication/managing-commit-signature-verification/generating-a-new-gpg-key) and  [configure Git](https://docs.github.com/en/authentication/managing-commit-signature-verification/telling-git-about-your-signing-key) to use the GPG to sign git commits

```bash
# Generate a new GPG key (RSA 4096)
gpg --full-generate-key
```

### Configure Git

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

### Configure GitHub

In order for GitHub to be able to verify commits, [add GPG public key to GitHub](https://docs.github.com/en/authentication/managing-commit-signature-verification/adding-a-gpg-key-to-your-github-account).

```bash
# Print the GPG key ID, in ASCII armor format
gpg --armor --export GPG_KEY_ID
```

Copy your GPG public key, beginning with `-----BEGIN PGP PUBLIC KEY BLOCK-----` and ending with `-----END PGP PUBLIC KEY BLOCK-----`.

Add the GPG public key to [GitHub GPG keys](https://github.com/settings/gpg/new). Use title `your@email.com GPG-RSA-4096 Device YYYY-MM-DD OPT_DESCRIPTION`


### Test signing

To test that git signing works, add a git commit and push it to GitHub. You should be able to see the `Verified` mark on GitHub


## SSH signing

> *Note: This is fairly new, available since [`git v2.34`](https://github.blog/2021-11-15-highlights-from-git-2-34/#tidbits) and [GitHub](https://github.blog/changelog/2022-08-23-ssh-commit-verification-now-supported/) since Aug 2022. However, VSCode does not support this yet, so it only works with CLI commits. Use [GPG signing](#signing-using-gpg-key) until it is supported.*

### Configure Git

[Configure Git](https://docs.github.com/en/authentication/managing-commit-signature-verification/telling-git-about-your-signing-key#telling-git-about-your-ssh-key) to use the SSH key from previous step to sign git commits

```bash
# Set signing format to ssh
git config --global gpg.format ssh

# Copy SSH public key (alternagtively, open in editor and copy content of the file manually)
pbcopy < ~/.ssh/id_ed25519.pub

# Set git signing key - enclose in single quotes and include all spaces
git config --global user.signingkey 'COPIED_FROM_CLIPBOARD'
```

### Configure GitHub

In order for GitHub to be able to verify commits, you need to [add SSH public key to GitHub](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)

Add the GPG public key to [GitHub GPG keys](https://github.com/settings/ssh/new): 

- Use title `your@email.com ED25519 Device YYYY-MM-DD OPT_DESCRIPTION (SIGNING KEY)` and 
- ⚠ Key type **MUST BE SET TO** `Signing Key` ⚠


