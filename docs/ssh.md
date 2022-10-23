
- [SSH](#ssh)
  - [Configure SSH](#configure-ssh)
    - [Restrict permissions on Windows](#restrict-permissions-on-windows)
    - [Update ssh config](#update-ssh-config)
  - [Start `ssh-agent` Service (Windows only)](#start-ssh-agent-service-windows-only)
  - [Generate a new SSH key](#generate-a-new-ssh-key)

# SSH

## Configure SSH
```bash
# Create .ssh folder if it doesn't already exist
mkdir -p ~/.ssh

# Backup existing ssh config file if it exists, just in case
mv ~/.ssh/config ~/.ssh/config.bak

# Copy ssh config
cp ./HOME/.ssh/config ~/.ssh/config

# Restrict access / set permissions (Mac & Linux only; for Windows, see below)
chmod 700 ~/.ssh
chmod 600 ~/.ssh/config
```

### Restrict permissions on Windows

On Windows, find the `.ssh` folder in Explorer, right-click > `Properties` > `Security` tab > click `Advanced` > click `Disable inheritance`. Then remove all Administrator users other than yourself from the `Permission entries` table. See more details on [Stack Overflow](https://stackoverflow.com/a/58275268/192331).

### Update ssh config

Replace `Firstname.Lastname` in the [`~/.ssh/config`](~/.ssh/config) file with real name:

```bash
# Replace with real name
User Firstname.Lastname
```

On Windows and Linux, remove (or comment out) the following line in the [`~/.ssh/config`](~/.ssh/config) file:

```bash
# Mac only (remove/comment out on Linux & Windows)
UseKeychain yes
```

## Start `ssh-agent` Service (Windows only)

To run the `ssh-agent` service automatically on computer startup, run PowerShell as Administrator, and execute the following command:

```bash
# Automatically start ssh-agent on computer startup
Get-Service ssh-agent | Set-Service -StartupType Automatic -PassThru | Start-Service

# Manually start the ssh-agent for the first time
start-ssh-agent.cmd
```

> *See the following [guide for more info](https://interworks.com/blog/2021/09/15/setting-up-ssh-agent-in-windows-for-passwordless-git-authentication/)*


## Generate a new SSH key

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

# Ubuntu & Windows
ssh-add ~/.ssh/id_ed25519
```

> *Next, continue to [`git`, GitHub and GPG Signing setup guide](./git.md)*