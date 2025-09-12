# How to create a digital garden with MkDocs

For full documentation visit [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/getting-started/).

## Prerequisite
Please make sure you have the followings:

* git
* python
* pip

## Install
Install the mkdocs-material

### pip
```
pip install mkdocs-material
```

### github

```
git clone https://github.com/squidfunk/mkdocs-material.git
pip install -e mkdocs-material
```

## Create project
Under your desired directory
```
mkdocs new .
```

You will get
```
.
├─ docs/
│  └─ index.md
└─ mkdocs.yml
```

## Configuration
edit mkdocs.yml
```
site_name: site_name
theme:
  name: material
```

## Preview
Just for preview, you can skip if you don't care
```
mkdocs serve
```

## Build site
Use mkdocs to generate the site for you
```
mkdocs build
```

You will get a `site` folder

But you don't want it to be committed to your main branch in github
to add this into gitignore
```
echo "site/" >> .gitignore
```

## Github pages

### create account
Create account if you don't have one, or if your account already used for 1 github page site

### create repo
After creating account, create a new repo
The repo name should be
```
{accountname}.github.io
```

### invite collaborators
If you want to grant access to your main github account, or friends to help maintain
Goto the repo > Setting > Collaborators, and search the target account

A email will be sent to the target for acception

### sync local to repo
Goto the local project

```
git init
```
You will get a gitignore there

you can add the site folder to gitignore mentioned in [#Build site](#build-site) now


```
git branch -M main
```

create a main branch for the project


```
git remote add origin https://github.com/{accountname}/{accountname}.github.io.git
```

```
git push -u -origin main
```

## Deploy to github page
```
mkdocs build
mkdocs gh-deploy
```