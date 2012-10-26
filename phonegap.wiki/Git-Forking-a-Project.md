# Git Forking the PhoneGap Documentation

Now that you have [Installed and Configured Git](wiki/Git-Setup), you can now grab your own copy of the PhoneGap Documentation source!

## Fork the Repository

- Open your web browser to http://github.com/apache/incubator-cordova-docs
- Click __Fork__

Since you do not have write access to the apache/incubator-cordova-docs, you need to create a fork of the main repository. A fork is a copy of the apache/incubator-cordova-docs repository that is stored on your public GitHub account. This is your public copy of the repository that you will use to share your code contributions with the incubator-apache-docs maintainers.

## Clone Your Repository Fork

    $ cd ~/development
    $ git clone git@github.com:username/incubator-cordova-docs.git
    $ cd incubator-cordova-docs

Once you have forked apache/incubator-cordova-docs, you will need to download your public repository onto your local computer. You can accomplish this by cloning your public repository.

You will need to replace username with your GitHub username.

## Add the Main Repository

### Add Remote Repository

    $ git remote add apache git://github.com/apache/incubator-cordova-docs.git
    $ git fetch apache

You fork is only loosely linked to the main repository apache/incubator-cordova-docs. It is your responsibility to keep your fork up-to-date.

You will want to stay up-to-date with the main repository so that your contributions can merge cleanly. You can update your local copy by pulling down the changes from the main repository apache/incubator-cordova-docs. This is accomplished by adding apache/incubator-cordova-docs as a remote repository.

The fetch command simply grabs the latest from apache/incubator-cordova-docs without merging it into your working branch. Now we can take another look at our repository and see what's there.

### Verify the Main Repository was Added

    $ git branch -a
    $ * master
    $   remotes/origin/HEAD -> origin/master
    $   remotes/origin/master
    $   remotes/apache/master

`git branch -a` lists all your available branches. There is one local branch named master. There are also two remote master branches - one for your fork origin and one for the main repository apache.

### View the Remote Repositories

    $ git remote -v
    $ origin  git@github.com:mwbrooks/incubator-cordova-docs.git (fetch)
    $ origin  git@github.com:mwbrooks/incubator-cordova-docs.git (push)
    $ apache  git://github.com/apache/incubator-cordova-docs.git (fetch)
    $ apache  git://github.com/apache/incubator-cordova-docs.git (push)

`git remote -v` is a useful command when you forget the name of a remote repository.

## Update Your Repository

    $ git checkout master
    $ git pull apache master
    $ git push origin master

From time-to-time, you will want to get the latest updates from the main repository apache/incubator-cordova-docs. Optionally, you may want to push those updates to your fork, so that your fork is also up-to-date.

To update your repository (in this case, the master branch), first, checkout the master branch.

Next, you will pull down the latest changes from the apache remote. Remember apache points to the main repository apache/incubator-cordova-docs.

Finally, you can optionally push the latest changes to your fork on GitHub. You may not want to push the changes to your fork if you have made commits on master that you are not ready to share.
