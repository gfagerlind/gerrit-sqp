# gerrit-sqp
```
# sqp [REMOTE/BRANCH]
# squashpush2review:
# this is a gerrit helper that makes it so
# you dont need to squash or commit amend all the time.
#
# Just commit, amend, merge, cherry-pick, rebase etc. like ordinary,
# and then to push to gerrit with `sqp`
#
# If you need to change something in your gerrit changeset,
# just commit as usual and then run `sqp` again.
#
# If you want to diff against or checkout your last gerrit changeset,
# use `sqp/<branch>`, like `git diff mybranch sqp/mybranch`
#
# If you rather run it as `git sqp`, add:
#       sqp = "!f(){ sqp $@; };f"
# to you git config
#
# This uses the branch name to map to gerrit changes, so if you reuse branch names
# for different changes this will behave weird (while still work).
#
# internally, step by step, this script:
# - breaks loose from the branch (so to not change it)
# - autosquashes to the branch off point,
#   in relation to the target branch (origin/master)
# - commits the squashed files,
#   starting commit message from all squashed commit messages
#    OR
#   the commit message used the previous time this branch was sqp'd
# - marks this commit with refs/sqp/<branch>, so to keep the commit message
# - pushes the refs/sqp/<branch> to the remote/target
# - makes sure to always exit on the original branch
# ...
# │
# o $BRANCH_BASE (origin/master or branch off point)
# ├┬┐
# ││o $TARGET (origin/master, sometimes identical with $BRANCH_BASE)
# │o refs/sqp/$BRANCH (what is pushed, contentwise identical with $BRANCH)
# ... (commits)
# │
# o $BRANCH
```
