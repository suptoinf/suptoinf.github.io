---
layout: default
---

# Contents
[使用github.io和Jekyll搭建个人主页](#github-page)

<a id="github-page"></a>
# 使用github.io和Jekyll搭建个人主页

## 建立github.io仓库

在github中建立仓库，仓库名为`<username>.github.io`，github会自动生成页面

## 使用Jekyll初始化页面

1. 安装Jekyll(Fedora)
    ```shell
    sudo dnf install ruby ruby-devel openssl-devel redhat-rpm-config gcc-c++ @development-tools
    gem install jekyll bundler
    ```

2. 建立站点并测试

    (1) 在github.io项目根目录中使用`jekyll new`命令
    ```shell
    jekyll new --skip-bundle .
    ```

    (2) 修改Jekyll创建的`Gemfile`文件，注释`gem "jekyll"`，并取消注释`gem "github-pages"`
    ```Gemfile
    # gem "jekyll", "~> 4.4.1"
    gem "github-pages", group: :jekyll_plugins
    ```

    (3) 运行`bundle install`

    (4) 本地测试
    ```shell
    bundle exec jekyll serve
    ```

3. 更换主题

    (1) 将主题提供的名称添加进`_config.yml`，如：
    ```yml
    remote_theme: pages-themes/architect@v0.2.0
    plugins:
    - jekyll-remote-theme
    ```

    (2) 字体配置

    新建`assets/css/style.scss`文件，添加如下内容，按给定的顺序查找并使用字体
    ```scss
    ---
    ---

    @import "{{ site.theme }}";

    body {
        font-family: "PingFang SC", "Hiragino Sans GB", "Microsoft YaHei", "WenQuanYi Micro Hei", sans-serif;
    }

    ```

    遇到的问题：更换主题后，原有主题的layout不识别。默认主题`Minima`有`page`、`post`等layout配置，而新主题未提供。解决方法，将所有页面的layout更换为`default`

## 参考
[Creating a GitHub Pages site with Jekyll](https://docs.github.com/zh/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll)
