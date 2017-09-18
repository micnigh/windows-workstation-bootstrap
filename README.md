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
  sublimetext3-contextmenu \
  visualstudiocode \
  webstorm \
  datagrip \
  intellijidea-ultimate \
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

# in elevated `powershell`

```bash
# add subl command for shells
$PATH = [Environment]::GetEnvironmentVariable("PATH", "Machine")
$subl_path = "C:\Program Files\Sublime Text 3"
[Environment]::SetEnvironmentVariable("PATH", "$PATH;$subl_path", "Machine")


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
    linter-ui-default \
    linter-eslint \
    linter-sass-lint \
    linter-tslint \
  pigments \
  language-docker \
  language-babel \
  file-type-icons \
  file-icons \
  editorconfig \
  atom-typescript \
  atom-ide-ui

# optional - visual studio code packages
code --install-extension eg2.tslint
code --install-extension jpoissonnier.vscode-styled-components
code --install-extension mgmcdermott.vscode-language-babel
code --install-extension PeterJausovec.vscode-docker
code --install-extension robertohuertasm.vscode-icons
code --install-extension stringham.move-ts

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

# in elevated `conemu`

```bash
# optional - install android adb tool (for pushing ota to device)
cinst -y adb

# optional - android development tools, studio and sdk
cinst -y android-sdk androidstudio

```



# reboot

All finished after rebooting :)
