Bootstrap guide for new windows workstation setup.

# in elevated `cmd`

```bash

# install [Chocolatey](https://chocolatey.org/)
@powershell -NoProfile -ExecutionPolicy Bypass -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin

# install conemu
cinst -y conemu git

```

# in elevated `git bash`

```bash

# install ConEmu.xml config
curl \
  --insecure \
  -o $APPDATA/ConEmu.xml \
  https://raw.githubusercontent.com/micnigh/windows-workstation-bootstrap/master/files/AppData/Roaming/ConEmu.xml

# create default start dir
mkdir -p /c/projects/

```

# in elevated `conemu`

```bash
# workstation tools
cinst -y \
  7zip \
  googlechrome \
  firefox \
  atom \
  sublimetext3 \
  sublimetext3.packagecontrol \
  sublimetext3-contextmenu \
  docker \
  docker-compose \
  notepadplusplus \
  putty \
  winscp \
  greenshot \
  bulkrenameutility \
  curl \
  wget \
  python \
  nodejs

```

# in elevated `cmd`

```bash
# add subl command for shells
mklink /h c:\windows\system32\subl.exe "c:\Program Files\Sublime Text 3\subl.exe"
```

# in elevated `conemu`

```bash
# install dev dependencies to compile nodejs binary packages
npm install --global --production windows-build-tools
```

# in `conemu`

```bash
# optional - atom editor packages
apm install \
  minimap \
    minimap-git-diff \
    minimap-find-and-replace \
    minimap-selection \
    minimap-pigments \
  linter \
    linter-eslint \
    linter-sass-lint \
    linter-tslint \
  pigments \
  language-docker \
  language-babel \
  file-type-icons \
  file-icons \
  editorconfig \
  atom-typescript

# optional - generate ssh key
# generate personal ssh certificates into `~/.ssh`
# NOTE - update your email and name
ssh-keygen -f ~/.ssh/id_rsa -t rsa -N "" -C "email@email.com"
git config --global user.email "email@email.com"
git config --global user.name "John Doe"
chmod 700 ~/.ssh/
chmod 600 ~/.ssh/id_rsa*

# optional - install my version of windows dotfiles
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
