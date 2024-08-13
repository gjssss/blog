---
title: 博客插件介绍
date: 2024-08-13T00:00:00.000+08:00
---

博客使用Nuxt3框架搭建，使用Nuxt Content模块渲染和管理Markdown，文章存放于Github`gjssss/blog`仓库中。

插件使用Nuxt Module编写（[仓库]([gjssss/blog-plugins (github.com)](https://github.com/gjssss/blog-plugins))）其中`main`分支为模板分支，其他插件可以由其签出编写
# 编写新插件

## 初始化项目

首先克隆插件仓库
```bash
git clone https://github.com/gjssss/blog-plugins
```
在终端打开仓库后，安装依赖
```bash
cd blog-plugins
pnpm i
```
而后签出分支，名字为你想要编写的插件名字
```bash
git checkout -b my-plugin
```
这样就可以在这个分支下安装你所需要的其他依赖来自定义你的插件了，下面我们不介绍具体的插件编写细节，插件的详情可以看[Nuxt官网]([Module Author Guide · Nuxt Advanced](https://nuxt.com/docs/guide/going-further/modules))

## 配置项目

当插件编写完成后，我们需要发布npm包才能在博客中安装，首先你需要有一个npm的账号，具体注册方法看[NPM官网](https://www.npmjs.com/)，还需要有组织`@blog-plugins-gjs`的权限（不是必须）
而后打开项目中`README.md`文件，可以看到一段注释，这是一段Placeholder
```markdown
<!--
Get your module up and running quickly.

Find and replace all on all files (CMD+SHIFT+F):
- Name: My Module
- Package name: @blog-plugins-gjs/my-module
- Description: My new Nuxt module
-->
```
你只需要用vscode的全局搜索`Ctrl+Shift+F`，将上述名字替换为你的插件名字即可，如我的插件名字为`Account`，npm包名字为`@blog-plugins-gjs/account`，描述为`这是用于记录账户的插件`，则需要全局替换`My Module -> Account` `@blog-plugins-gjs/my-module -> @blog-plugins-gjs/account` `My new Nuxt module -> 这是用于记录账户的插件`即可

## 发布NPM包

当你将项目配置完毕后，即可使用命令发布插件，不过发布前需要先登录你之前创建的npm账号

```bash
npm adduser --registry=https://registry.npmjs.org/
pnpm release
```

当运行结果不报错时即允许完成

## 启用插件

由于插件是作为一个独立的包发布的，所以在Blog项目中需要先安装npm包，以上述Account为例

```bash
pnpm i -D @blog-plugins-gjs/account
```

而后在`nuxt.config.ts`中启用即可

```ts twoslash
export default defineNuxtConfig({
	modules: [
    '@vueuse/nuxt',
    '@unocss/nuxt',
    '@pinia/nuxt',
    '@nuxtjs/color-mode',
    'nuxt-module-eslint-config',
    'nuxt-content-twoslash',
    '@nuxt/content',
    '@blog-plugins-gjs/account', // [!code hl]
  ],
})
```

