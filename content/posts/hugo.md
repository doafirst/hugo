---
title: "Hugo"
date: 2021-08-10T22:11:20+08:00
draft: true
---

### Git path from git hub

```bash
git clone https://github.com/doafirst/hugo.git
./sub_update.sh
```

### 1. Hugo install on ubuntu

```bash
sudo snap install hugo --channel=extended
```

### 2.  New Site Hugo

```bash
hugo new site hugo_sample
cd hugo_sample
```

![Hugo%20ea8f1a335d184aa69cb6f1aee434867d/Screenshot_from_2021-08-09_10-45-04.png](Screenshot_from_2021-08-09_10-45-04.png)

### 3. Add theme

```bash
cd hugo_sample/
git init 
git submodule add https://github.com/mivinci/hugo-theme-minima.git themes/minima
cp themes/minima/exampleSite/config.toml .
#or
echo 'theme = "minima"' >> config.toml

```
  
Submodule Commands

```bash
#First time add theme method
git submodule add https://github.com/AmazingRise/hugo-theme-diary.git themes/diary

#If .gitmodules theme has already exist. but folder is empty
git submodule init
git submodule update
#or single update
git submodule update --remote themes/diary
```


### 4. New Post

```bash
hugo new posts/hello.md
cat content/posts/hello.md
```


### 5. Server start

```bash
hugo server -D
```


![Hugo%20ea8f1a335d184aa69cb6f1aee434867d/Screenshot_from_2021-08-09_10-52-28.png](Screenshot_from_2021-08-09_10-52-28.png)

![Hugo%20ea8f1a335d184aa69cb6f1aee434867d/Screenshot_from_2021-08-09_10-56-41.png](Screenshot_from_2021-08-09_10-56-41.png)

### 6. Generate Github Page Content

Set correct baseURL address in **config.toml** file
My github page path is [https://doafirst.github.io/hugo_website](https://doafirst.github.io/hugo_website)

![Hugo%20ea8f1a335d184aa69cb6f1aee434867d/Untitled.png](Untitled.png)

Hugo build 

```bash
hugo -d ../hugo_website -D
# -D, --buildDrafts            include content marked as draft
# -d, --destination string     filesystem path to write files to
cd ../hugo_website
ls 
#Check index.html existed
```


### 7. Create new repository

![Hugo%20ea8f1a335d184aa69cb6f1aee434867d/Untitled%201.png](Untitled%201.png)

Git Path : [https://github.com/doafirst/hugo_website.git](https://github.com/doafirst/hugo_website.git)


### 8. Push hugo_website  folder to github

```bash
cd hugo_website
git init 
git add .
git commit 
git add remote origin https://github.com/doafirst/hugo_website.git
git push origin master 
```


### ９. Github Page Enable

hugo_website Repository → Settings → Page →Select Branch & Save

![Hugo%20ea8f1a335d184aa69cb6f1aee434867d/Untitled%202.png](Untitled%202.png)

![Hugo%20ea8f1a335d184aa69cb6f1aee434867d/Untitled%203.png](Untitled%203.png)

### Lesson Learn 1 : 
###Git clone repository "themes" folder empty

After git clone and hugo build , and some error message showed.

![Hugo%20ea8f1a335d184aa69cb6f1aee434867d/Untitled%204.png](Untitled%204.png)

Build fail reason is themes folder empty , there is nothing in **diary** folder

![Hugo%20ea8f1a335d184aa69cb6f1aee434867d/Untitled%205.png](Untitled%205.png)

I use git submodule to clone themes , therefore the themes submodules will not upload to git repository. 

![Hugo%20ea8f1a335d184aa69cb6f1aee434867d/Untitled%206.png](Untitled%206.png)
