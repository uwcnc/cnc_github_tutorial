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
**Note**: `origin/main` here refers to the main branch of the origin repo. `main` is the main branch. We won't go into branching too much here, so just ignore that. `Origin` is a name for the remote repository this local repository is cloned from, the "Forked" repo. Git by default keeps track of this remote repo after a `git clone` command. It will also be helpul for git to keep track of another remote repo, the "Parent" repo. To configure this, run:
```
git remote add upstream https://github.com/uwcnc/cnc_github_tutorial.git
```
This will tell your local git repo about another remote repo, and name it upstream. This will come in handy when there are changes to the "Parent" repo you want to keep track of locally. 

### **To do this in VSCode:**

Open a new window and "Clone Git Repository":
![01_vscode_welcome_inked](https://user-images.githubusercontent.com/91637560/176282400-1a05da04-0280-47e0-bb6b-ad517545b5fb.jpg)

Paste the clone URL and create a local directory `cnc_github_tutorial` for the repository location:
![02_vscode_cloneURL](https://user-images.githubusercontent.com/91637560/176283021-f46afeca-90ff-4fe8-8c59-9e42ed981ca4.PNG)

Check/change what branch you're on in the bottom left corner:                                                                                                
![04_branch](https://user-images.githubusercontent.com/91637560/176284703-2a052218-a1cd-4180-9b04-44dbe842f0f1.PNG)

Add the remote "Parent" repo by opening the Command Palette (Ctrl+Shift+P) and typing `Git: Add Remote`:
![image](https://user-images.githubusercontent.com/91637560/176289001-adaaf1e3-73f3-4bcb-add5-042edb2fffa6.png)

Paste the parent URL (found under the "Clone" section on Github):
![image](https://user-images.githubusercontent.com/91637560/176289478-861f6c9e-d755-459c-bbd1-58345f44e9db.png)

Name the "Parent" repo `upstream`:                                                                                                
![image](https://user-images.githubusercontent.com/91637560/176290365-b1fdd234-8979-409d-98de-f37e2125f803.png)

Now you have access to local, remote (origin), and remote parent (upstream) branches:
![image](https://user-images.githubusercontent.com/91637560/176294456-3d057a92-155c-4243-9e63-4d6fe83d5d36.png)


## 3. Make local changes 
In your local repository, feel free to make any changes you'd like. For simplicity, you can create a new file `<YOUR_NAME>_test.txt` and add some text to it. Once that is saved, remember to `git add` and `git commit` your changes:
```
git add . && git commit -m "created new file"
```

### **To do this in VSCode:**

Find the "Source Control" tab on the left panel and select the file you have created/modified to see a side-by-side comparison of the changes:
![08_changes](https://user-images.githubusercontent.com/91637560/176285647-d6b56a4f-7c29-4ad4-8ed9-b47fc2249e09.PNG)

Use "+" to stage changes to specific files or stage all changes:
![09_stagechanges](https://user-images.githubusercontent.com/91637560/176286062-4e64258b-0b36-49bd-82bd-698a483601d0.PNG)

Add a commit message and use "✓" to commit the staged changes:
![10_commitchanges](https://user-images.githubusercontent.com/91637560/176286244-517f9ba3-62cd-47ab-8487-d9e6f8588a51.PNG)


## 4. Push your changes to your "Forked" repo on Github
You've made and commited changes to your local repository, now its time to push your changes to your "Forked" remote repo on Github!

Run: 
```
git push origin master
```
Doing so both backs up your changes, and gets you ready to create a pull request. Note again, origin here is referring to the forked remote repo. 

### **To do this in VSCode:**
"Sync Changes" on the "Source Control" tab or simply use the sync button in the bottom left corner:
![12_pushchanges_inked](https://user-images.githubusercontent.com/91637560/176287487-a3f7a27b-0165-4440-8201-036b100d0070.jpg)


## 5. Create a Pull Request to integrate your changes into the "Parent" repo
Now, to integrate your changes into the "Parent" repo, you can create a Pull Request via Github. 

Navigate to https://github.com/<YOUR_USERNAME>/cnc_github_tutorial. Under the "Pull requests" tab, make a new pull request and select the branches you want the pull from/to: 
![14_PRacrossfork2](https://user-images.githubusercontent.com/91637560/176301427-5b678457-0d2a-4f57-b986-a025382b4d32.PNG)


## 6. Fetch changes from the parent repo to your local repo
While you were busy working on your awesome feature, other changes might've been merged into "Parent" as well, so before working on anything else, its always good to have your local repo up-to-date with what's in "Parent". In Step 2, we already configured our local git repo to track the "Parent" repo as "Upstream", so now we can just do:
```
git fetch upstream  # fetches upstream branches
git merge upstream/main  # merges upstream/main into your local main branch
```
Alternatively, a `git pull` command also works:
```
git pull upstream main
```
Now, any changes that have been merged into "Parent" should also be reflected in your local repo. 

## 7. (Potentially) Resolve merge conflicts
Merge conflicts arise when Git doesn't know how to reconcile conflicting changes occuring on the same file. In these situations, Git leaves it to the user to figure out how to best resolve the conflicting changes. 
For this example, to create a merge conflict, navigate to your local repo and run:
```
git pull upstream patrick_branch
```
Don't worry too much about the specifics of this command for now. You should see some text:
```
Auto-merging some_file.txt
CONFLICT (content): Merge conflict in some_file.txt
Automatic merge failed; fix conflicts and then commit the result.
```
Opening up some_file.txt in any text editor, you should see something like:
```
This file contains some text
<<<<<<< HEAD
Some change katherine has made
Another change katherine has made
=======
Some change patrick has made
>>>>>>> b49f523264642383fb9c61bda4dcd0348f11d695
```
The text within the `<<<<<<<` and the `>>>>>>>` are the conflicting areas. 
Anything between `<<<<<<< HEAD` and `=======` represent what you had in the file, before trying to merge in any new changes. 
Anything between `=======` and `>>>>>>>` represent what the incoming changes are. 
You can choose to accept what you had, the incoming changes, both, or a mixture of the two. 
For our example, let's choose to accept both, so remove the any lines with `<<<<<<< HEAD`, `=======` and `>>>>>>>`
Your file should now look like:
```
This file contains some text
Some change katherine has made
Another change katherine has made
Some change patrick has made
```
Now, to finish up the merge, we need to add/commit our changes. 
```
git add . && git commit -m "resolve merge conflict, keep both changes"
```
Your merge conflict has been successfully resolved!
