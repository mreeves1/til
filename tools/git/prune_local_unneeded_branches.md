# Prune unneeded local git branches

Based on http://stackoverflow.com/questions/13064613/how-to-prune-local-tracking-branches-that-do-not-exist-on-remote-anymore

So first this removes remote branches that no longer exist remotely. This command will then delete any branches listed in remote tracking that are not in remote. The "-d" flag prevents deleting unmerged branches.

git remote prune origin && git fetch --prune && git branch -r | awk '{print $1}' | egrep -v -f /dev/fd/0 <(git branch -vv | grep origin) | awk '{print $1}' | xargs git branch -d
