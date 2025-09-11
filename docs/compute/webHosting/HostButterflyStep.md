---
title: How to build a butterfly blog in Github Pages
date: 2024-09-03 21:06:52
tags: github-page
top_img: img/hisameTop.png
cover: img/hisameCover.png
---

tldr: Follow the [instruction](https://butterfly.js.org/posts/21cfbf15/) from the author

## Step 1 - Initialize a hexo project

Set up a brand new hexo project by `hexo init`

After the init, these files should be appeared

![](hexoinit.png)

In the hexo root folder, clone the butterfly theme and download the hexo-renderer-pug and hexo renderer-stylus

```powershell
git clone -b master https://github.com/jerryc127/hexo-theme-butterfly.git themes/butterfly

npm install hexo-renderer-pug hexo-renderer-stylus --save
```

go to `themes/butterfly/_config.yml`. Copy all the content, create a `_config.butterfly.yml` and paste all the content

## Step 2 - Setup packages

If you have `hexo-server` and `hexo-browser-sync` installed, you can skip this

Install the hexo-server by running

```powershell
npm install hexo-server --save
```

Please noted that you need to install npm if npm is not found.

You might also want to install BrowserSync to enable hotreload

```powershell
npm install -g browser-sync

npm install hexo-browsersync --save
```

## Step 3 - Try local host

You may run `hexo server` to host a local webiste.

## Step 4 - Change theme

You might see a default hexo template but not with butterfly theme after running to local host.
Go to `_config.yml` from root and change ~~landscape~~ into butterfly

```
theme: butterfly
```

## Step 5 - Set up Github repository

Go to your github and create new repository

follow the instruction from github

```
git init
git add *
git remote add <repos url>
git commit -m 'first commit'
git push
```

## Step 6 - Set up Github Pages

Since Github page default compiling website using jekyll and we are not using jekyll, so we need to tell github not to compile as jekyll.
In the root folder, create a empty file named `.nojekyll`

**\*** Make sure to change your repository name into `<username>.github.io`, since github page can only host one website for each account and the repository name is restricted

Go to your repository in Github > Settings > Pages

Choose `Deploy from a branch` in Source

Select the branch you want to deploy

And go to `www.<username>.github.io` to see if it work after built

If you don't see the page being built, try these several things

1.  Toggle the github pages by changing deploy branch to `none` and back to the branch you like

2.  Install hexo git deployer by

```
npm install hexo-deployer-git --save
```

Go to `_config.yml` and add deploy setting

```
deploy:
  type: git
  repo: <repo url>
  branch: <branch to deploy>
```

**\*** Do not use main branch to deploy, it will generate files to the branch for deploy, it will messup your source code

then run below to directly deploy changes to github

```
hexo generate
hexo deploy
```
