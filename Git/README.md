# Git

Everything you need to know about git.

---
## Table of Contents

- [Git Install](git_install.md)
- [Working with Git](working_with_git.md)
- [Stashing](stashing.md)
- [Rebasing](rebasing.php)
- [Working with Patches](working_with_patches.md)

---

#### Resources:

1. https://ariejan.net/2009/10/26/how-to-create-and-apply-a-patch-with-git/
2. http://rogerdudler.github.io/git-guide/

---

## The End

```sh
//Commands to add
git reset --hard HEAD~1 -> will remove everything of last commit
git reset --hard HEAD~2 -> will remove everything from last 2 commits
git reset --soft HEAD~1 -> will remove commits without there changes
git am < /var/www/html/patches/patchName.patch -> to apply patch
git log

rebase in git
git rebase --abort
```

http://stackoverflow.com/questions/1628088/reset-local-repository-branch-to-be-just-like-remote-repository-head

http://stackoverflow.com/questions/10657315/git-merge-left-head-marks-in-my-files
