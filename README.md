# Arch-On-WSL

Here is information on how to install WSL if you need it.
<br/>
https://learn.microsoft.com/en-us/windows/wsl/install
<br/>
If you want a list of valid distributions that can be installed, ```wsl --list --online```
<br/>
Install Arch, ```wsl --install archlinux```
<br/>
After the install is complete you are logged in as the root user. I recommend you create a root password with the passwd command.

### Configure Arch

Update archlinux ```pacman -Syu```
<br/>
make passowrd for Root ```passwd```
<br/>
create a user and password protect it.
<br/>
```useradd -G wheel -m <your-username>```
<br/>
```passwd <your-username>```

Install packages 
<br/>
```
sudo pacman -Sy stow sudo base-devel neovim zsh networkmanager zsh-autosuggestions zsh-syntax-highlighting zsh-autocomplete zsh-history-substring-search zoxide fzf bat trash-cli glibc tcpdump vi git
```

Enable NetworkManager.
<br/>
```systemctl enable --now NetworkManager```

configure the locale settings.
<br/>
Edit ```nvim /etc/locale.gen``` with your favorite editor.
<br/>
Uncomment the locale you want to use, mine is, ```en_US.UTF-8 UTF-8```
<br/>
Run ```locale-gen```

change to root by ```su -```
run ```visudo``` and remove the # from the NOPASSWD line and put a # in front of the other %wheel line. This way you are not prompted for a sudo password.
<br/>
```
##
## User privilege specification
##
root ALL=(ALL:ALL) ALL

## Uncomment to allow members of group wheel to execute any command
## %wheel ALL=(ALL:ALL) ALL

## Same thing without a password
%wheel ALL=(ALL:ALL) NOPASSWD: ALL
```

### The WSL Config
Create /etc/wsl.conf and add this configuration to it.
<br/>
This sets the hostname to archy, tells WSL to not overwrite ```/etc/hostname``` and ```/etc/resolv.conf```. Boot using systemd instead of init. If you want to use specific DNS servers remember to put them in ```/etc/resolv.conf```
<br/>
```
[network]
hostname = archy
generateHosts = false
generateResolvConf = false
[boot]
systemd=true
[user]
default=waso
```

stop the running instance and start it back up again.
<br/>
```wsl --terminate archlinux``` and start it back up again with ```wsl -d archlinux```

### Setup yay

get the yay package.
<br/>
```git clone https://aur.archlinux.org/yay.git```
<br/>
Change into the yay directory, cd yay
<br/>
```makepkg -si yay```
<br/>
On of the packages I install with yay is for example zsh-vi-mode
<br/>
```yay -Sy zsh-vi-mode```
<br/>
Change default shell:
```chsh -s $(which zsh)```
