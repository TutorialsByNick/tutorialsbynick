---
layout: post
title: Using Github Pages
comments: true
author: Nicholas Day
email: true
---

[Github Pages](https://pages.github.com/) is a service that Github offers which hosts websites for you. There is an option for either generated websites (like this one) using [Jekyll](https://jekyllrb.com/), a website generator. Generated websites are websites where there is for example a blog post template and you just write your post in a text box and then the generator makes the static webpages. There is also an option for hosting non-generated static webpages like in [my HTML and CSS Basics tutorial]. In this tutorial, we will learn how to host non-generated static webpages using Github Pages. You should have already read my tutorial on [Github Basics] and have Visual Studio Code installed.

First you create a repository on Github Desktop like in my [Github Basics] tutorial. Then, open the repository folder from the repository you created earlier:

![VSCode Open Folder]

In my case, the repository folder name is `my-first-app`.

If you hover over the folder name, some icons should pop up like below.

![VSCode Hover Folder]

Click the first icon, which creates a new file, and make a file named `.nojekyll`. This tells Github Pages that your repository is a simple static page one and not a Jekyll one. Press `Enter` to save the file.

![VSCode Create .nojekyll]

Now in Github Desktop, we can commit the files to git and push them to the server:

![Github Desktop commit]

Now go to your Github repository on the Github website. My repository name is `my-first-app` and my username is `nicholasday`, so the url for me would be [github.com/nicholasday/my-first-app](https://github.com/nicholasday/my-first-app).

![Github repo online]

Click on the _Settings_ link, and scroll down until you see _Github Pages Settings_ header.

![Github Pages Settings]

Click on _None_ and select the _master branch_ option. What this does is build your Github Pages website from your master branch rather than a different branch that you have created.

![Github Pages Select Master]

Don't forget to save your selection!

![Github Pages Save Master]

The page should reload and if you scroll back down to _Github Pages Settings_ there should be a website link. For me it's https://nicholasday.github.io/my-first-app/. 

![Website Link]

Previously, in my [Github Basics] tutorial we created a file called `test.txt`. So we go to the url they showed us earlier, and add `/test.txt`. The url would then be https://nicholasday.github.io/my-first-app/test.txt. As you can see VSCode and the website both have the same page!

![VSCode Test File]
![Website Test File]

If you want something to show up when you just go to a folder, place an `index.html` file in that folder. So if we want something to show up when we go to https://nicholasday.github.io/my-first-app/, we create an `index.html` in the base repository folder. Then, all you have to do is commit it to Github and push it to their servers. It should show up almost immediately on your website.

![Create Index]
![Index Website]

Feels good, right? You can now show people your work by sending them a nice link!

[my HTML and CSS Basics tutorial]: {% post_url 2017-08-31-basics-of-html-and-css %}
[Github Basics]: {% post_url 2017-09-07-github-basics %}
[VSCode Open Folder]: {{ site.url }}/images/using-github-pages/open-folder.png
[VSCode Hover Folder]: {{ site.url }}/images/using-github-pages/hover-folder.png
[VSCode Create .nojekyll]: {{ site.url }}/images/using-github-pages/nojekyll.png
[Github Desktop commit]: {{ site.url }}/images/using-github-pages/commit.png
[Github repo online]: {{ site.url }}/images/using-github-pages/repo-online.png
[Github Pages Settings]: {{ site.url }}/images/using-github-pages/github-pages-settings.png
[Github Pages Select Master]: {{ site.url }}/images/using-github-pages/select-master.png
[Github Pages Save Master]: {{ site.url }}/images/using-github-pages/save-master.png
[Website Link]: {{ site.url }}/images/using-github-pages/website-link.png
[VSCode Test File]: {{ site.url }}/images/using-github-pages/vscode-test-file.png
[Website Test File]: {{ site.url }}/images/using-github-pages/website-test-file.png
[Create Index]: {{ site.url }}/images/using-github-pages/create-index.png
[Index Website]: {{ site.url }}/images/using-github-pages/index-website.png