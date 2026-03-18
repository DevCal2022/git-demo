# Git Tutorial
## 1. Basic
1. Check Git version
   ```bash
      git --version
   ```
2. Show config
   ```bash
      git config --global --list
      git config --local --list
   ```
3. Set identity
   ```bash
      git config --global user.name "DevCal2022"
      git config --global user.email "devendra.kag@calsoftinc.com"
   ```
4. Clone repository
   ```bash
      git clone <repo_url>
   ```
5. Import from existing folder (manual clone alternative)
   ```bash
      git init <project-directory-name>
      git remote add origin <repo_url>
      git fetch origin
      git checkout <main-branch>
   ```
6. Create branch
   ```bash
      git checkout -b <branch-name>
   ```
7. Stage files
   ```bash
      git add .
      git add <filename>
   ```
8. Commit
   ```bash
      git commit -m "message about commit"
   ```
9. Push branch
   ```bash
      git push origin <branch_name>
   ```
10. Pull branch
   ```bash
      git pull origin <branch_name>
   ```
11. Status
   ```bash
      git status
   ```
## 2. Branch
12. Rename branch
   ```bash
      git branch -m <new_name>
      # or
      git branch -m <old_branch_name> <new_branch_name>
   ```
13. Set default branch name
   ```bash
      git config --global init.defaultBranch "<branch-name>"
   ```
14. Commit tracked changes directly
   ```bash
      git commit -am "commit message"
   ```
15. Unstage file
   ```bash
      git reset HEAD <file_name>
   ```
16. Discard local changes in file
   ```bash
      git checkout -- <file_name>
   ```
17. Stash work in progress
   ```bash
      git stash
   ```
18. Rename file in Git
   ```bash
      git mv <current_file_name> <new_file_name>
   ```
19. Rename file outside Git
   ```bash
      git add -A
      git add <file_name>
   ```
20. Remove file and stage deletion
   ```bash
      git rm <file_name>
   ```
21. File deleted outside Git (use add -A / git rm through Git)
   ```bash
      git add -A
   ```
## 3. History

22. View history

   ```bash
git log
git log --abbrev-commit
git log --oneline
git log --oneline --graph --decorate
   ```

- By range: `git log <commit-range>`
- Since: `git log --since="3 days ago"`
- File history: `git log -- <filename>`
- History across renames: `git log --follow -- <filename>`
- Commit detail: `git show <commit-id>`

23. Alias history command

   ```bash
git config --global alias.hist "log --all --oneline --graph --decorate"
   ```

24. .gitignore rules

   - `text.txt`
   - `*.ext`
   - `level1/`

## 4. Install and Configure P4Merge

25. Setup P4Merge (Linux)

   1. Download p4merge from Perforce.
   2. Extract and copy to `/opt/p4merge`:

      ```bash
      gunzip p4v.tgz
      tar xvf p4v.tar
      sudo mkdir -p /opt/p4merge
      sudo mv /home/devendra/Downloads/p4v-2019.1.1830398/* /opt/p4merge
      ```

   3. Symlink executable:

      ```bash
      sudo ln -s /opt/p4merge/bin/p4merge /usr/local/bin/p4merge
      ```

   4. Set Git diff/merge tool:

      ```bash
git config --global merge.tool p4merge
git config --global mergetool.p4merge.path /usr/local/bin/p4merge
git config --global mergetool.prompt false

git config --global diff.tool p4merge
git config --global difftool.p4merge.path /usr/local/bin/p4merge
git config --global difftool.prompt false
      ```

   5. Use:

      ```bash
git difftool
      ```

   - For local repo config: replace `--global` with `--local`.

## 5. Comparison

26. Compare changes

   - Working directory vs staging:

     ```bash
git diff
git difftool
     ```

   - Working directory vs local HEAD:

     ```bash
git diff HEAD
git difftool HEAD
     ```

   - Staging vs local HEAD:

     ```bash
git diff --staged HEAD
git difftool --staged HEAD
     ```

27. Single file compare:

   ```bash
git diff -- <file>
git difftool -- <file>
   ```

28. Between commits:

   ```bash
git diff <r1> <r2>
git diff <r1> HEAD
git diff HEAD HEAD^

git difftool <r1> <r2>
   ```

29. Local vs remote

   ```bash
git diff <local_branch> <remote_branch>
git difftool <local_branch> <remote_branch>
   ```

30. Delete local branch

   ```bash
git branch -d <branch_name>
   ```

## 6. Merge & Rebase

31. Fast-forward merge

   ```bash
git merge <branch_name_to_merge>
   ```

   - For no fast-forward:

     ```bash
git merge <branch_name_to_merge> --no-ff
     ```

32. Recursive merge

   ```bash
git merge <branch_name> -m "commit message"
   ```

33. Resolve conflicts

   - Edit files manually
   - Use `git mergetool`

34. Abort merge

   ```bash
git merge --abort
   ```

35. Rebase feature branch

   ```bash
git rebase <source_branch>
   ```

36. Abort rebase

   ```bash
git rebase --abort
   ```

37. Pull with rebase

   ```bash
git pull --rebase origin/master
   ```

## 7. Stashing

38. Apply stash

   ```bash
git stash apply
git stash list
git stash drop
   ```

39. Stash untracked changes

   ```bash
git stash -u
git stash pop
   ```

40. Save stash with message

   ```bash
git stash save "message"
git stash show "stash@{index}"
   ```

41. Work with specific stash

   ```bash
git stash apply stash@{n}
git stash drop stash@{n}
   ```

42. Clear all stashes

   ```bash
git stash clear
   ```

43. Apply stash to branch

   ```bash
git stash -u
git stash branch <branch_name>
git add .
git commit -m "message"
   ```

## 8. Tagging

44. Lightweight tag

   ```bash
git tag <tag_name>
git tag --list
git tag --delete <tag_name>
git show <tag_name>
   ```

45. Annotated tag

   ```bash
git tag -a <tag_name>
# or
git tag -a <tag_name> -m "tag message"
   ```

46. Amend commit message

   ```bash
git commit --amend
   ```

47. Compare tags

   ```bash
git diff <start_tag> <end_tag>
git difftool <start_tag> <end_tag>
   ```

48. Tag specific commit

   ```bash
git tag -a <tag_name> <commit>
   ```

49. Move tag to another commit

   ```bash
git tag -a <tag_name> -f <commit>
   ```

50. Push tag

   ```bash
git push origin <tag_name>
   ```

51. Push all tags

   ```bash
git push origin <branch_name> --tags
   ```

52. Delete remote tag

   ```bash
git push origin :<tag_name>
   ```

## 9. Reset & Reflog

53. Time travel back

   ```bash
git reset HEAD^
git reset HEAD~n
   ```

54. View reflog

   ```bash
git reflog
   ```
