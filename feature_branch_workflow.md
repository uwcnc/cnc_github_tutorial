# Feature Branch Workflow

## Intro
Welcome to the Git Feature Branch workflow tutorial! We will use this repo to demonstrate a workflow that allows for collaborative development of a shared code repository. It has the features:
- "main" (previously "master") contains the source of truth
- development occurs on separate, non-"main" branches
- changes get merged into "main" through Pull Requests (PRs)
<img width="800" alt="GitHub-Flow copy" src="https://user-images.githubusercontent.com/97498519/176041670-c7b471b6-1b25-43c8-9c8f-b7c57b80bd77.png">

The steps through this demo are:
1. Cloning a repo
2. Creating a new branch
3. Pushing the branch, 
4. Creating a pull request
5. Dealing with merge conflicts

## 1. Cloning a repo
If there is an existing remote repository you'd like to start development on, usually the first thing to do would be to clone that repository to your local machine. 
To obtain a local copy of any repo, go to a directory you'd like to place the repo in, and run: 
```
git clone <REPOSITORY_URL>
```
For this repo, the command to run locally will be: 
```
git clone https://github.com/pqz317/cnc_github_tutorial.git
```
The URL can always be found under the "Clone" Section of the Github page of the repo: 
<img width="800" alt="Screen Shot 2022-06-27 at 9 42 45 AM" src="https://user-images.githubusercontent.com/97498519/175992957-a6794a57-b257-474e-b2ef-73859bfe40d2.png">
Once cloned, you should have a directory `cnc_github_tutorial` in your local filesystem. Run `git status` to verify that the directory is a git repository, and that you are on the `main` branch. An example output: 
```
Patricks-MacBook-Pro:cnc_github_tutorial patrick$ git status
On branch main
Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean
```
You have now successfully cloned a repo!

## 2. Creating a new local branch
One general convention is to keep your local `main` branch tracking the `main` in the remote, and perform any development on a different branch
To do this, run:
```
git checkout -b <SOME_BRANCH_NAME>
```
This will checkout create a new branch, and switch over to that branch. Any changes you make to files now will occur on this new branch, and not affect `main`. Using your favorite text editor, feel free to make any changes to the `test_file.txt` file. 
Once saved, we can check the status of our branch using 
```
git status
```
and add+commit our changes using: 
```
git commit -am "<SOME COMMIT MESSAGE>"
```

## 3. Pushing the branch
Currently your new branch only exists locally and not in the remote repository. To "push" it to the remote repo, run
```
git push origin <YOUR_BRANCH_NAME>
```
This will create a remote branch with the same name, and "push" your changes in your local branch to that remote branch. 

## 4. Creating a Pull Request
Your changes are on a branch on remote, but these changes are not integrated into the `main` branch yet. To integrate them, you can issue a "Pull Request", or a "request for someone to pull your changes into `main`"
Github allows you to do this easily through their website. 
