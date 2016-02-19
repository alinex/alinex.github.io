Installation
=========================================


Installation of node.js and npm
-----------------------------------------

You may install node from your repository on any system or with USE the following
manual steps. The repository mostly has a very old version in debian.

### Linux systems

Here you find a good documentation under (NodeSource)[https://github.com/nodesource/distributions].
This will help you to install on an productive system.

For development systems better use NVM to easily switch between versions. With NVM,
everything is kept in your home folder (so no need for sudo), and you can install
multiple versions of Node (including 4.0) and switch between them with ease.

Like documented on the (NVM Site)[https://github.com/creationix/nvm#installation]:

``` bash
sudo apt-get install -y curl
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.29.0/install.sh | bash
```

Tell your shell to use nvm (if not already added):
``` bash
echo "source ~/.nvm/nvm.sh" >> ~/.bashrc
```

Now you may install the latest node version:

``` bash
nvm install 4.2
```

And tell nvm which version of Node you want to use in your session if you want to change:

``` bash
nvm use 4.2 # specific version
nvm use system # back to default installed node
```

You may also want to add this line also to ~/.bashrc, so that you don't have to
pick a node version each time you start your terminal.


Developmnet helpers
-----------------------------------------

For development please install some global modules like below:

``` bash
sudo apt-get install -y python-virtualenv
sudo easy_install Pygments
```

And to make work with git easy:

``` bash
git config --global user.name Alinex
git config --global user.email info@alinex.de
```

The same goes for npm:

``` bash
npm adduser
# you will be  required to give your user information
```


Alinex Applications
-----------------------------------------

To install the alinex applications you can now simply call npm:

``` bash
sudo npm install -g alinex-... --production
```

See [npm](npm.md) for more help to use the package manager.

### Daemon

You may use the forever productive system to run as daemon.

``` bash
sudo npm install -g forever
```
