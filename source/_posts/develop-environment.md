title: develop environment
date: 2015-09-09 20:16:34
tags:
---

## setting up vim
TODO


## setting up git
### install git-complete

```bash
 wget --no-check-certificate https://raw.githubusercontent.com/git/git/master/contrib/completion/git-completion.bash
 chmod a+x git-completion.bash
 mv git-completion.bash /etc/bash_completion.d/   # or anywhere else
```

### setting configs
```bash
git config --global color.ui auto
git config --global user.name "my name"
git config --global user.email "my email"
```

 edit the ~/.bash_profile, add `source /etc/bash_completion.d/git-completion.bash`

logout and login, and it's done

### WHAT ELSE ??

