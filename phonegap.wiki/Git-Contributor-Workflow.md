# Git Contribution Workflow

Now that you have Forked the PhoneGap Documentation, you can starting making some changes.

## Topic Branch

A good habit to get into is using topic branches for your work, while keeping the master branch untouched. You can then keep the master branch up-to-date with the main repository without worrying about merge conflicts.

### Reduce Merge Conflicts

By not working on the master branch, you ensure that the branch's history will not diverge from the main repository's master branch. This allows you to pull in updates from the main repository (apache/incubator-cordova-docs) without merge conflicts.

### Organize and Isolate Contributes

By creating a topic branch for each contribution, you effectively isolate your changes into a single branch of history. As long as the topic branch is up-to-date, your changes will merge cleanly into the main repository. If your contributions cannot be merged cleanly, the repository maintainer may have to reject your contribution until you update it.

### Easier for the Maitainer

Maintainers like topic branches. It is easier to review the pull request and merge the commit into the main repository

## Git Workflow 

Consider that you've decided to work on JIRA ticket #11, which is testing the iOS implementation of `accelerometer.watchPosition`.

### Update the master branch

    $ git checkout master
    $ git pull apache master
    $ git push origin master

First, you want to checkout your master branch and update it with apache/incubator-cordova-docs latest changes.

### Create a topic branch

    $ git checkout master
    $ git checkout -b ticket_11
    $ git branch
        master
      * ticket_11

Now, create a topic branch named `ticket_11` from master for ticket #11.

You can name the topic branch anything, but it makes sense to name it after the ticket. This topic branch is now isolated and branched off the history of your master branch.

### Make File Changes

    $ [ edit accelerometer/watchPosition.md ]
    $ git status
      modified: accelerometer/watchPostion.md 

git status shows that you have modified one file.

### Commit the File Changes

    $ git add accelerometer/watchPosition.md
    $ git status
    $ git commit -m "[#11] Add iOS as supported for accelerometer.watchPosition."

git add will stage the file changes. You can then commit the staged file(s) with git commit.

Alternatively, you could skip git add and use `git commit -am "...."` 

### Commit More File Changes

    $ [ edit accelerometer/watchPosition.md ]
    $ git commit -am "[#11] Fix syntax error watchPosition example." 

### Prepare to Send Pull Request

    $ git checkout master
    $ git pull apache master
    $ git checkout ticket_11
    $ git rebase master

Before sending the pull request, you should ensure that your changes merge cleanly with the main repository apache/incubator-cordova-docs.

You can do this by pulling the latest changes from the main repository and rebasing the history of the master branch onto the topic branch ticket_11. Essentially, this will fast-forward your topic branch to the latest commit of the master.

Alternatively, you can use `git merge master` instead of `git rebase master`, but your topic branches history may not be as clean.

### Share your Changes on GitHub

    $ git checkout ticket_11
    $ git push origin ticket_11

By pushing your topic branch onto your GitHub fork, a apache/incubator-cordova-docs maintainer can review and merge the topic branch into the main repository.

## Sending a Pull Request from GitHub


Open a web browser to your GitHub account's fork of the incubator-cordova-docs repository.
Select your topic branch so that the pull request references the topic branch.

- Click the Pull Request button.
- Select mwbrooks as the Recipient. 

## While Waiting, Continuing Crafting Commits

Since you worked on the topic branch instead of the master branch, you can continue working while waiting for the pull request to go through.

Be sure to create the topic branch from master.

    $ git checkout master
    $ git pull apache master
    $ git checkout -b fix_ugly_vibrate_example
    $ git branch -a
      * fix_ugly_vibrate_example
        master
        ticket_11

## When your Pull Request is Accepted

    $ git checkout master
    $ git pull apache master
    $ git log 
    ( hey there's me! ya! )

You can now delete your topic branch, because it is now merged into the main repository and in master branch.

    $ git branch -d ticket_11
    $ git push origin :ticket_11

I know, deleting a remote topic branch is ugly (git push origin :ticket_11).

## If your Pull Request is Rejected

In this case, you just need to update your branch from the main repository and then address the rejection reason.

    $ git checkout master
    $ git pull apache master
    $ git checkout ticket_11
    $ git rebase master
    ( edit / commit / edit / commit)
    $ git push origin ticket_11

Once you are ready, resend the pull request from your GitHub account.
