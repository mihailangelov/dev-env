# MacOS setup

## 1. Install your MacOS

## 2. Clone config files from repository

```
git clone https://gitlab.com/mihailangelov/dev-env ~/dev-env
```


## 3. Install HomeBrew from Terminal

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

## 4. If on Mac Silicon make sure homebrew is ARM64 version

Edit your ~/.zshrc or ~/.bashrc with at the end of file :
```
export PATH=/opt/homebrew/bin:$PATH
```
After this, tap source ~/.zshrc in your terminal or restart it.

## 5. Install nessesary tools

```
brew install \
    curl \
    ffmpeg \
    git \
    htop \
    pass \
    pwgen \
    python \
    ripgrep \
    rsync \
    tmux \
    unzip \
    vim \
    qlmarkdown
```
**qlmarkdown** will quick preview .MD in the Finder, this extension need to be enabled in the FireVault and force restart finder:
```
defaults write com.apple.finder QLEnableTextSelection -bool TRUE; killall Finder
```

## 6. Install python virtual environments

Create a folder that will contain all your virtual environments:
```
mkdir ~/.virtualenvs
```

Install “virtualenv” and “virtualenvwrapper” packages:
```
pip3 install virtualenv

pip3 install virtualenvwrapper
```

This two packages will be installed here:

```
/usr/local/bin/
```

or here:

```
/home/mihailangelov/.local/bin/
```


Add this to your ~/.zprofile file (replace  `/usr/local/bin/` with `/home/mihailangelov/.local/bin/` if nessesary):
```
export WORKON_HOME=~/.virtualenvs
export VIRTUALENVWRAPPER_PYTHON=/usr/local/bin/python3
export VIRTUALENVWRAPPER_VIRTUALENV=/usr/local/bin/virtualenv
source /usr/local/bin/virtualenvwrapper.sh
```

Or clone ".zprofile_macos" from the repository bellow.
<br>
Restart the shell.
<br>
More info here [How To Use Virtual Environments for Python Projects](http://www.patricksoftwareblog.com/how-to-use-virtual-environments-for-python-projects/)


## 7. Install "Oh-My-ZHS" framework

```
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```
Restart your terminal

## 8. Download nessesary glyph fonts for the "Powerlevel10k" and install them
```
git https://gitlab.com/mihailangelov/dev-env/p10k_fonts ~/p10k_fonts
```
After installing the fonts, open Terminal > Preferencies and change the font to "MesloLGS NF" with size of 14, character spacing 1.0004. You have to do this for every profile you will use with p10k.

## 9. Install "Powerlevel10k theme"

```
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
```
You can configure it with this command
```
p10k configure
```
Or use ".p10k.zsh" from the repository bellow

## 10. Copy various config files to your home folder

```
cp ~/dev-env/dotfiles/.zprofile_macos ~/.zprofile
cp ~/dev-env/dotfiles/.zshrc_macos ~/.zshrc
cp ~/dev-env/dotfiles/.tmux.conf ~/.tmux.conf
cp ~/dev-env/dotfiles/.p10k.zsh ~/.p10k.zsh
cp ~/dev-env/dotfiles/.gitconfig ~/.gitconfig
```

## 11. Install TPM (Tmux plugin manager).

```
git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
```
Start a tmux session and install the configured plugins. You would type in
tilda key \` followed by I (capital i) to issue the command.
tmux
`I

## 12. Check to make sure git is configured with your name, email and custom settings.

```
git config --list
```
<br>  

This configuration is inspired by this repository:<br>  
[Nick Janitakis DotFiles](https://github.com/nickjj/dotfiles)