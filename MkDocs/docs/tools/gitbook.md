# GitBook使用简易指南

>Modern book format and toolchain using Git and Markdown

这是[GitBook项目主页](https://github.com/GitbookIO/gitbook)对它的定义.

>GitBook helps you publish beautiful docs for your users and centralize your teams' knowledge for advanced collaboration. 

这是[GitBook官网](https://www.gitbook.com)对其使用场景的描述.

前几天看到 NJU 的 PA lab, 他们的讲义是用 GitBook 生成并在 GitHub Pages 上托管, 这极大地方便了同学及时地获取最新版本. 回想本人参与的助教工作, 所有资料, 作业, 实验要求的发布均通过 QQ 群完成, 并且发布形式局限于 Word 或 PDF. 和前一种方式相比, 使用 QQ 群发布作业的效率简直低得可怕, 当我们发现错误需要更新时, 必须在QQ群里发布相应的通知, 还会担心有同学没有看到. 另外, 经常修改 PDF 也会导致同学们手里的资料版本混乱. 如果采用 GitBook 托管到 GitHub Pages 的方式, 只需要同学们保持对其正常关注频率便可及时获得更新信息.

简单学习了一下 GitBook 的构建以及如何在 GitHub 上托管, 记录在此. 

## 安装GitBook

首先需要安装 Node.js. 在官网下载即可.

使用 NPM 安装 GitBook: `npm install gitbook -g`

## 项目结构

新建一个 GitHub 仓库, 克隆下来之后在根目录添加 `README.md` 和 `SUMMARY.md` 两个文件, 其中 `README.md` 是对书籍的简单介绍, `SUMMARY.md` 是书籍的目录结构, 内容格式大致如下:

```
* [Chapter1](chapter1/README.md)
  * [Section1.1](chapter1/section1.1.md)
  * [Section1.2](chapter1/section1.2.md)
* [Chapter2](chapter2/README.md)
```

创建这两个文件后使用 `gitbook init` 创建 `SUMMARY.md` 中的目录结构, 之后便可以开始专注于内容的编写.

使用 `gitbook serve` 生成在线预览, 可以刷新浏览器界面实时追踪.

使用 `gitbook build` 编译书籍, 之后可以打包发送或者通过 GitHub Pages 托管.

## 使用 GitHub Pages 托管

我个人习惯是将所有代码放在一个仓库中, 通过不同的分支来管理. 比如 main branch 用于管理生成 GitBook 的源代码, gh-pages branch 用于管理发布到 GitHub Pages 的内容. 如果仓库名为 test, 将网页代码 push 到 gh-pages 分支后可以在 pastglory.github.io/test 访问.

1. 在 GitHub 上新建一个仓库, 假设名为 test.
2. Clone it. (目前是空的)
3. 新建 `README.md` 和 `SUMMARY.md` 两个文件并按格式写好.
4. `gitbook init`.
5. `gitbook build`.
6. 添加 `.gitignore`, 忽略 `_book` 文件夹(编译出来的 site, 不通过 main 分支管理).
7. commit and push 到 main 分支, 通过 main 分支管理生成 book 的源代码.
8. `git checkout --orphan gh-pages` (创建分支).
9. `git rm --cached -r .` (删除不必要的文件).
10. 删除 `_book` 文件夹以外的内容.
11. `cp -r _book/* .`.
12. 添加 `.gitignore`, 忽略 `_book` 文件夹和 `*~` (只管理 site 内容).
13. commit and push 到 gh-pages 分支.
14. 通过 pastglory.github.io/test 访问.

需要注意的是, 在对 git 分支管理不够熟悉的时候, 一定要多使用 `git status` 观察当前的 stage 内容, 以免造成不必要的损失. 为了隐私考虑, 第7步也可以不 push, 仅仅在本地管理源代码. 
同时为了方便开发, 还需要实现简单的脚本, 用于快速推送.

## 使用插件

为了美化 GitBook, 难免会使用各式各样的插件, 经过尝试学习了一种可行的方法, 记录于此.

在上一节的步骤 4 以后, 在根目录下添加 `book.json` 文件 

按照模版格式编辑(现在我用的插件如下)

```
{
    "plugins": [
        "callouts",
        "intopic-toc",
        "page-footer-ex",
        "theme-comscore",
        "-sharing"
    ],
    "title": "测试",
    "pluginsConfig": {
        "page-footer-ex": {
            "copyright": "By lfr",
            "markdown": false,
            "update_label": "此页面修订于",
            "update_format": "YYYY-MM-DD HH:mm:ss"
        }
    }
}
```

之后再 build 即可.