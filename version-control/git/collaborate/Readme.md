[Up To Schedule](../../../README.md) - Back To [Working with Github](../github/Readme.md)

# Collaboration : An exercise in GitHub and Testing
----

**Based on material by Katy Huff, Anthony Scopatz, Sri Hari Krishna
Narayanan, and Matt Gidden**

This section will outline an exercise to get your feet wet in using some of
GitHub's features. We'll be continuing our work on testing as an example.

For the rest of this section, I'll assume that there are two collaborators,
Alpha and Beta.

Let's start off by relocating back to the original simplestats repository.

    $ cd ~/simplestats

In our lab, all projects have an upstream repository which serves to coordinate
the efforts of everyone working on the project. Individual lab members have
their own forks which they periodically incorporate into the upstream repo.

In today's tutorial, alpha and beta will both be working to implement a stats
function. Like good SWC followers, we'll be working in a branch, called
`median`, which I will now create. Once I have, update your local copies and
remotes:

    $ git checkout -b median upstream/median
    $ git push origin median

## Group up

Group up in pairs and decide who will be "Alpha" and who will
be "Beta" for this exercise.  


## Pull Requests : Sending Your Collaborators an Update

From GitHub's [website](https://help.github.com/articles/using-pull-requests), a
pull request

> lets you tell others about changes you've pushed to a GitHub repository. Once
a pull request is sent, interested parties can review the set of changes,
discuss potential modifications, and even push follow-up commits if necessary.

### Exercise : Issue a Pull Request and Review it

In this exercise, "Beta" will be making changes and submitting a pull request
to the upstream repository, and "Alpha" will be reviewing the pull request and
merging it into the upstream repository, and then their own local (and remote)
repositories. In the following instructions Beta will be performing Steps 1-4
(while Alpha waits and observes), and then Alpha will continue with Steps 5-7
(while Beta observes).  

#### For Beta (submitting the pull request)

**Step 1** : Create a stats_alpha_beta.py module to add the median function (shown below), where alpha and beta are the initials of the participants.

```python
def median(vals):
    vals.sort()
    z = len(vals)
    index = z / 2
    if z % 2 == 0:
       return mean([vals[index], vals[index - 1]])
```

**Step 2** : Commit your changes

    $ git add stats.py
    $ git commit -m "I added a median function."

**Step 3** : Update your remote

    $ git push origin median

**Step 4** : Issue a Pull Request to the upstream `median` branch

  - Go to your remote's page (github.com/beta/simplestats)
  - Click Pull Requests (on the right menu) -> New Pull Request -> Edit
  - choose the base fork as **upstream/simplestats**, the base branch as **median**, the
    head fork as **beta/simplestats**, and the compare branch as **median**
  - write a descriptive message and send it off.

#### For Alpha (after Beta has finished and submitted the pull request)

**Step 5** : Review the pull request

  - Go to the upstream page (https://github.com/McMahonLab/simplestats)
  - Click Pull Requests (on the right menu
  - Click on beta's pull request

  - Is the code clear? Does it need comments? Is it correct? Does something
    need clarifying? Feel free to provide in-line comments. Beta can always
    update their version of commits during a pull request.

**Step 6** : Merge the pull request using the merge button

**Step 7** : Update your local and remote repositories.  At this point, all the changes exist
**only** on the upstream repository.

    $ git checkout median
    $ git fetch origin
    $ git merge upstrem/median
    $ git push origin median

### Exercise : Swap Roles

Ok, so we've successfully issued a pull request and merged the updated code
base. Let's swap the roles of pull requester and reviewer. This time, Alpha will
add some additional code to the median function, submit a pull request and Beta will
review the pull request.  Alpha will follow steps 1-4, and Beta will wait
until they finish, then follow steps 5-7.  

####For Alpha (submitting the pull request):

**Step 1** : Modify the stats_alpha_beta.py median function so the code is the following.

```python
def median(vals):
    vals.sort()
    z = len(vals)
    index = z / 2
    if z % 2 == 0:
       return mean([vals[index], vals[index - 1]])
    else:
       return vals[index]
```

**Step 2** : Commit your changes

    $ git add stats.py
    $ git commit -m "I added else statment to the median function."

**Step 3** : Update your remote

    $ git push origin median

**Step 4** : Issue a Pull Request

  - Go to your remote's page (github.com/alpha/simplestats)
  - Click Pull Requests (on the right menu) -> New Pull Request -> Edit
  - choose the base fork as **upstream/simplestats**, the base as **median**, the
    head fork as **alpha/simplestats**, and the compare as **median**
  - write a descriptive message and send it off.

####For Beta (after Alpha has finished and submitted the pull request)

**Step 5** : Review the pull request

  - Go to the upstream page (https://github.com/McMahonLab/simplestats)
  - Click Pull Requests (on the right menu
  - Click on alpha's pull request

  - Is the code clear? Does it need comments? Is it correct? Does something
    need clarifying? Feel free to provide in-line comments. Alpha can always
    update their version of commits during a pull request.

**Step 6** : Merge the pull request using the merge button

**Step 7** : Update your local and remote repositories.  At this point, all the changes exist
**only** on the upstream repository.

    $ git checkout median
    $ git fetch origin
    $ git merge upstrem/median
    $ git push origin median

## git merge : Conflicts

This is the trickiest part of version control, so let's take it very carefully.

Alpha and Beta have made changes to that file in sync with each other. What
happens if someone else makes changes on the same lines? A dreaded conflict...

Now, I will assume the role of PI.  Instead of waiting around for my grad
students to finish their work, let's say that I decided to take my own stab at
the median function. I'll add something to stats_alpha_beta.py and
push it to the upstream repository. Sadly, this addition overlaps with your
recent median addition. **Note**: If all of the pairs had created a `stats.py`
file, conflicts would also have appeared.

### Exercise : Experience a Conflict

**Step 1** : Experience the Conflict

    $ git fetch upstream
    $ git merge upstream/median
    remote: Counting objects: 2, done.
    remote: Total 2 (delta 0), reused 0 (delta 0)
    Unpacking objects: 100% (2/2), done.
    From git@github.com:UW-Madison-ACI
    d063879..90fbb5e  median     -> upstream/median
    Auto-merging stats_alpha_beta.py
    CONFLICT (content): Merge conflict in stats_alpha_beta.py
    Automatic merge failed; fix conflicts and then commit the result.

## Resolving Conflicts

Now what?

Git has paused the merge. You can see this with the ``git status`` command.

    On branch median
    Your branch and 'upstream/median' have diverged,
    and have 1 and 1 different commit each, respectively.
    (use "git pull" to merge the remote branch into yours)

    You have unmerged paths.
    (fix conflicts and run "git commit")

    Unmerged paths:
    (use "git add <file>..." to mark resolution)

    both modified:      stats_alpha_beta.py

If you open your stats_alpha_beta.py file, you'll notice that git has added some strange
characters to it. Specifically, you'll see something like:

    <<<<<<< HEAD:stats_alpha_beta.py
    ** your version of the code **
    =======
    ** upstream's version of the code **
    >>>>>>> upstream:stats.py

Now, your job is to determine how the code *should* look. For this example, that
means you should replace the PI's ```median``` function with yours.

### Exercise : Resolve a Conflict

**Step 1** : Resolve the conflict by editing your stats_alpha_beta.py file. It should
run as expected and should look exactly like your version, but with the
PI's changes included.

**Step 2** : Add the updated version and commit

    $ git add stats_alpha_beta.py
    $ git commit -m "Updated from PI's commit"
    $ git push origin median

## Issues and Milestones

Let's take a look at Issues and Milestones, both of which are great project
planning tools.

----

[Up To Schedule](../../../README.md) - Back To [Working with Github](../github/Readme.md)
