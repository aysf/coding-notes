# Linux Coding Notes

## Setting BunsenLabs (Debian 10)

BunsenLabs Linux is a distribution offering a light-weight and easily customizable Openbox desktop.

### Setting menu

go to `menu` > `Preferences` > `jgmenu` > `Edit Menu Content`

in the last of line in file `prepend.csv`, add the following lines 

```csv
^tag(apps)
Back,^back()
Chromium, /snap/bin/chromium
Postman, postman
Code, /snap/bin/code
MySql-Workbench, /snap/bin/mysql-workbench-community
```

## Installing fundamental software in Debian 10

- git
- vscode (snap)
- docker (snap)
- chromium (snap)
- postman

### git installation

```sh
sudo apt update
sudo apt install git
```

## Installing Go in Debian 10

execute these following lines on the terminal

```bash

# preparation
sudo apt update
sudo apt install curl

# choose version
version=1.17.4

# download go
curl -O https://dl.google.com/go/go$version.linux-amd64.tar.gz

# extract tarball
tar xfv go$version.linux-amd64.tar.gz

# Recursively change the owner and group of this directory into root and move to /usr/local
sudo chown -R root:root ./go
sudo mv go /usr/local

# setting path
nano ~/.bashrc

# add the folling lines to .bashrc and save it
GOPATH=$HOME/work
PATH=$PATH:/usr/local/go/bin:$GOPATH/bin

# refresh by running
source ~/.bashrc

# testing
go version

```

alternatively, put the lines to file, say `installer.sh`, set the execute permission using `chmod +x` and run the script using `./installer.sh` or `bash installer.sh` or `sh installer.sh`

reference : https://www.digitalocean.com/community/tutorials/how-to-install-go-on-debian-10