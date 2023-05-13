# System setup

## mac os terminal themes:

https://github.com/lysyi3m/macos-terminal-themes

clone the repo and open themes.

## Fonts

We're using [nerd fonts](https://www.nerdfonts.com/font-downloads)

You can easily download one and install it. Ubuntu mono can be a good option if you're familiar with ubuntu.


Now you can review the settings of your termianl and set the theme, font, and other settings.

## zsh

### oh-my-zsh

#### theme

oh-my-zsh with powerlevel10k theme.

Install it following the steps in its website, and then replace the value of `ZSH_THEME` you can find ìn the `.zshrc´ file:

```
ZSH_THEME="powerlevel10k/powerlevel10k"
```

Restart your terminal or type:

```zsh
source ~/.zshrc
```

to run the configuration guide: `p10k configure`


#### plugins

Syntax highlighting and autosuggestions are interesting plugins.

## SSH keys

Now that your terminal looks pretty, its time to set up some useful things. Let's start with ssh keys.

### 1. Generate a new ssh-key (for github, for example)

On macOS, look at 2.1. before generate the keys.

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

Don't forget to enter a passpharse ;)

### 2. Add the SSH keys to the ssh-agent

Check if your ssh-agent is working:

```bash
ssh-agent
```

#### 2.1. macOS agent config

To add keys automatically to the agent and store passphrases in the keychain, we need to configure it. Just add this config to the ssh config file (`~/.ssh/config`):

```bash
Host github.com
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_ed25519
```

And now we can add the key to the agent:

```zsh
ssh-add --apple-use-keychain ~/.ssh/id_ed25519
````

or 

```zsh
ssh-add -K ~/.ssh/id_ed25519
```

**Note:** The `--apple-use-keychain` option stores the passphrase in your keychain for you when you add an SSH key to the ssh-agent.

### 3. Set up your keys in remote servers.

For example, for github: https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account

Click [here](https://docs.github.com/en/authentication/connecting-to-github-with-ssh) for more details.


## GPG Keys

[Source](https://docs.github.com/en/authentication/managing-commit-signature-verification/checking-for-existing-gpg-keys)

Check you have GnuPG installed:

```bash
gpg version
```

List the existing keys

```bash
gpg --list-secret-keys --keyid-format=long
```

### 1. Create your key

```bash
gpg --full-generate-key
```

Again, don't forget the passphrase!

### 2. Set your key

```bash
gpg --list-secret-keys --keyid-format=long
```

From the list of GPG keys, copy the long form of the GPG key ID you'd like to use. In this example, the GPG key ID is `3AA5C34371567BD2`:

```bash
$ gpg --list-secret-keys --keyid-format=long
~/.gnupg/secring.gpg
------------------------------------
sec   4096R/3AA5C34371567BD2 2016-03-10 [expires: 2017-03-10]
ssb   4096R/4BB6D45482678BE3 2016-03-10
```

Paste the text below, substituting in the GPG key ID you'd like to use. In this example, the GPG key ID is `3AA5C34371567BD2`:

```bash
$ gpg --armor --export 3AA5C34371567BD2
# Prints the GPG key ID, in ASCII armor format
```

3. Add your GPG Key to github

 [Online guide](https://docs.github.com/en/authentication/managing-commit-signature-verification/adding-a-gpg-key-to-your-github-account)


4. Set up your git config to sign commits


```bash
git config --global user.name "<Your Name>".
git config --global user.email "<your email>"
git config --global user.signingkey 3AA5C34371567BD2
```

Now you can sign commits with the `-S` flag. However, git can automatically sign all your commits:

```bash
git config --global commit.gpgsign true
```

Check that everything went fine:

```bash
git config --list
```

## VSCode

### Basic config

#### code command

Install vscode as usual. Once you have it, open it, Ctrl++Shift+P and look for the shell command installation, to open it from terminal.

### Dev containers

#### 0. Requirements

Install Docker and dev containers extension

#### 1. Check installation

There are several ways to test if it is working (sample repos, open a repository o PR, etc). However, in this repo we include a `.devcontainer` folder with the required filest to run a dev container ;)

In you want to sign commits, you must ensure that git and gpg are available within the container. The dev-container extension will manage your keys, making them available inside the container. To validate this, just open a new terminal attached to the container and type:

```bash
git config --list
gpg --list-secret-keys --keyid-format=long
```

#### 2. VS Extension

Common extensions, like themes, can be installed on your local vscode. However, the most convinient way to deal with specific extensiones (linters, spell checkers, etc), is installing them in the container. Yo can declare this in the `devcontainer.json`.

