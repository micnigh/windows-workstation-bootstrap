Bootstrap guide for new windows workstation setup.

# manually install from links

[Chrome](https://www.google.com/chrome/browser/desktop/index.html)

[Atom](https://atom.io/download/windows)

[Docker Toolbox](https://www.docker.com/toolbox) - check all the checkboxes

# install [Chocolatey](https://chocolatey.org/) from elevated `cmd`

```bash
@powershell -NoProfile -ExecutionPolicy Bypass -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin
```

# install conemu from elevated `cmd`

```bash
cinst -y conemu
```

# in elevated `conemu`

```bash
#
# workstation tools - may take a long time
#
cinst -y \
  7zip \
  androidstudio \
  visualstudio2015community \
  python2 \
  nodejs \
  firefox \
  eclipse \
  vcredist2013 \
  mysql.workbench \
  notepadplusplus \
  putty \
  winscp \
  sublimetext3 \
  sublimetext3.packagecontrol \
  sublimetext3-contextmenu \
  greenshot \
  bulkrenameutility \
  treesizefree \
  curl \
  wget

# requires interaction or sometimes fails
cinst -y \
  colorpic

#
# games
#
cinst -y \
  steam \
  origin \
  teamspeak

#
# misc
#
cinst -y \
  dropbox \
  handbrake.install \
  anydvd
```

# in `conemu`

```bash

# install ConEmu.xml config
curl \
  -o $APPDATA/ConEmu.xml \
  https://raw.githubusercontent.com/micnigh/windows-workstation-bootstrap/master/files/AppData/Roaming/ConEmu.xml

# apm packages
apm install \
  minimap \
    minimap-git-diff \
    minimap-find-and-replace \
    minimap-selection \
    minimap-pigments \
  linter \
    linter-eslint \
    linter-htmlhint \
    linter-less \
    linter-scss-lint \
  pigments \
  line-ending-converter \
  git-plus \
  merge-conflicts \
  language-docker \
  language-babel \
  file-type-icons \
  file-icons \
  tabs-to-spaces \
  Sublime-Style-Column-Selection \
  color-picker \
  editorconfig

# npm config
# use user path, not install path
npm config set prefix ~/npm
# use msys2015 when compiling modules
npm config set msvs_version 2015

```

# prepare c++ tools [due to node-gyp npm issues](https://github.com/nodejs/node-gyp/issues/629#issuecomment-151018292)

Roughly from this [comment](https://github.com/nodejs/node-gyp/issues/629#issuecomment-151009181)

 - Start VS2015
 - File -> New Project
 - Run Install support for C++

This will install the sdk you need to compile node C++ modules on windows.

# install personal ssh certificates into `~/.ssh`

# add dotfiles from git bash

From [micnigh/windows-dotfiles](https://github.com/micnigh/windows-dotfiles)

```bash
cd ~/
git init .
git remote add origin https://github.com/micnigh/windows-dotfiles.git
git fetch --all
git reset --hard origin/master
```

# reboot

All finished after rebooting :)
