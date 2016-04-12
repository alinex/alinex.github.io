---
title: Git Code Repository
layout: develop
---

Read more on the following pages:

* TOC
{:toc}


Setup
-------------------------------------------------

### Configure default user

    git config --global user.name alinex
    git config --global user.email info@alinex.de

### Password caching

The next option will tell Git that you don't want to type your username and
password every time your computer talks to GitHub.

To use this option, you need to turn on the credential helper so that Git will
save your password in memory for some time:

    git config --global credential.helper cache

This will keep the password for 15 minutes in memory.
But you can also have Git store your credentials permanently using the following:

    git config --global credential.helper store

Note: While this is convenient, Git will store your credentials in clear text
in a local file (.git-credentials) under your "home" directory


Create a new server repository
-------------------------------------------------

First create a bare repository:

    git --bare init myrepo
    cd myrepo
    git --bare update-server-info
    cd ..
    chown -R www-data:www-data myrepovi

Now make a new local repository:

    git init <path>

After you have everything committed add the remote and push the repository:

    git remote add origin <url>
    git push --all origin
    git push --tags origin

Add the login credentials in the .netrc file which is used by curl:

    $ cat ~/.netrc
    machine git.yourdomain.com
    login reader
    password reader


Moving repository
-------------------------------------------------

First you have to fetch all remote branches:

    git fetch origin

Now check if all branches are local:

    git branch -a

If there are some branches listet as remote which didn't exist as local ones
you have to check them out:

    git checkout -b <name> origin/<name>

Now define a new remote repository:

    git remote add new-origin <url>

Everything set up so you may transfer the repository:

    git push --all new-origin
    git push --tags new-origin

At last you may delete the old origin and rename it:

    git remote rm origin
    git remote rename new-origin origin


Pull/push to origin
-------------------------------------------------

Use the preset names:

    git pull origin master
    git push origin master


Subversion Integration
-------------------------------------------------
If you have a subversion server as master you may also use git for your work and
sync the changes back to subversion as the master repository.

To use this you have to install the extension:

``` bash
apt-get install git-svn
```

To do so you first init your git repository from the subversion master and load
the initial data:

``` bash
git svn clone -s https://github.com/alinex/my-repo
# -s is for --stdlayout which presumes the svn recommended layout for tags, trunk, and branches
```

If you don't want the complete history you may use:
``` bash
git svn clone -s -r 40000:HEAD https://github.com/alinex/my-repo
# -r is for the revision to start taking history from
```

To update your repository to HEAD of subversion master run:

``` bash
git svn rebase
```

And to push your commits further to subversion:

``` bash
git svn dcommit
```
