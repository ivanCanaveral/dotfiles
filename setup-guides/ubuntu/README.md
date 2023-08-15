# Ubuntu

## 1. Update :)

```bash
sudo apt update
```

### 1.1. Snap

```bash
sudo snap install htop
```

## 2. zsh

```
sudo apt install zsh
```

Check the installation with:

```bash
zsh --version
```

Installing ZSH will not modify and set it as the default shell. We have to modify the settings to make ZSH our default shell. Use the “chsh” command with '-s' flag to switch the default shell for the user.

```bash
echo $SHELL
> /bin/bash

chsh -s $(which zsh)
```

Compared to other shells like BASH, ZSH requires some first-time configuration to be taken care of. When you start ZSH for the first time it will throw you some options to configure. Let’s see what those options are and how to configure those options.

Select option `1` on the first page which will take us to the main menu, and configure your zsh shell.

Once you are on the “History Configuration page” you can simply type "1" or "2" or "3" to change the associated configuration. Once you make the changing status will be changed from “not yet saved” to “set but not saved”.

Press "0" to remember the changes. Once you come out to the main menu status will change from “recommended” to “Unsaved changes“.

Similarly, you have to modify the configuration for the completion system, keys, and common shell options. Once done press “0” to save all the changes.

You can run the new-user install command again:

```bash
autoload -Uz zsh-newuser-install
zsh-newuser-install -f
```

This process generates a `.zshrc` file you can modify. You can always skip this first setup process, generate a file with the defaults and modify the settings later file you can modify. You can always skip this first setup process, generate a file with the defaults and modify the settings later.

