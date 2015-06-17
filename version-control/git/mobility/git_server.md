## Setting Up a "Base" Repository

If you want to use GitHub as your repository host, you can safely skip this. If
you want to use a university server as your repository host, you'll have to go
through these steps.

We'll start off in the home directory and create a bare repository in a new
directory.

    $ mkdir server
    $ cd ~/server
    $ git init --bare myrepo.git

You'll see a new directory in ~/server named myrepo.git. If you ```cd``` into
myrepo.git and give an ```ls``` command, you'll see the contents of the .git
directory you saw earlier in the [Use Version Control](../local/Readme.md)
section.

    $ cd myrepo.git
    $ ls
    branches  config  description  HEAD  hooks  info  objects  refs

This is git's way of storing your repository's information. You shouldn't touch
this, and you can safely ignore it.

## Bare Repositories

A bare repository is meant to simply **store** your files. It actually stores
the contents of the .git directory that you see in all normal repositories. It's
generally not meant to be touched by a human's hands, and is designed to
communicate through git with other non-bare repositories. In fact, when you
initialize a new repository on GitHub, GitHub's version is a bare repository.

Why use a bare repository? The answer is that non-bare repositories don't always
play nice together, and it turns out it helps to have a single, base repository
that's "always right". You can get a more detailed answer
[here](http://www.gitguys.com/topics/shared-repositories-should-be-bare-repositories/).

## More than One Way to Clone

If the repository is served on an external (e.g., university)
server, you'll likely have to use git's ssh cloning
protocol. [Here](http://git-scm.com/book/en/Git-on-the-Server-The-Protocols#The-SSH-Protocol)'s
a great, short explanation of how to do that. GitHub's cloning protocol is
pretty simple, and described on the [Fork help
page](https://help.github.com/articles/fork-a-repo#step-2-clone-your-fork).
