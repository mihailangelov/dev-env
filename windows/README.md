# Windows setup

## 1. Install your fresh windows 10

## 2. Run PowerShell as Admin and install Chocolatery package manager for Windows

```
Set-ExecutionPolicy Bypass -Scope Process -Force;

[System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072;

iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
```

## 3. Install various tools for Windows

```
choco install googlechrome
choco install ditto
choco install 7zip
choco install adobe-creative-cloud
choco install irfanview
choco install notepadplusplus
choco install svg-explorer-extension
```

## 4. Enable WSL2

In elevated PowerShell run this commands:

```
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart

dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart

wsl --set-default-version 2
```

## 5. Install Windows Terminal and WSL2

```
choco install microsoft-windows-terminal
choco install wsl-ubuntu-2004
```

Make sure that the Ubuntu is running as WSL2:
```
wsl --list --verbose
```
The output should show "VERSION - 2". If not 2, change it with this command:
```
wsl --set-version Ubuntu-20.04 2
```
After ubuntu is installed, open Windows Terminal and run "Ubuntu 20.04" terminal to configure it.

## 6. Copy settings for Windows Terminal
- Run Windows Terminal and open settings file with "Ctrl+'", locate the file and make a backup.
- Copy and paste from "windows/settings.json" and save the file.
- In **"startingDirectory": "//wsl$/Ubuntu-20.04/home/mihailangelov"** change the **mihailangelov** with your username

## 7. Install nessesary tools

```
sudo apt-get update && sudo apt-get install -y \
    curl \
    ffmpeg \
    git \
    htop \
    pass \
    pwgen \
    python \
    python3-pip \
    ripgrep \
    rsync \
    shellcheck \
    tmux \
    unzip \
    vim
```

## 8. Install ZSH shell and make it default:

```
sudo apt install zsh

chsh -s $(which zsh)
```
Restart Windows Terminal.
Confirm that ZSH is set as your default shell:
```
echo $SHELL
```
It should print `/usr/bin/zsh`

## 9. Install "Oh-My-ZHS" framework

```
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```
Restart your terminal

## 10. Download glyph font for the "Powerlevel10k" and install it:

[DroidSansMono Nerd Font](https://gitlab.com/mihailangelov/dev-env/-/raw/master/p10k_fonts/Droid%20Sans%20Mono%20Nerd%20Font%20Complete.otf)


## 11. Install "Powerlevel10k theme"

```
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
```
You can configure it with this command
```
p10k configure
```
Or use ".p10k.zsh" from the repository bellow

## 12. Clone config files from repository

```
git clone https://gitlab.com/mihailangelov/dev-env ~/dev-env
```

## 13. Install python virtual environments

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
/home/mihailangelov/.local/bin/
```

or here:

```
/usr/local/bin/
```


Add this to your ~/.zprofile file (replace `/home/mihailangelov/.local/bin/` with `/usr/local/bin/` if nessesary):
```
export WORKON_HOME=~/.virtualenvs
export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3
export VIRTUALENVWRAPPER_VIRTUALENV=/home/mihailangelov/.local/bin/virtualenv
source /home/mihailangelov/.local/bin/virtualenvwrapper.sh
```

Or clone ".zprofile_wsl2" from the repository bellow.
<br>
Restart the shell.
<br>
More info here [How To Use Virtual Environments for Python Projects](http://www.patricksoftwareblog.com/how-to-use-virtual-environments-for-python-projects/)

## 14. Copy various config files to your home folder

```
cp ~/dev-env/dotfiles/.zprofile_wsl2 ~/.zprofile
cp ~/dev-env/dotfiles/.zshrc_wsl2 ~/.zshrc
cp ~/dev-env/dotfiles/.tmux.conf ~/.tmux.conf
cp ~/dev-env/dotfiles/.p10k.zsh ~/.p10k.zsh
cp ~/dev-env/dotfiles/.gitconfig ~/.gitconfig
```

## 15. Install TPM (Tmux plugin manager).

```
git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
```
Start a tmux session and install the configured plugins. You would type in
tilda key \` followed by I (capital i) to issue the command.
tmux
`I

## 16. Check to make sure git is configured with your name, email and custom settings.

```
git config --list
```
<br>  

This configuration is inspired by this repository:<br>  
[Nick Janitakis DotFiles](https://github.com/nickjj/dotfiles)