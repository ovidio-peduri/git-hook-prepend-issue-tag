# git-hook-prepend-issue-tag
This repo explains how to set up git hooks to automatically prepend your git messages with your work item's issue number.
For example
- For a branch ```somthing/W-123456``` it will prepend the message with ```W-123456```

##### This is taken from http://mranderson.nl/2018/10/24/git-hook-commit-message/ but updated because the script was broken

# Git alias set up instructions
- edit ```~/.gitconfig``` file and add the line found at https://github.com/ovidio-peduri/git-hook-prepend-issue-tag/blob/master/config-example/.gitconfig#L1-L3
- save
- now when you run ```git po``` it will run ```git push --set-upstream origin branchName```

# Git Hooks set up instructions

### Global Setup
If you wish to have your git commit messages prepended across all repositories do the following
Make the following directory
```
mkdir ~/.git-templates/hooks
```
- create a file ```~/.git-templates/hooks/prepare-commit-msg```
- copy the contents of https://github.com/ovidio-peduri/git-hook-prepend-issue-tag/blob/master/script/prepare-commit-msg
- Save
- Make the file executable
- ```chmod a+x ~/.git-templates/hooks/prepare-commit-msg  ```

```
git config --global init.templatedir '~/.git-templates'
git config --global core.hooksPath '~/.git-templates/hooks'
```

#### Note: you may need to run ```git init``` in your repo before this hook works. All new repos should be initialized correctly.

### Per repository
If you wish to only set up prepended commit messages for a single repo
- navigate to your repo
- create a file ```./.git/hooks/prepare-commit-msg```
- copy the contents of https://github.com/ovidio-peduri/git-hook-prepend-issue-tag/blob/master/script/prepare-commit-msg
- Save
- Make the file executable
- ```chmod a+x ./git/hooks/prepare-commit-msg ```
- run ```git init```

# Using the hook
 By default it will match issues such as ```W-123456```
 So for example, if my branch name is ```something/W-123456```
 and you do ```git commit -m "My cool message```
 your commit message will be ```W-123456 My cool message```
 If the regex pattern is not found, then the commit message will not be modified.
 The regex can be modified in the source script https://github.com/ovidio-peduri/git-hook-prepend-issue-tag/blob/master/script/prepare-commit-msg#L16

