# hexo + github pages + next 主题，十分钟学会

## 建一个仓库

- 创建仓库页面

![image-20220117153956920](https://raw.githubusercontent.com/hzzzzzzzq/Blog/feat-picture/asseats/images/hexo/image-20220117153956920.png)

- 仓库名称固定，必须是 username.github.io

![image-20220117154056202](https://raw.githubusercontent.com/hzzzzzzzq/Blog/feat-picture/asseats/images/hexo/image-20220117154056202.png)

- 进入设置页面

![image-20220117154209325](https://raw.githubusercontent.com/hzzzzzzzq/Blog/feat-picture/asseats/images/hexo/image-20220117154209325.png)

![image-20220117154336407](https://raw.githubusercontent.com/hzzzzzzzq/Blog/feat-picture/asseats/images/hexo/image-20220117154336407.png)

- 选择主题之后，就会自动跳转到 readme 的提交页面

![image-20220117154539668](https://raw.githubusercontent.com/hzzzzzzzq/Blog/feat-picture/asseats/images/hexo/image-20220117154539668.png)

- 根据提供给的链接打开网址，我们就可以看到我们选择的主题（这一步其实不重要，因为我们会用别的主题替换）

![image-20220117154713730](https://raw.githubusercontent.com/hzzzzzzzq/Blog/feat-picture/asseats/images/hexo/image-20220117154713730.png)

## 安装并运行 hexo

```bash
# 安装 hexo
$ npm install -g hexo-cli
```

```bash
# 建立文档
# file - 文件路径
$ cd <file>
$ hexo init

# 或者
# 建立的文件路径/以及名称
# desktop/Blog。desktop为路径 Blog 为文件名称
$ hexo init <file>
```

来演示一次。

![image-20220118144154623](https://raw.githubusercontent.com/hzzzzzzzq/Blog/feat-picture/asseats/images/hexo/image-20220118144154623.png)

- 安装依赖

```bash
# file 到文件目录
$ cd <file>

# 安装依赖
$ npm install
```

![image-20220118144310872](https://raw.githubusercontent.com/hzzzzzzzq/Blog/feat-picture/asseats/images/hexo/image-20220118144310872.png)

目录结构

![image-20220118151322761](https://raw.githubusercontent.com/hzzzzzzzq/Blog/feat-picture/asseats/images/hexo/image-20220118151322761.png)

- 本地运行

```bash
$ hexo server
# or
$ hexo s # 简写
```

![image-20220118144332639](https://raw.githubusercontent.com/hzzzzzzzq/Blog/feat-picture/asseats/images/hexo/image-20220118144332639.png)

我们通过 `http://localhost:4000/` 就可以打开页面了，这就是默认页面了。

![image-20220118144408105](https://raw.githubusercontent.com/hzzzzzzzq/Blog/feat-picture/asseats/images/hexo/image-20220118144408105.png)

## 部署到 github pages

部署其实很简单，就是修改 `hexo` 文件的 `_config.yml` 底部的 `deploy` 部署代码。

```yml
# gitname: your github name
# branch: 分支

# 下面注释掉的这种方式在2021年8月起不是很支持，可能会报错
# github: https://github.com/<gitname>/<gitname>.github.io.git
deploy:
  type: git
  repo:
    github: git@github.com:<gitname>/<gitname>.github.io.git
  branch: <branch>
```

- 还需要下载一个自动部署插件

```bash
$ npm install hexo-deployer-git
```

所有上面的东西，部署好之后，就可以进行部署了，我们通过一下 `hexo d` 命令对 `github` 进行部署。

```bash
$ hexo generate
$ hexo deploy
# or
$ hexo g
$ hexo d
# or
$ hexo g -d
```

这时候我们的代码就部署到我们的 `github` 上了。

我们可以直接打开链接看一下 `<gitname>.github.io`，就可以看到我们部署的项目了，与 `hexo s` 运行结果相同。

## next 主题

我们来下载 next 主题

```bash
# 方式一
$ npm install hexo-theme-next@latest

# 方式二
$ git clone https://github.com/next-theme/hexo-theme-next themes/next
$ git pull	#更新
```

使用方法一更好一些，但是如果就更改内容来说，可能方法二比较方便。

我们使用 方法一来实现一次。

![image-20220118151413475](https://raw.githubusercontent.com/hzzzzzzzq/Blog/feat-picture/asseats/images/hexo/image-20220118151413475.png)

我们在修改 `_config.yml` 中的 `theme` 配置

```yml
theme: next
```

然后我们执行命令，并对 github 进行部署。

```bash
$ hexo g -d
```

我们来看看，我们的成果吧。

![image-20220118151655445](https://raw.githubusercontent.com/hzzzzzzzq/Blog/feat-picture/asseats/images/hexo/image-20220118151655445.png)

这时候，我们就已经成功了。

但是有许多配置项可能都还不理解，我们进行分篇幅介绍。

## 相关文章

[hexo 配置项]()

[next 配置项]()
