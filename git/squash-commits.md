# Squashing Commits

When working locally sometimes you will commit lots of small changes/fixes that makes
sense to combine them all into one commit.

To do this run the command `git rebase -i HEAD~{number of commits}`
where `{number of commits}` is the last number of commits to squash.

For example:
```
git rebase -i HEAD~2

pick 01d1143 fixed linting
pick 6340aaa implemented feature x

# Rebase 01d1143..6340aaa onto 69i0fda
#
# Commands:
#  p, pick = use commit
#  e, edit = use commit, but stop for amending
#  s, squash = use commit, but meld into previous commit
#
# If you remove a line here THAT COMMIT WILL BE LOST.
# However, if you remove everything, the rebase will be aborted.
#
```

To squash the last two commits:
```
pick 01d1143 fixed linting
squash 6340aaa implemented feature x
```

Save the file. Then git shows:
```
# This is a combination of 4 commits.
# The first commit's message is:
fixed linting

# This is the 2nd commit message:

implemented feature x

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
# Explicit paths specified without -i nor -o; assuming --only paths...
# Not currently on any branch.
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#
#	new file:   LICENSE
#	modified:   README.textile
#	modified:   Rakefile
#	modified:   bin/jekyll
#
```

You can now provide a new message to the squashed commit!
