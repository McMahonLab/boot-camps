[Up To Schedule](../../../README.md)

# Mobility: Using Version Control at Work and Home

**Based on material by Matt Gidden**

## Overview

One of the powerful ways to use version control is to maintain your workflow
between the office, home, and wherever else you find yourself being
productive. This type of workflow can be used extensively with both research
work (i.e., coding project collaboration) and thesis writing (i.e., "personal"
activities).

The workflow in this section describes three repository locations - a server, a
work computer, and a home (laptop) computer. The server will host the "base"
repository, and the server can live anywhere you have a connection to. For
example, you could use your GitHub repository (described in the
[Make Changes from Anywhere (GitHub)](../github/Readme.md) section) as the server. If
you have access to a server on campus (e.g., server.uni.edu), you can host your
repository there (and it's private!).

For the purposes of this exercise, all of the repositories will be represented
by different folders in order to provide you with the "flavor" of how such a
workflow would work. For example, we'll use ~/work to represent your work
station. You should assume that ~/work is effectively your work station's home
directory.

## Exercise: Adding a Report to Simplestats

You've been working on your stats module for a while, and you'd like to add a
report to it. You've heard about [Latex](http://www.latex-project.org/) and that
it works really well with version control systems, so you wanted to try it
out. You're spending your time writing, so you'd like to be able to move between
work, some coffee shops, and home.

Aside:  Markdown (what this document was written in) also works very well with
version control software and is easier to read/learn than Latex.  Sarah is
moving to writing all of her documentation in Markdown.  Ask her for some examples
and talk to her about it if you are interested.

Let's start by making a laptop and work directory.

    $ cd
    $ mkdir work
    $ mkdir laptop

### Setting Up the "Work" Repository

Let's clone our simplestats repo to our "work computer". You'll find the repository is named
properly.

    $ cd ~/work
    $ git clone https://github.com/YOU/simplestats.git
    $ ls
    simplestats

Go ahead and ```cd``` into simplestats and look around at the files. Also, take a
gander at that remote.

    $ cd simplestats
    $ ls -a
    .  ..  .git  README.md  stats.py  test_stats.py
    $ git remote -v
    origin  https://github.com/YOU/simplestats.git (fetch)
    origin  https://github.com/YOU/simplestats.git (push)

Let's do some work in a branch.

    $ git branch report
    $ git checkout report

Pro-tip:  You could also create a branch and check it out with one command `git checkout -b report`.


Go ahead an add a file and commit it.

    $ touch report.tex
    $ git add report.tex
    $ git commit -m "added the base tex file for my report"
    $ git push origin report

Note that if you're working on your own repository's master branch, that last
command would look like ```git push origin master```.

### Setting Up the "Laptop" Repository

Ok, you've spent a long day at work. Maybe you still have a little more to do,
but you'd really rather go home and cook dinner first. Let's set up that "laptop
repository" so you can pick up exactly where you left off.

    $ cd ~/laptop
    $ git clone https://github.com/YOU/simplestats.git
    $ ls
    simplestats

Let's investigate what's inside.

    $ cd simplestats
    $ git checkout report
    $ ls -a
    .  ..  .git  README.md  report.tex stats.py  test_stats.py

Ok, awesome, we were able to checkout the updated version of the repository.

Let's try making one set of changes. We'll add some content to the report

    $ echo "this is one fancy report" >> report.tex
    $ git add report.tex
    $ git commit -m "added some content to the report"
    $ git push origin report

So now the home machine is synced with the repository that's on the
server. Any time you're doing work, as long as you **commit and push** the work
you're doing, it will be available to you anywhere you have access to the
internet. In fact, you don't even **need** access to the internet. Once your
repository is up to date, you can do all your editing and committing without
being online. Once you have a connection again, you can push your changes.

And now let's update our work machine to also be synced against our github
repository.

    $ cd ~/work/simplestats
    $ git pull origin report
    $ tail report.tex
    this is one fancy report

Work and laptop are synced again!

#### Aside: Version-Control Best Practices

At this point, you're fully set up to work in a best-practice, version-control
work flow. Experience shows that it's best to work in branches (i.e., other than
master) to make sure the master branch stays up-to-date with your server's
(origin's) master branch. This stuff may not be intuitive when you're first
starting out, though, so just play around and get used to the general work flow
for now. You'll get better at it over time.

#### Aside: Using Server as Remote Host
If you want to use a university server as your repository host, you'll have to go
[through these steps](git_server.md).

----

[Up To Schedule](../../../README.md#schedule) - Back To [Make Changes from Anywhere (GitHub)](../github/Readme.md) - Forward To [Collaborate](../collaborate/Readme.md)
