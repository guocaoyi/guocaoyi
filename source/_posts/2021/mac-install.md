---
layout: post
title: MacOS 装机
date: 2021-02-20 12:49:06
tags:
  - article
  - os
auther: guocaoyi
---

# MacOS 装机

> 「Level ｜ Type ｜ Origin」：建议程度｜类型｜安装源

- Level（建议程度）
  - M（Must） 必须
  - S（Shall） 要
  - R（Recommend） 推荐
- Type（类型）
  - Env（Lang、CLI、Global、REPL、Compiler、Tool、PM）
  - APP（Desktop、GUI Client、IDE、Product）
  - VM（Runtime、VM、Container）
  - Extension（Plugin、Configuration）
- Origin（安装源）
  - App Store
  - Github
  - Official Website
  - Homebrew（System PM）
  - Docker Hub
  - Package Manager（MVN、NPM、Inner Registry）

<!-- more -->

## Reference

1. 通用环境
2. 场景开发（Frontend、Backend、iOS、Android、Service）
3. 其他（WebApp、Extension、App）

## 通用环境

- Brew「M ｜ Env ｜ Github or Run Shell Scripts」

```sh
# install homebrew
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# if network error(403), download shell script
sh install.sh
/bin/bash -c install.sh

# brew 切中科大镜像（required git）
cd "$(brew --repo)"
git remote set-url origin git://mirrors.ustc.edu.cn/brew.git
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
git remote set-url origin git://mirrors.ustc.edu.cn/homebrew-core.git

# download cache folder(can remove all)
ls ~/Library/Caches/Homebrew/downloads
```

- Git「M ｜ CLI ｜ Brew or Xcode」

```sh
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<\%an>%Creset' --abbrev-commit --"
```

```sh
brew install git # or install xcode(include git)

# configuration
git config --global user.name "***"
git config --global user.email "***"

git config --global alias.lg \"log --color --graph --pretty=format:\'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<\%an>%Creset' --abbrev-commit --"
```

- Chrome「M ｜ Desktop ｜ Brew or https://google.cn/chrome」

```sh
brew install --cask google-chrome
brew install --cask google-chrome —appdir=/Applications Chrome

# sign in and sync you setting & extension & bookmark
```

- Visual Studio Code「S ｜ IDE ｜ Brew or https://code.visualstudio.com」

```sh
brew install --cask visual-studio-code

# ⇧ + ⌘ + p > shell command: install 'code....
code --version

# sign in and sync you setting & extension
```

- Docker「S ｜ Env ｜ Brew」

```sh
# gui + cli
brew install --cask docker
```

- iTerm2「R ｜ IDE ｜ Brew」

```sh
brew install --cask iterm2

# extensions
```

- Oh My Zsh「R ｜ CLI ｜ Github or Run Shell」

```sh
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

- ClashX「R ｜ CLI ｜ Github」

```sh
brew install --cask clashx

# inject your subscribe & token
```

### Tools

- Command Line「S ｜ CLI ｜ Brew」

```shell
# ssh & ssl
brew install telnet
brew install ca-certificates

# compress
brew install --cask rar # may be blocked, allow anyway
brew install unzip
brew install zstd

# network
brew install htop # top replacement
brew install procs # ps replacement
brew install dog # dig replacement
brew install curl
brew install httpie # curl replacement

# folder
brew install cloc # code analysis
brew install exa # ls replacement
brew install rename
brew install tree
brew install broot # tree replacement, overview
brew install zoxide # cd replacement,
brew install bat # cat replacement, line number & highlight
brew install fx # json viewer, line number & highlight
brew install hexyl # hex viewer
brew install diff-so-fancy # diff-highlight
brew install fd # find replacement
brew install ripgrep # grep replacement
brew install mcfly # ctrl-r replacement
brew install choose # cut replacement
brew install duf # du replacement
brew install ncdu # du replacement
```

- Xnip「S ｜ Global Tools ｜ App Store」
- Alfred「S ｜ GUI Client ｜ App Store」

- Postman「R ｜ GUI Client ｜ App Store or Brew」

```sh
brew install --cask postman
# sign in and sync your settings
```

- Sublime Merge「R ｜ GUI Client ｜ Brew」

```sh
brew install --cask sublime-merge
```

- DevToys「R ｜ GUI Client ｜ Github & Brew」

```sh
brew install --cask devtoys
```

- SnippetsLab「R ｜ GUI Client ｜ App Store」
- Terminus「R ｜ GUI Client ｜ App Store」
- Git Streaks「R ｜ GUI Client ｜ App Store」
- SwitchHosts「R ｜ Desktop ｜ GitHub」
- OSS Browser「R ｜ GUI Client ｜ GitHub」
- Apifox「R ｜ GUI Client ｜https://apifox.cn」

## 场景开发

### Frontend（Web、小程序、Hybrid）

- NVM「M ｜ PM ｜ Brew」

```bash
# nvm
brew install nvm

mkdir ~/.nvm
vi ~/.zshrc # add
export NVM_DIR="$HOME/.nvm"
    [ -s "$(brew --prefix)/opt/nvm/nvm.sh" ] && \. "$(brew --prefix)/opt/nvm/nvm.sh" # This loads nvm
    [ -s "$(brew --prefix)/opt/nvm/etc/bash_completion.d/nvm" ] && \. "$(brew --prefix)/opt/nvm/etc/bash_completion.d/nvm" # add this to ~/.zshrc or .bashrc
```

- Node「M ｜ Env ｜ NVM」

```bash
# node LTS
nvm install 12 # 12.22.12
nvm install 14 # 14.19.3
nvm install 16 # 16.15.0
nvm install 18 # latest

# nvm set default(new terminal session keeping)
nvm alias default ** # lts version, install first

# npmrc & registry
npm login --registry=https://registry.npmjs.com
npm login --registry=https://registry.npmmirror.com
npm set registry https://registry.npmmirror.com # taobao源
npm adduser

# use npx change registry
npx nrm use taobao
npx nrm use npm

# deno
brew install deno

# other pm
brew install pnpm
brew install yarn
```

- TypeScript「S ｜ Lang ｜ Brew」

```sh
brew install typescript
```

#### 小程序

- Taro「R ｜ Lang ｜ Brew」

```sh
npm i -g @tarojs/cli # use npx @tarojs/cli to replace
```

#### 桌面客户端

- Electron「R ｜ Lang ｜ Brew」

```sh
npm i electron-rebuild -g # use npx to replace
npm i node-gyp -g # use npx to replace

brew install cmake # cross platform

# mirror, better to write in your project .npmrc
npm config set electron_mirror https://mirrors.huaweicloud.com/electron/
```

### Backend（VM、WebServer、DB、Middleware）

- Java「M ｜ Lang ｜ Brew」

```sh
brew install jenv

# zulu OpenJDK
brew tap homebrew/cask-versions
brew install --cask zulu11

# pm(versino manage)
brew install maven

# mvn registry maven.aliyun.com
```

- Python「S ｜ Lang ｜ Brew」

```sh
brew search python
brew list | grep python #  python@3.7 python@3.8 python@3.9

brew switch python 3.9
```

- Rust「R ｜ Lang ｜ rustup.rs or Brew」

```sh
# offical
curl https://sh.rustup.rs -sSf | sh

# or
brew install rust
brew install cargo-c
```

### Android & iOS

- Android Studio「M ｜ CLI ｜https://developer.android.com/studio」
- Android SDK & AVD「M ｜ CLI ｜ Brew」
- Android Platform Tools

```sh
brew install --cask android-platform-tools
```

- Kotlin「S ｜ Lang ｜ Brew」

```sh
brew install kotlin
```

- Xcode「M ｜ Env ｜ App Store」

- CocoaPods「M ｜ CLI ｜ Brew」

```bash
brew install cocoapods
```

- React Native「R ｜ Lang ｜ NPM」

```sh
brew install watchman

# android
brew tap homebrew/cask-versions
brew install --cask zulu11

# init
npx react-native init AwesomeProject
```

- Dart & Flutter「R ｜ Lang ｜ NPM」

```sh
# dart
brew tap dart-lang/dart
brew install dart

# flutter(include dart)
brew install --cask flutter

# view https://dartpad.dev, online playground
```

- Genymotion「S ｜ CLI ｜https://www.genymotion.com」

- Debugging「S ｜ CLI ｜ Brew」

```sh
# Charles
brew install --cask charles
# Flipper(https://fbflipper.com)
brew install --cask flipper
```

### Service

> 使用 Docker 来管理常用服务（应用、中间件）可以保证环境的纯净，以及移植性

- Docker Images「R ｜ Env ｜ Docker」

```shell
# mongo
docker pull mongo
docker pull mongo-express # web-based

# mysql
docker pull mysql:latest # 8.x
docker pull mysql:5.7

# redis
docker pull redis
docker pull bitnami/redis

# sqlite3
docker pull nouchka/sqlite3

# memcached
docker pull memcached

# zookeeper
docker pull zookeeper

# kafka
docker pull bitnami/kafka

# jenkins
docker pull jenkins

# sentry
docker pull sentry

# tomcat
docker pull tomcat

# server
brew install nginx

# apache
docker pull httpd
```

- GUI Client「R ｜ GUI Client ｜ Brew」

```shell
# Sequel Ace(for mysql)
brew install --cask sequel-ace

# MongoDB Compress(mongo)
brew install --cask mongodb-compass-isolated-edition
# MongoDB Realm Studio(for realm)
brew install --cask mongodb-realm-studio

# SQLite Broswer
brew install --cask db-browser-for-sqlite
```

- Medis「R ｜ GUI Client ｜ App Store」

## 其他（WebApp、Extension、App）

### WebApp

- Excalidraw「S ｜ Tools ｜https://excalidraw.com」
- ProcessOn「S ｜ Tools ｜https://processon.com」
- Miro「S ｜ Tools ｜https://miro.com」
- 小画桌协同白板「R ｜ Tools ｜https://xiaohuazhuo.com」

### Extension

- EditThisCookie「S ｜ Chrome Ext ｜ Chrome WebStore」
- PrettyPrint「S ｜ Chrome Ext ｜ Chrome WebStore」
- Octotree「S ｜ Chrome Ext ｜ Chrome WebStore」
- Gitlab tree「S ｜ Chrome Ext ｜ Chrome WebStore」
- SingleFile「S ｜ Chrome Ext ｜ Chrome WebStore」
- Vimium「S ｜ Chrome Ext ｜ Chrome WebStore」

- Logs Explorer「R ｜ Docker Ext ｜ Docker Marketplace」

- Debugger for Chrome「R ｜ Code Ext ｜ Code」
- EditorConfig for VS Code「R ｜ Code Ext ｜ Code」
- ENV「R ｜ Code Ext ｜ Code」
- Git History「R ｜ Code Ext ｜ Code」
- GitHub Copilot「R ｜ Code Ext ｜ Code」
- MarkdownLint「R ｜ Code Ext ｜ Code」
- Material Icon Theme「R ｜ Code Ext ｜ Code」
- Prettier「R ｜ Code Ext ｜ Code」
- SVG Viewer「R ｜ Code Ext ｜ Code」
- TODO Highlight「R ｜ Code Ext ｜ Code」
- Path Intellisense「R ｜ Code Ext ｜ Code」

### App

#### 通讯

- WeChat「S ｜ Desktop ｜ App Store」
- DingTalk「R ｜ Desktop ｜ App Store」
- WeCom「R ｜ Desktop ｜ App Store」

#### 字典 & 文档 & 记录

- Eudic「S ｜ Desktop ｜ App Store」
- Bear「S ｜ Desktop ｜https://bear.app」
- aDrive「R ｜ Desktop ｜https://aliyundrive.com」
- MindNode「R ｜ Desktop ｜ App Store」

#### 电脑磁盘整理

- CleanMyMac X「S ｜ Desktop ｜https://macpaw.com」

### Brew Bundle

```sh
Using dart-lang/dart
Using homebrew/bundle
Using homebrew/cask
Using homebrew/core
Using homebrew/services
Using broot
Using cloc
Using cmake
Using cocoapods
Using curl
Using exa
Using ideviceinstaller
Using ios-deploy
Using jenv
Using kotlin
Using nvm
Using rename
Using rust
Using telnet
Using tree
Using unzip
Using zoxide
Using dart-lang/dart/dart
Using android-platform-tools
Using charles
Using clashx
Using db-browser-for-sqlite
Using devtoys
Using docker
Using flipper
Using google-chrome
Using iterm2
Using mongodb-compass
Using mongodb-realm-studio
Using postman
Using rar
Using redis-pro
Using sequel-ace
Using sublime-merge
Using visual-studio-code
```
