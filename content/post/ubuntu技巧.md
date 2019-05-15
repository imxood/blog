+++
date = "2019-05-14T19:25:43+08:00"
draft = true
title = "linux命令"
+++


# ubuntu 技巧

## 使用gsettings配置Gnome3行为

### gsettings set/get/range/list-keys

gsettings range org.gnome.shell.extensions.dash-to-dock click-action

gsettings list-keys org.gnome.shell.extensions.dash-to-dock | awk '{print $1}' | xargs -i sh -c "echo '{}:' >> test.txt && gsettings describe org.gnome.shell.extensions.dash-to-dock {} >> test.txt && echo >> test.txt"

### 点击图标最小化
gsettings set org.gnome.shell.extensions.dash-to-dock click-action 'minimize'
