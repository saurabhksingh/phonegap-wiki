# Git Commit Message Format

Most of this article is paraphrased from [Pro Git: Chapter 5.2](http://progit.org/book/ch5-2.html#commit_guidelines).

## Formatting a Commit Message

There are a few basic rules that makes Git commit messages more readable on the terminal and GitHub.

The most important rule is use the first line as a summary and to keep it short.

### Message Format

    Short (50 chars or less) summary of changes

    More detailed explanatory text, if necessary.  Wrap it to about 72
    characters or so.  In some contexts, the first line is treated as the
    subject of an email and the rest of the text as the body.  The blank
    line separating the summary from the body is critical (unless you omit
    the body entirely); tools like rebase can get confused if you run the
    two together.

    Further paragraphs come after blank lines.

    - Bullet points are okay, too

    - Typically a hyphen or asterisk is used for the bullet, preceded by a
      single space, with blank lines in between, but conventions vary here

## Help from Syntax Highlighting

GIT installs a VIM commit message highlighter that is very handy when crafting commit messages. It should just work, there is no configuration.

## Wording Style

It is good idea to use the imperative present tense in the summary message. Think of it as telling it what to do.

### Good Example (Assertive)

Add tests for accelerometer.

### Bad Examples (Wimpy)

I added some test to accelerometer.

Added tests to accelerometer.

### Why use Imperative Present Tense?

Some Git commands like interactive rebasing (git rebase -i) and interactive adding (git add -i) are easier to read when commit messages use a short summary and a present tense voice.
