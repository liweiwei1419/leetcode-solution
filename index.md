# Welcome to MkDocs

For full documentation visit [mkdocs.org](http://mkdocs.org).

## Commands

* `mkdocs new [dir-name]` - Create a new project.
* `mkdocs serve` - Start the live-reloading docs server.
* `mkdocs build` - Build the documentation site.
* `mkdocs help` - Print this help message.

## Project layout

    mkdocs.yml    # The configuration file.
    docs/
        index.md  # The documentation homepage.
        ...       # Other markdown pages, images and other files.

## 搭建这个博客的参考资料

[mkdocs 的所有配置参数（来自 mkdocs 官方中文网站）](http://markdown-docs-zh.readthedocs.io/zh_CN/latest/user-guide/configuration/)

### 自动发布到 GitHub 上
1、在 mkdocs.yml 文件中增加配置 `repo_url` 项（可能连这一步都不用吧，我感觉跟下一步重复了）：
```
repo_url: https://github.com/liweiwei1419/leetcode-solution.git
```
2、在我们的 mkdocs 项目的根目录下初始化 git 项目，并且添加远程 GitHub 仓库的链接：
```
git init
git remote add origin <GitHub 仓库链接>
```
3、执行 `mkdocs gh-deploy` 命令，就可以将 site 目录下的内容发布到 GitHub 仓库的 **gh-pages 分支**；  
4、通过地址 `https://<GitHub 用户名>.github.io/<GitHub 仓库名>/` 可以访问。
例如我的地址就是：[https://liweiwei1419.github.io/leetcode-solution/](https://liweiwei1419.github.io/leetcode-solution/)。
