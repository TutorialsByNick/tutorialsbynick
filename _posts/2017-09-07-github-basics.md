---
layout: post
title: Github Basics
comments: true
author: Nicholas Day
email: true
---

Github is a place where many people put their code. Github hosts git servers for you, git servers serve git repositories. Git repositories are basically folders that you put code in, but they have some special features. They let you share them on sites like Github or Bitbucket and store the complete history of the files you put in there and the changes you've made to them. It does this by looking for the differences between your original files and your new changes everytime you make a commit (referred to as diffing). Diffing also allows other people to collaborate on your code easier than before because every person sees the changes everyone makes. Commits save your changes into git and do this diffing process. When you _push_ your code you're uploading to a git server, and when you _pull_ you're download from a git server. That was a lot of jargon so let's see it in action.

# Table of Contents
* TOC
{:toc}

# Setting up Github for Desktop

Github Desktop is an easy interface to the git program and Github itself, so we'll use it.

First, download [Github for Desktop](https://desktop.github.com/). Once you install it, the following window should pop up:

![Github Desktop First Screen]

Click _Sign into Github_ or _Create your free account_ if you don't have one.

![Github Registration]

# Creating your first repository

Once you're signed in a screen like below should show up. This name and email will show up when you contribute to a project.

![Github Desktop Configure Git]

Now Github Desktop should look like this:

![Github Desktop Logged In]

You're ready to create your first repository! Click on _Create new repository_ and then select a folder to put your repository in. Usually the default option is fine, but you'll have to remember where it's stored so you can edit your code inside of your repository folder. In my case, the repository is located at `/home/nicholas/downloads/Github/my-first-app`. When you clone a project that means download for the first time onto this computer.

![Github Desktop Repository Creation]

You can switch repositories by clicking on the dropdown at the top.

![Github Desktop Repository List]

# Making your first commit

A commit is a change saved into the git repository's history. Add a code file you'd like to put in the repository by copying and pasting that file into your code repository folder. You can also just edit a new file in that folder.

Inside of Github Desktop, you should see the changes you just made. You can select what changes will be committed and what will be left out of the commit to be changed later. At the bottom you can provide a summary and description of the changes you made. When you click `Commit to Master`, your change is saved in the `master` branch. Branches are like branches on trees. They all stem from the master 'tree' and can diverge from it. So you can make changes in a `fixallthebugs` branch that won't affect the `master` branch and then later you can merge `fixallthebugs` into master once the bugs are all fixed. For most projects though, just using the `master` branch is good enough.

On the right is a 'diff'. This shows a line by line summary of the changes that you've made to the selected file.

![Github Desktop First Commit]

# Publishing your Repository

Before we do anything, let's publish our repository to Github. Click the _Publish repository_ button, and make sure to uncheck _keep this code private_ unless you want to pay Github for a private repository (public repositories are free by default). If you're a student with an edu email, you can sign up for the [Github Student Developer Pack](https://education.github.com/pack) which has free private repos, and some free server hosting credits.

![Github Desktop Publish Button]

![Github Desktop Publish Repo]

# Pushing and Pulling

If you want to share your changes or back them up, you can push to origin. Origin is the main server that you'll use for git, but there can be other servers that you can push to. Like if you wanted to push to another server and it would put your code onto a website and deploy it. Github Desktop has a handy button for that at the top.

![Github Desktop Push Button]

Pulling and fetching download code from the server onto your computer and can merge the code from the server with your code. This is handy if you want to backup your code, move computers, or collaborate with other people. 

![Github Desktop Fetch Button]

# Your History

Next to the _History_ tab, there is a tab for the history of your repository. When you click on it, you should be able to see a log of all the the commits you have made and their diffs.

![Github Desktop History]

You can also right click on a commit and revert it. This will undo your changes in the commit. Its a very handy feature for when you make a mistake and want to undo it, even a few commits later. Its important to commit small working changes for this purpose.

# The End

There is a lot more to git and Github than I went over here, but this should be enough to get you started. Git is a very advanced tool and there are lots of gotchas and ways to use it, but you should only add complex features when you actually need them. Not when you think it is cool, but when you have a need for it.


[Github Registration]: {{ site.url }}/images/github-basics/registration.png
[Github Desktop Logged In]: {{ site.url }}/images/github-basics/logged-in.png
[Github Desktop Configure Git]: {{ site.url }}/images/github-basics/configure-git.png
[Github Desktop First Screen]: {{ site.url }}/images/github-basics/first-window.png
[Github Desktop First Commit]: {{ site.url }}/images/github-basics/first-commit.png
[Github Desktop Push Button]: {{ site.url }}/images/github-basics/push-button.png
[Github Desktop Fetch Button]: {{ site.url }}/images/github-basics/fetch-button.png
[Github Desktop History]: {{ site.url }}/images/github-basics/history.png
[Github Desktop Publish Repo]: {{ site.url }}/images/github-basics/publish-repo.png
[Github Desktop Publish Button]: {{ site.url }}/images/github-basics/publish-button.png
[Github Desktop Repository List]: {{ site.url }}/images/github-basics/repo-list.png
[Github Desktop Repository Creation]: {{ site.url }}/images/github-basics/repo-creation.png
