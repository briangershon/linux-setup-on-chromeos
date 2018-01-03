# Linux Setup on ChromeOS

Tested on Toshiba Chromebook 2 (2015) CB30/CB35 (GANDOF) (Intel Broadwell)

Here are two options:

* Replace ChromeOS with Linux

* Run Ubuntu Shell on ChromeOS via Crouton

I initially went the Crouton route (to support ChromeOS and Linux together) but replaced with Linux
to use additional tools like Docker, and a formal terminal.

# Replacing ChromeOS with Linux

Instructions to boot Linux Mint from USB and replace ChromeOS:

http://www.fascinatingcaptain.com/howto/install-linux-mint-on-a-chromebook-with-a-separate-home-drive/

If your laptop battery drains all the way down, you will lose ability to boot it. These instructions will allow you to set the necessary nvram flag and boot again: https://dev.chromium.org/chromium-os/developer-information-for-chrome-os-devices/workaround-for-battery-discharge-in-dev-mode

# Run Ubuntu via Crouton

## Useful resources

* https://www.linux.com/learn/how-easily-install-ubuntu-chromebook-crouton%20
* https://github.com/dnschneid/crouton/wiki/crouton-in-a-Chromium-OS-window-(xiwi)

## Install Crouton

    # Download Crouton
    sh ~/Downloads/crouton -t list
    sudo sh ~/Downloads/crouton -t core,cli-extra,xiwi,audio,extension

    # if you need to add something else
    sudo sh ~/Downloads/crouton -u -t extension

    # create another chroot with -n
    sudo sh ~/Downloads/crouton -n another -t core,cli-extra,xorg,audio,extension

## Enter chroot

    # Ctrl-Alt-t
    shell
    sudo enter-chroot

## Install Packages

    sudo apt-get update
    sudo apt-get upgrade

    # Install manpages for all existing packages
    sudo apt-get install man
    sudo dpkg -l | grep '^ii ' | sed 's/  */\t/g' |cut -f 2,3 | sed 's/\t/=/' | xargs sudo apt-get install --reinstall -y --ignore-missing

    # Install more tools
    sudo apt-get install tmux vim git

    # Install nvm and node.js
    wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.31.2/install.sh | bash
    command -v nvm
    nvm
    nvm install node
    nvm use node

    # set up a git repo
    git init
    git config --global user.name "<value here>"
    git config --global user.email <value here>

    vim ~/.bashrc
    # add: alias s="git status"

    # generate key for github access
    ssh-keygen -t rsa -b 4096
    cat ~/.ssh/id_rsa.pub
    # add key to github

    # setup and run Atom
    # download atom-amd64.deb from https://github.com/atom/atom/releases
    sudo dpkg --install ~/Downloads/atom-amd64.deb
    xiwi -T atom

    # install latest Go
    sudo apt-get update
    sudo apt-get -y upgrade
    curl -O https://storage.googleapis.com/golang/go1.7.1.linux-amd64.tar.gz
    sudo tar -C /usr/local -xzf go1.7.1.linux-amd64.tar.gz
    vim ~/.bashrc    # and add PATH=/usr/local/go/bin:$PATH

## Copy and Paste betweeen Chrome windows and Terminal windows

Use `shift-ctrl-c` and `shift-ctrl-v` for universal copy/paste in both Chrome and shell windows.

*(`ctrl-c`, `ctrl-v` work inside Chrome, but not in the shell window)*
