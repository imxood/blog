+++
date = "2019-05-14T19:25:43+08:00"
draft = true
title = "linux命令"
+++


# ubuntu 技巧

## 使用gsettings配置Gnome3行为

#### gsettings list-schemas/list-keys/set/get/range

```sh
# 显示所有的scheme用法描述

#!/bin/bash

schemas=$(gsettings list-schemas)

echo "gsettings doc" > test.txt

for schema in $schemas
do
    echo "schema: $schema" >> test.txt
    keys=$(gsettings list-keys $schema)
    for key in $keys
    do
        echo -e "\tkey: $key" >> test.txt
        describe=$(gsettings describe $schema $key)
        echo -e "\tdescribe: $describe\n" >> test.txt
    done
done
```
#### 查看所有的schema
gsettings list-schemas

#### 查看某个schema的所有key
gsettings list-keys org.gnome.shell.extensions.dash-to-dock

#### 查看某个schema的某个key的可选值
gsettings range org.gnome.shell.extensions.dash-to-dock click-action

#### 查看某个schema的某个key的当前值
gsettings get org.gnome.shell.extensions.dash-to-dock click-action


## 常用gsettings配置

#### 点击图标最小化
gsettings set org.gnome.shell.extensions.dash-to-dock click-action 'minimize'

#### 在dock窗口中,滚动轮滑键,切换窗口
gsettings set org.gnome.shell.extensions.dash-to-dock scroll-action 'cycle-windows'
