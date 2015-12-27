Bootstrap guide for new windows workstation setup.

# manually install from links

[Chrome](https://www.google.com/chrome/browser/desktop/index.html)

[Atom](https://atom.io/download/windows)

[Docker Toolbox](https://www.docker.com/toolbox) - check all the checkboxes

# in elevated `cmd`

```bash

# install [Chocolatey](https://chocolatey.org/)
@powershell -NoProfile -ExecutionPolicy Bypass -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin

# install conemu
cinst -y conemu

```

# in elevated `git bash`

```bash

# install ConEmu.xml config
curl \
  -o $APPDATA/ConEmu.xml \
  https://raw.githubusercontent.com/micnigh/windows-workstation-bootstrap/master/files/AppData/Roaming/ConEmu.xml

# create default start dir
mkdir -p /c/projects/

```

# in elevated `conemu`

```bash

#
# workstation tools - may take a long time
#
cinst -y \
  7zip \
  jdk8 \
  maven \
  gradle \
  androidstudio \
  visualstudio2015community \
  python2 \
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
  wget \
|| cinst -y nodejs -version 4.2.2

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

# prepare c++ tools [due to node-gyp npm issues](https://github.com/nodejs/node-gyp/issues/629#issuecomment-151018292)

Roughly from this [comment](https://github.com/nodejs/node-gyp/issues/629#issuecomment-151009181)

 - Start VS2015
 - File -> New Project -> Visual C++
 - Run `Install Visual C++ 2015 Tools`

This will install the sdk you need to compile native node C++ modules on windows, improving performance.

# in `conemu`

```bash

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
  editorconfig \
  imdone-atom

# npm config
# use user path, not install path
npm config set prefix '~/npm/'
# use msys2015 when compiling modules
npm config set msvs_version 2015

```

# in `git bash`

```bash

# generate personal ssh certificates into `~/.ssh`
# NOTE - update your email and name
ssh-keygen -f ~/.ssh/id_rsa -t rsa -N "" -C "email@email.com"
git config --global user.email "email@email.com"
git config --global user.name "John Doe"
chmod 700 ~/.ssh/
chmod 600 ~/.ssh/id_rsa*

# From [micnigh/windows-dotfiles](https://github.com/micnigh/windows-dotfiles)
# install dotfiles
cd ~/
git init .
git remote add origin https://github.com/micnigh/windows-dotfiles.git
git fetch --all
git reset --hard origin/master

```

# reboot

All finished after rebooting :)
