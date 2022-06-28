# Forking Workflow

## Intro
Welcome to the Forking Workflow tutorial! Here we will demonstrate a workflow that allows for collaborative development of a shared code repository. In brief, the "Forking Workflow" can be described as:
- Individual developers "fork" some shared repository
- Development occurs on individual, forked repositories
- Individual development gets integrated into shared repository through Pull Requests (PRs)


The Forking Workflow involves 3 different repositories:
- **Upstream, or "Parent" Repo**: This remote repository belongs to some organization that is not the individual developer. Maintainers of this repository control who gets to make changes, and can review/accept/decline and incoming changes through pull requests. 
- **Origin, or "Forked Remote" Repo**: This remote repository is a fork of the "Parent", and belongs to the individual developer. Any changes made here are separate from the parent. The individual developer can create pull requests from this repo to the parent. 
- **Local Repo**: This is the local repo on the device of the individual developer, and it is where development occurs. It is a clone of the "Forked Remote" repo. 

![featured_hud478d74d48d19bfd1c1c03fc398c8033_312322_720x0_resize_lanczos_3](https://user-images.githubusercontent.com/97498519/176066441-ac8fadbf-a6c3-4dd1-b137-d59274bdcb0e.png)


**Note**: There is a separate workflow that you may encounter which uses branches within the same repository to achieve similar affects. There is a tutorial for that as well: https://github.com/pqz317/cnc_github_tutorial/blob/main/feature_branch_workflow.md 

The steps through this demo are:
1. Fork this "Parent" Repo to create a "Forked" Repo
2. Clone the "Forked" Repo to create a Local Repo
3. Make local changes 
4. Push your changes to your "Forked" repo on Github
5. Create a Pull Request to integrate your changes into the "Parent" repo
6. Fetch changes from the parent repo to your local repo
7. (Potentially) Resolve merge conflicts

## 1. Fork this "Parent" Repo to create a "Forked" Repo
Say there is an existing remote repository that belongs to some organization, and you'd like to start development on it, usually the first thing to do would be to create a "fork" of this repository for yourself. This provides you with a repository on Github that is a clone of its "parent", where you can do any type of development and testing on without affecting the parent. 

For this tutorial, you can fork this repo with the "fork" button on Github: 
<img width="1000" alt="Screen Shot 2022-06-27 at 7 00 30 PM" src="https://user-images.githubusercontent.com/97498519/176095938-ef63421c-a878-426b-bcfb-2a3e736d3b2c.png">
You have now successfully "forked" the `cnc_github_tutorial` repo, and created a new repo that is `<YOUR_USERNAME>/cnc_github_tutorial`


## 2. Clone the "Forked" Repo to create a Local Repo
Your "forked" repo still only lives on Github, so to obtain a local copy of it and begin developing, run 
```
git clone https://github.com/<YOUR_USERNAME>/cnc_github_tutorial.git
```
The URL can always be found under the "Clone" Section of the Github page of your "forked" repo: 
<img width="800" alt="Screen Shot 2022-06-27 at 9 42 45 AM" src="https://user-images.githubusercontent.com/97498519/175992957-a6794a57-b257-474e-b2ef-73859bfe40d2.png">
Once cloned, you should have a directory `cnc_github_tutorial` in your local filesystem. Run `git status` to verify that the directory is a git repository, and that you are on the `main` branch. An example output: 
```
Patricks-MacBook-Pro:cnc_github_tutorial patrick$ git status
On branch main
Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean
```
**Note**: `origin/main` here refers to the main branch of the origin repo. `Main` is the main branch. We won't go into branching too much here, so just ignore that. `Origin` is a name for the remote repository this local repository is cloned from, the "Forked" repo. Git by default keeps track of this remote repo after a `git clone` command. It will also be helpul for git to keep track of another remote repo, the "Parent" repo. To configure this, run:
```
git remote add upstream https://github.com/uwcnc/cnc_github_tutorial.git
```
This will tell your local git repo about another remote repo, and name it upstream. This will come in handy when there are changes to the parent repo you want to keep track of locally. 

## 3. Make local changes 
In your local repository, feel free to make any changes you'd like. For simplicity, you can create a new file `<YOUR_NAME>_test.txt` and add some text to it. Once that is saved, remember to `git add` and `git commit` your changes:
```
git add . && git commit -m "created new file"
```

## 4. Push your changes to your "Forked" repo on Github
You've made and commited changes to your local repository, now its time to push your changes to your "Forked" remote repo on Github!
run: 
```
git push origin master
```
Doing so both backs up your changes, and gets you ready to create a pull request. Note again, origin here is referring to the forked remote repo. 


## 5. Create a Pull Request to integrate your changes into the "Parent" repo
Now, to integrate your changes into the "Parent" repo, you can create a Pull Request via Github. 
Navigate to https://github.com/<YOUR_USERNAME>/cnc_github_tutorial. 

