---
layout: post
title:      "Error: does not have a commit checked out"
date:       2020-08-07 15:23:48 +0000
permalink:  error_does_not_have_a_commit_checked_out
---


When creating a project that contains both a back-end and a front-end, you may be tempted to create two repositories, one for each of them. However, by doing so you have to jump through a few hurdles with git to link the repositories under another one so commits can be synched. This is done through submoduling. This is also NOT the route I took. I chose to house my folders for back-end and front-end within a main project directory. However, if you were to try and "git add" or "git commit" from the main directory you will get the above error in the title. This occurs do to a hidden .git file existing in the folders. By following the below steps, you will be able to "add" and "commit" without encountering the error.

1. Create main project directory on your PC. For example, we will name this /project
```
mkdir project
```
2. Change directory, cd, into the newly created /project
```
cd /project #will change depending on where directory is housed
```
3. Create repository under the same name in github. *Do not intialize the repo with a README*
4. Follow the below commands to push your newly created directory to the repository
```
echo "# project" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin git@github.com:githubusername/project.git
git push -u origin master
```
5. Create back-end and front-end folders using scaffolding/generators *I will be using rails and react*
```
rails new project-backend
npx create-react-app project-frontend
```
6. "cd" into both the back-end and front-end folders to check/remove .git files
```
cd /project/project-backend
#check for .git files using this command
ls -la
#if .git files present
rm -rf .git
```
```
cd /project/project-frontend
#check for .git files using this command
ls -la
#if .git files present
rm -rf .git
```
7. Change directory, cd, into the main /project directory
```
cd /project
```
8. Follow the steps to add, commit, and push changes
```
git add .
git commit -m "create frontend and backend scaffolding"
git push
```

At this point your entire project, including the back-end and front-end folders, now exist under one repository. This means that you will not have to submit commits to two different repositories. Also, for organizational purposes, your code exists in one place. Happy Coding :)

