title: iTerm2 with powerline theme
comment: true
date: 2019-06-13 14:01:03
categories: 工具控
---
### 确保已经安装了oh-my-zsh
[https://github.com/robbyrussell/oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh)

### 安装 oh-my-zsh-powerline-theme
[https://github.com/jeremyFreeAgent/oh-my-zsh-powerline-theme](https://github.com/jeremyFreeAgent/oh-my-zsh-powerline-theme)

```shell
cd ~/.oh-my-zsh/themes
git clone git@github.com:jeremyFreeAgent/oh-my-zsh-powerline-theme.git

#更新submodule,进行powerline-fonts安装
cd oh-my-zsh-powerline-theme
git submodule init
git submodule update

#安装
./install_in_omz.sh
```

### 更改iterm字体
iTerm2 -- Preferences -- Profiles -- Text
找到Font，点击Change Font，将字体改为`Fira mono for powerline`, 字号14pt

### 修改zsh配置
打开`~/.zshrc`文件，修改`ZSH_THEME"`为`powerline`

添加如下配置
```shell
POWERLINE_RIGHT_B=""  
POWERLINE_RIGHT_A="date"  
POWERLINE_RIGHT_A_COLOR_FRONT="black"  
POWERLINE_RIGHT_A_COLOR_BACK="red"  
POWERLINE_HIDE_HOST_NAME="true"
POWERLINE_PATH="short"
POWERLINE_SHORT_HOST_NAME="true"
POWERLINE_DETECT_SSH="true"
POWERLINE_GIT_CLEAN="✔"
POWERLINE_GIT_DIRTY="✘"
POWERLINE_GIT_ADDED="%F{green}✚%F{black}"
POWERLINE_GIT_MODIFIED="%F{blue}✹%F{black}"
POWERLINE_GIT_DELETED="%F{red}✖%F{black}"
POWERLINE_GIT_UNTRACKED="%F{yellow}✭%F{black}"
POWERLINE_GIT_RENAMED="➜"
POWERLINE_GIT_UNMERGED="═"
```

### 最终效果
![/uploads/powerline.png](/uploads/powerline.png)
