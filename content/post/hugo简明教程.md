+++
date = "2019-02-20T19:25:43+08:00"
draft = true
title = "hugo简明教程"

+++


1. 安装hugo
```
    sudo apt install hugo
```

2. 创建新站点
```
    hugo new site www, ps: 子命令： new 新的, 创建类型:site, 创建目标路径: ./www
```

3. 写文章:
```
    hugo new post/first.md

    在后面添加一下内容:

    # Hello. the world!
```

4. 使用主题:
```
    git clone https://github.com/imxood/hugo-theme-slim.git themes/slim
```

5. 启动本地调试:
```
    hugo server --theme=slim --buildDrafts
    ps: --theme=slim 指定使用"slim"主题, "--buildDrafts" 编译草稿, "--watch" 实时刷新页面
```

6. 做一些配置:
```
    vim config.toml

    它的基本内容是:
    baseurl = "http://replace-this-with-your-hugo-site.com/"
    languageCode = "en-us"
    title = "My New Hugo Site"

    修改成你需要的相关信息, 如我的配置:
    baseurl = "http://imxood.github.io"
    languageCode = "en-us"
    title = "分享生活, 分享感动"
```

7. 上传本地站点
```
    hugo --theme=slim --baseUrl="http://imxood.github.io"
```



# 使用Travis Ci持续集成

1. 安装Travis
sudo apt-get install ruby-full
