## About

This article will help you install Git and grab a GitHub account.

Even if you have Git installed, it is worth jumping down to [Configuring Git](#configuring-git) to deal with line endings and turn on colours.

## Installing Git

- [Installing Git on Mac OS X](http://help.github.com/mac-git-installation/)
- [Installing Git on Windows](http://help.github.com/win-git-installation/)
- [Installing Git on Linux](http://help.github.com/linux-git-installation/)

<a name="configuring-git"></a>
## Configuring Git

### Generating SSH Keys

A SSH key allows you to authenticate with GitHub, so that you can transfer data between your computer and the GitHub server.

- [Generating a SSH key on Mac OS X](http://help.github.com/mac-key-setup/)
- [Generating a SSH key on Windows](http://help.github.com/msysgit-key-setup/)
- [Generating a SSH key on Linux](http://help.github.com/linux-key-setup/)

### Simplify the SSH Key Passphrases _(Optional)_

If your SSH key has a passphrase, then you will need to enter it every time Git authenticates with your key. If this sounds annoying to you, then you will be interested in this article:

- [Working with SSH Key Passphrases](http://help.github.com/working-with-key-passphrases/)

### Dealing with End of Lines

Incorrect line endings are really annoying.

Cross platform projects need to deal with the different character codes used to terminate a line. Most UNIX and OS X systems use a linefeed (`LF`) character, while Windows uses a carriage-return and linefeed (`CRLF`) to terminate a line.

One problem is that text editors usually use your system's default line ending. Some text editors go as far as updating the whole file to the system's default line ending. The result is that Git may see a single line edit as rewriting the entire file, because the line ending of every line was changed.

We are using `LF` for [PhoneGap Documentation](http://github.com/phonegap/phonegap-docs). If you submit a commit using `CRLF`, then we will sadly reject it and ask you to fix the line endings. So, please configure your Git setup by following this article:

- [Configuring Git to Deal with Line Endings](http://help.github.com/dealing-with-lineendings/)

### Dealing with Filemodes _(Windows-only, Optional)_

On Windows, your repository may report modified files that are only filemodes differences.

For example:

    $ git status
        modified: one/file.md
        modified: another/file.md
    $ git diff
        diff --git a/one/file.md b/one/file.md 
        old mode 10755
        new mode 10644

The solution is to disable filemode on your current Git repository. You should also disable filemode globally, so that future projects do not have this problem.

    git config core.filemode false
    git config --global core.filemode false

### Adding Colour to Git

Colours are nice and easy to setup with the following command:

    git config --global color.ui true

Now you will have terminal colours for all Git commands.

## GitHub Setup

- [Create a Free Account](http://www.github.com/)
- [Associate your GitHub Account with your Git Install](http://help.github.com/git-email-settings/)

## Learn Git

- [GitRef](http://gitref.org/): By GitHub. A great way to be introduced to Git.
- [GitHub Help Pages](http://help.github.com/): A bunch of simple Git configuring and contributing principles.
- [Pro Git](http://progit.org/book/): More advanced Git explained with lots of nice graphs.