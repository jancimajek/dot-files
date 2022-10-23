
- [Starship 🚀](#starship-)
  - [Powershell](#powershell)
- [Scoop](#scoop)


# Starship 🚀

- Install [Nerd fonts](https://www.nerdfonts.com/)
- Install [Starship](https://starship.rs/#install-latest-version)


## Powershell

> *For configuring Starship for zsh, see [zsh guide](./zsh.md#starship-🚀)*

Download and install [the MSI Installer](https://github.com/starship/starship/releases/latest)

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


# Scoop

> *Just don't bother, you'll waste just time and effort, age 5 years and it won't work at the end anyway. Use MSI installers where possible instead*

Install [scoop package manager for Windows](https://scoop.sh/)

```bash
# Optional: Needed to run a remote script the first time
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser

# Install scoop
iwr -useb get.scoop.sh | iex
```


