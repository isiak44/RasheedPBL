# Project 2 -- Basic Git Project

---

## Initializing a Repository and Making Commits 

I created a new file in the home directory called Devops_pbl and inside this folder, I ran the `git init` to reinitialise the repository in the Devops_pbl folder because I have run it before.

`git init`

<img width="1656" alt="git init" src="https://github.com/isiak44/Rasheed_Devops/assets/27869977/54ecb1a2-31fa-4852-afae-4479eb31226b">

After running `git init` we run the `git add .` to stage the modified index.htm and Project3 directory.

`git commit -m`

The -m specifies a commit message. 

<img width="1656" alt="git commit" src="https://github.com/isiak44/Rasheed_Devops/assets/27869977/43d9da33-f0e4-4a88-8578-2e5a5296cdf4">

---

## Working with Branches in Git

`git checkout -b newbranch`

The `git checkout` switch to a new branch while the -b creates a new branch. 

<img width="1656" alt="gitcheckout-b" src="https://github.com/isiak44/Rasheed_Devops/assets/27869977/94b22059-510c-4adc-b4ee-0a59940bcd81">

`git branch`

The `git branch` show list of running branch as shown below. 

<img width="1656" alt="gitbranch" src="https://github.com/isiak44/Rasheed_Devops/assets/27869977/1228d5b8-9fab-4ccb-a541-6d4a00fd8b40">

`git checkout main`

The `git checkout` help switch between branches as shown below.

<img width="1656" alt="gitcheckout" src="https://github.com/isiak44/Rasheed_Devops/assets/27869977/594983d2-1ef3-4d0f-a592-30830815b58d">

`git merge main`

In order to merge content in newbranch with main, we first checkout to newbranch with `git checkout newbranch` then we execute the `git merge main` .

<img width="1656" alt="git merge" src="https://github.com/isiak44/Rasheed_Devops/assets/27869977/a1dcbc1c-f9fb-4368-a5a7-18917eed5ba5">

`git branch -d newbranch`

Deleting `newbranch` from my branch list. 

<img width="1656" alt="giitbranch-d" src="https://github.com/isiak44/Rasheed_Devops/assets/27869977/e99dc11f-825f-495d-9b80-ae81a288be10">

---

## Collaboration and Remote Repository

After creating a github account, I created 2 Repositories, and one is Rasheed_PBL and the other is Rasheed_Devops. 
In this case, Rasheed_PBL will be linked to my local git repository. This allows me to push and pull codes from my local git repository to my GitHub repository. 

`git remote add origin` 

After the linking, I tried to push my git local Repository to GitHub with the command `git push origin main` and got an error.

<img width="1656" alt="git remote" src="https://github.com/isiak44/Rasheed_Devops/assets/27869977/e8248569-5ccb-4b25-bebb-1a060a75b349">

> Github Personal access token

The error message led me to generate a token which was used to complete the linking and no error message popped when I tried to Push to guthub. 

<img width="1723" alt="token" src="https://github.com/isiak44/Rasheed_Devops/assets/27869977/1b365528-39f0-4726-bc97-c30e93e3c086">

`git remote seturl | git push origin main `

<img width="1656" alt="git remote seturl" src="https://github.com/isiak44/Rasheed_Devops/assets/27869977/cbe9ea93-a1c7-4c14-9461-f3de0863e3b6">

`git clone https://github.com/isiak44/Rasheed_Devops.git`

here I cloned my project1.md file and project2 folder, reason for that is to move them to my Rasheed_PBL repository on my github which has been linked to my local git repositories. 

<img width="1266" alt="git clone" src="https://github.com/isiak44/Rasheed_Devops/assets/27869977/7c1afc3b-588a-4002-8567-738a67c0047a">





 
