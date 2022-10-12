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

