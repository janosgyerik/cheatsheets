## Migrating from Subversion

http://git-scm.com/course/svn.html

Print the content of a file at some revision or branch:

    svn cat path/to/file -r REV
    git show REV:path/to/file

Print the diff of a revision:

    svn diff -cREV
    git show REV

Export a project subdirectory:

    svn export PATH /path/to/dir
    git archive master > /path/to/export.tar

Remove file from version control but keep it in the working directory:

    svn rm --keep-local PATH
    git rm --cached PATH

## Getting started

Set username and email that will be recorded in commits:

    git config --global user.name "Your Name"
    git config --global user.email you@your.domain.com
    
Set username and email for particular repo instead of global config
    
    git config user.name "Your Other Name"
    git config user.email "you@your.other.domain.com"
 
Convert any directory to a Git repository:

    git init     # create repo in current dir or specified path
    git add .    # add all files in current dir and all subdirs
    git status
    git commit -m "added project files"

## ~/.gitconfig

An example configuration.
Most importantly, shorter version of commands,
to reduce typing dramatically,
and for familiarity with other systems (`co`, `st`, `ci`, ...)

    [user]
        name = Janos Gyerik
        email = me@my.domain.com

    [alias]
        st = status
        ci = commit
        br = branch
        co = checkout
        ls = ls-files
        ign = ls-files -o -i --exclude-standard
        lol = log --graph --decorate --pretty=oneline --abbrev-commit
        lola = log --graph --decorate --pretty=oneline --abbrev-commit --all

        # View the SHA, description, and history graph of the latest 20 commits
        l = log --pretty=oneline -n 20 --graph
        # View the current working tree status using the short format
        s = status -sb
        # Show verbose output about tags, branches or remotes
        tags = tag -l
        branches = branch -a
        remotes = remote -v

    [url "git@github.com:"]
        insteadOf = "gh:"
        pushInsteadOf = "github:"
        pushInsteadOf = "git://github.com/"

## Specifying recent revisions

    git log HEAD        # the current checkout points to this commit
    git log HEAD^       # previous commit
    git log HEAD^^      # 2 commits ago
    git log HEAD~5      # 5 commits ago
    git log treeish^    # the commit before "treeish": branch / tag / SHA
    git log treeish^^   # 2 commits before treeish
    git log treeish~5   # 5 commits before treeish

In case insensitive filesystems like Windows,
instead of uppercase `HEAD` you can get away with lowercase `head` too.

## Browsing the repository, log, diff, etc

    git log --stat
    git log --name-status
    git log --name-only
 
    git log rev -- path
    git show rev -- path
    git diff rev -- path

## Searching for past commits

    git log --grep keyword

## Working with a Subversion repository in lock-step with upstream

Scenario: simple lock-step model, the rough equivalent of using svn checkout + svn update + svn commit.

    # this will create new local git repo in new dir "projname"
    git svn clone svn://path/to/repo/projname
    # note: this can take a long time
    # note: this can hang in the middle. When that happens,
    # cd into the partial clone, and run `git svn fetch`.
    # That too may hang, just keep repeating `git svn fetch` until success.
 
    # commit changes to local repo
    git commit -m "some work"
    git commit -m "some more work"
    git commit -m "even more work"
 
    # get changes from svn, and rebase local work on top of it
    git svn rebase
 
    # push local changes back to svn, as multiple individual commits
    git svn dcommit

## Working with a Subversion repository and local Git branches

Scenario: same as earlier, but this time use local Git branches

    # create local 'work' branch and switch to it
    git checkout -b work
 
    # work work work...
    git commit -m "some work"
    git commit -m "some more work"
    git commit -m "even more work"

    # switch back to master and get upstream changes from svn
    git checkout master
    git svn rebase
 
    # switch to work, rebase on top of master
    git checkout work
    git rebase master

    # switch back to master, merge from work, and push back to svn
    git checkout master
    git merge work
    git svn dcommit

## Working on a Subversion branch

    # add the url of the branch, and give it a "refname"
    git config --add svn-remote.newbranchname.url https://svn/path_to_newbranch/
    git config --add svn-remote.newbranchname.fetch :refs/remotes/newbranchname

    # fetch the branch
    git svn fetch newbranchname [-r<rev>]

    # create a local branch from the remote reference
    git checkout -b local-newbranchname -t newbranchname

    # update the local branch from the remote reference
    git svn rebase newbranchname

    # push the new revisions to subversion
    git svn dcommit --dry-run
    git svn dcommit

## Restoring a deleted directory from an old revision

If you know the path you want to restore, find the SHA where it was deleted:

    git log -- path/to/deleted/dir

Bring back the deleted directory from the revision before the one which deleted it:

   git checkout SHA^ -- path/to/deleted/dir

The above command will create the specified path in the working tree
and add it to the staging area. If you want to unstage:

    git reset -- path/to/deleted/dir

## How to start a local repository and push it to a server later

    cd /path/to/your/new/project
    git init
    git add .
    git commit -m 'first commit, added all files'
    ssh username@server git init --bare path/to/repos/git/project.git
    git remote add origin username@server:path/to/repos/git/project.git
    git push origin master

## How to push a git repo to svn for the first time

Create the target location inside the Subversion repository:

    svn mkdir https://reposerver/path/to/repo/path/to/project

Edit your git repository configuration to make the connection with git-svn:

    [svn-remote "svn"]
      url = https://reposerver/path/to/repo/path/to/project
      fetch = :refs/remotes/git-svn

Import the empty Subversion history:

    git svn fetch

Replay your commits on top of the empty Subversion history:

    git rebase remotes/git-svn

Push the commits to Subversion:

    git svn dcommit

## Removing untracked files

The `git clean` command is very sophisticated with many useful options.

    # by default doesn't remove anything, wouldn't be safe!
    git clean
    
    # dry run, check what would be removed
    git clean -n

    # force, really remove untracked files
    git clean -f
    
    # interactive mode
    git clean -i
    
## How to ...

Restore file or dir from head or rev:

    git checkout -- path
    git checkout rev -- path

Mark a file in the index 'assume unchanged':

    git update-index --assume-unchanged path_to_the_file

... and how to change it back:

    git update-index --no-assume-unchanged path_to_the_file

List files that are marked 'assume unchanged' in the index:

    git ls-files -v | grep ^[a-z]

Run this once in a while:

    git gc

Create a branch and switch to it:

    git checkout -b bname

Merge from another git repository:

    git pull path_to_dir

Track specific branches of a subversion repository:
<pre>
[svn-remote "huge-project"]
        url = http://server.org/svn
        fetch = trunk/src:refs/remotes/trunk
        branches = branches/{red,green}/src:refs/remotes/branches/*
        tags = tags/{1.0,2.0}/src:refs/remotes/tags/*
</pre>

Generate <tt>.gitignore</tt> in a checkout from subversion:

    git-svn show-ignore > .gitignore

Fetch revisions from a remote branch:

    git fetch some_name

See what has changed in a remote branch relative to current:

    git log master..some_name/master

Two equivalent methods to merge from a branch:

    git merge some_name
    git pull . remotes/some_name/master

## Other

<pre>
# staging hunks
git add --patch
git merge --squash <feature_branch>

git ls-tree -r $BRANCH

git show $REVISION:$FILENAME
git checkout $REVISION -- $FILENAME

git checkout $BRANCH@{yesterday}:$FILENAME # $FILENAME as it was yesterday 
git checkout $BRANCH^:$FILENAME            # $FILENAME on the first commit parent
git checkout $BRANCH@{2}:$FILENAME         # $FILENAME two commits ago
</pre>

## Switch to Subversion branch and do some work there

<pre>
git config --add svn-remote.newbranchname.url https://svn/path_to_newbranch/
git config --add svn-remote.newbranchname.fetch :refs/remotes/newbranchname
git svn fetch newbranchname [-r<rev>]
git checkout -b local-newbranchname -t newbranchname
git svn rebase newbranchname
...
git svn dcommit --dry-run
git svn dcommit
</pre>

## Resolve conflicts

http://www.kernel.org/pub/software/scm/git/docs/v1.7.3/user-manual.html#resolving-a-merge

<pre>
git status
git checkout --theirs path
git checkout --ours path
git commit -a
</pre>

## Cherry picking

Cherry-pick merge revisions in other branch that are not in master.

<pre>
git reset --hard
git cherry-pick --abort
git rev-list ^master other-branch | git cherry-pick -n --stdin
</pre>

## Doing on the daily

### Commit temporary changes to a separate branch

<pre>
git checkout -b some-name-describing-the-change
git commit -m 'describe the change' file1 file2
git checkout master
</pre>

## gitk

    # see all branches
    gitk --all

## unsorted

https://speakerdeck.com/u/holman/p/git-and-github-secrets

    git show :/something  # last matched commit search
    # master@{1.day.ago}
    # master@{yesterday}
    git log branchA ^branchB  # commits in branchA not in branchB
    git status -sb
    git diff HEAD^ --stat
    git config --global color.ui 1
    git branch --contains sha1

    # copy file without switching branches
    git checkout branchname -- path/to/file

* click a line on github : adds #L123 to the url
* works with ranges too

    git rev-list --reverse branch1 ^master --author codername sha1.. | git cherry-pick -n --stdin

* cherry pick the revisions that are in branch1 but not in master, by specific author, after specific revision

* change the url of a remote

    git remote set-url origin git://new.url.here

* set user email address

    git config --global user.email 'janos@xw8400'

* alias remove unused branches

    delete-unused-branches = "!f() { git branch | xargs git branch -d; }; f"

<pre>
# blame ignore whitespace
git blame -w

# detect moves
git blame -M

# detect moves over files, like -M but at other files in that same commit
git blame -C

# also looks at the commit the file was created in
git blame -CC

# also looks at all commits
git blame -CCC

# word diffs
git diff HEAD^ --word-diff

# fix typos like git comit
git config --global help.autocorrect 1

# short log with count grouped by author
git shortlog -sn
</pre>

## View differences with a diff tool

    # only when using for the first time, or to change the diff tool
    git config diff.tool gvimdiff
 
    # the -y is to skip the prompt "Launch 'gvimdiff' [Y/n]"
    git difftool -y branchname -- ./path/to/file

## How to push the current branch somewhere else and track it

<pre>
git init --bare /path/to/somewhere/else
git push -u /path/to/somewhere/else master
</pre>

After this you can do <code>git push</code> with no args to push to that location.

## Rename branch

    git branch -m old_branch new_branch
    git branch -M old_branch new_branch # rename branch even if the new_branch exists
    
## Delete remote branches and tags

    git push origin :BRANCHNAME
    git push origin :refs/tags/TAGNAME

For example:

<pre>
$ git branch -r
  origin/HEAD -> origin/master
  origin/master
  origin/blah
$ git push origin :blah
To git@github.com:user/repo
 - [deleted]         blah
</pre>

## Remotes

<pre>
# show all remotes
git remote -v

# show all remote branches
git branch -r

# add a new remote
git remote add sample /path/to/remote

# fetch all branches from remotes and update branch listing
git remote update

# checkout a remote branch
git checkout -b feature1 sample/feature1

# easy way to check out and switch to a branch from a remote
git checkout feature1
</pre>

## Create a patch from pending changes

You cannot. You have to commit the pending changes and then you can create a patch from the commit.
This is not really limiting, as you can easily create a temporary branch for the temporary commit.
Actually any change that deserves a patch also deserves to be committed.
Otherwise you may lose it by mistake.

The commit log message will be used in the filename of the patch file, with spaces and other fancy characters replaced. Write a good a log message.

## Create a patch from a commit

<pre>
# Create a patch from any revision
git format-patch REV

# Create a patch from the last revision
git format-patch HEAD^
</pre>

## Caching credentials for HTTPS remotes

As of Git 1.7, *wincred* is included by default,
and it can cache your credentials so you don't need to enter repeatedly.

To activate:

    git config --global credential.helper wincred

To adjust the expiration time:

    git config credential.helper 'cache --timeout=3600'

## random memo

<pre>
# show last 5 revision numbers
git rev-list master -n 5

# show last 5 revision numbers + online commit message
git rev-list master -n 5 --oneline

# merge up to specific revision
git merge sha1

# get directory from another branch
git checkout master -- dirname

# list files in a branch/commit
# http://stackoverflow.com/questions/1910783/git-1-list-all-files-in-a-branch-2-compare-files-from-different-branch
git ls-tree -r --name-only ref

# get specific file from other branch
git checkout branch -- path

# view list of files changed between two commits
git diff --name-only ref1 ref2

# diff between ref1 to ref2. The direction is crucial
git diff ref1 ref2
git diff ref1..ref2

# diff *going from* ref2 to ref1. Yes, in that order. Crucial! 
# In other words, changes in ref2 that should be merged into ref1
git diff ref1...ref2

# show the last commit with message matching 'stupid'
git show :/stupid

# checkout previous branch
git checkout -

# list branches that contain commit
git branch --contains c68c3a0

# commits in A that aren't in B
git log branchA ^branchB

# lost commits
git fsck --lost-found

# multi-remote fetches
git config remotes.mygroup 'remote1 remote2'
git fetch mygroup

# give me master but my final state should match my current branch
git merge master -s ours

# better line matching
git merge master -s recursive -X patience

# strip trailing whitespace, collapse newlines, add final newline
git stripspace < file

# good commit messages:
# short summary < 50c
# longer explanation -- wrap at 72c
</pre>

## Notes from Zach

https://speakerdeck.com/holman/more-git-and-github-secrets

        # check for trailing whitespace and other things
        git diff --check
        
        # get the status of everything you're ignoring
        git status --ignored

        curl https://github.com/janosgyerik.keys

        # fetch pull request #12 into a branch named pr
        git fetch origin pull/12/head:pr

### `hub`

        # install with mac ports
        sudo port install hub
        
        # clone github repos
        hub clone janosgyerik/cheetsheets
        
        # easy multi-remote push
        hub push origin,staging
        
        # see more at https://speakerdeck.com/holman/git-and-github-secrets

### Commit messages

* should have a short summary, less than 50c
* longer description, wrap lines at 72c
* <code>git commit</code> (without <code>-m</code> flag), helps writing ''good'' messages

Assumes:

        EDITOR=vim
        syntax on
        filetype indent plugin on
        
### Current branch

        git rev-parse --abbrev-ref HEAD
        git symbolic-ref --short HEAD #probably works for 1.8 and newer clients only
        
### Author Information

        git --no-pager show -s --format='%ae' COMMIT_HASH #get author e-mail
        git --no-pager show -s --format='%an <%ae>' COMMIT_HASH #get author name and e-mail in user <email> format
        
### Git-Blame-Dir

```bash
#!/bin/bash

format='%Cblue%h%Creset %s%x09%ar'
git ls-tree --name-only -z HEAD |
while IFS= read -d '' file; do
git log -1 --pretty="$file"$'\t'"$format" -- "$file"
done |
column -t -s $'\t'
```

### Emoji

* `:clap:` :clap:
* `:+1:` :+1:
* `:-1:` :-1:
* `:sparkles:` :sparkles:
* `:shipit:` :shipit:
* `:heart:` :heart:
* `:fire:` :fire:
* `:rage2:` :rage2:
* `:shit:` :shit:

### GitHub

* when commenting: highlight original text and press [r] to insert quoted text
* issue autocompleting: type [#] to search
* file finder: type [t] to find in project
* task lists within issues: <code>- [] do this</code>
* branch switcher: type [w]
* quick search: type [s]
* highlight specific line(s): Append #Ln or #Ln1-n2 eg: #L5 or #L10-18

## Links

* http://cheat.errtheblog.com/s/git
* https://speakerdeck.com/holman/git-and-github-secrets
