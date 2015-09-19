title: setting up blog environment for mac
date: 2015-09-09 20:17:06
tags:
---


#### the process is pretty easy, but takes a little bit time, just be patient

```bash
    #install nodejs and the npm
    sudo brew install npm   # if homebrew not installed, install homebrew first
    # install hexo
    sudo npm install hexo-cli -g
    sudo npm install hexo --save
    sudo npm install hexo-server --save
    # clone the source code
    git clone git@github.com:scofieldsoros/blog.git
    # install hexo dependencies
    sudo npm install
```

after that, goto the blog directory and begin writing your blog. ^_^

**some simple command of hexo**
1. hexo new "title" # create a new blog page
2. hexo generate   # generate static website files
3. hexo server     # start the server, default port 4000
4. hexo deploy      # deploy to github. already config in the _config.yml
 hexo n == hexo new
 hexo g == hexo generate
 hexo s == hexo server
 hexo d == hexo deploy

after installed, we can just start the server (hexo s) and change the 'title'.md and reload the page, change will be showed immidiately.
