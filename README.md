# Ubuntu Setup on ChromeOS

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
    git config user.name
    git config user.email

    vim ~/.bashrc
    # add: alias s="git status"

    # generate key for github access
    ssh-keygen -t rsa -b 4096
    cat ~/.ssh/id_rsa.pub 
    # add key to github

    # setup and run Atom
    sudo dpkg --install ~/Downloads/atom-amd64.deb 
    sudo apt-get install -f
    xiwi -T atom

    # install latest Go
    sudo apt-get update
    sudo apt-get -y upgrade
    curl -O https://storage.googleapis.com/golang/go1.7.1.linux-amd64.tar.gz
    sudo tar -C /usr/local -xzf go1.7.1.linux-amd64.tar.gz
    vim ~/.profile    # and add /usr/local/go/bin to the PATH
