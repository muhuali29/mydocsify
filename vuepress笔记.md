# vuepress笔记

## 安装npm init vuepress vuepress-starter

### 运行

npm run docs:dev

npm run docs:clean-dev //清除缓存

 如果端口被占用，执行命令npm run docs:dev -- --port 8082  换个端口，默认是8080端口

> netstat -ano |findstr  :8080   查看端口被哪个程序占用，经查被httpd，阿帕奇占用

### 打包命令

npm run docs:build

### 遇到报错提示

出现 `Module not found: Error: Can't resolve 'sass-loader'` 的错误，通常是因为项目中缺少 `sass-loader` 这个依赖。`sass-loader` 是一个用于处理 SCSS/SASS 文件的 Webpack 加载器，它允许你在 Vue.js 项目中使用 SCSS/SASS 语法编写样式。

以下是解决这个问题的步骤：

### 1. 安装 `sass-loader` 和相关依赖

`sass-loader` 依赖于 `node-sass` 或 `sass`（Dart Sass）来编译 SCSS/SASS 文件。你可以选择安装以下依赖之一：

#### 使用 `sass`（推荐，纯 JavaScript 实现，无需额外安装 Python 或 Visual Studio Build Tools

```
npm install sass-loader sass --save-dev
```

### 查看日志

npm install --verbose

## 2.全文搜索slimsearch

### 安装

npm i -D @vuepress/plugin-slimsearch@next

### 中文分词插件nodejs-jieba，配合slimsearch使用

npm install nodejs-jieba    //安装有点慢，有时候会失败，多试几次

### 还需在config.js中配置

```javascript
import { slimsearchPlugin } from '@vuepress/plugin-slimsearch'
import { cut } from 'nodejs-jieba'
slimsearchPlugin({
      // 添加工作线程路径配置
      // workerUrl: '/docs/search-worker.js',
      // placeholder: '搜档',
      // 生命周期钩子
      onSearchBoxMounted: ({ input }) => {
        input.setAttribute('aria-label', '搜索框');
      },
      indexOptions: {
        // 自定义配置项
        fields: ['title', 'content', 'tags'],
        storeFields: ['title', 'path', 'excerpt'],
        // tokenize: 'full',
        // 使用 nodejs-jieba 进行分词
        tokenize: (text, fieldName) =>
          fieldName === 'id' ? [text] : cut(text, true),
      },
      indexContent: true,
      maxSuggestions: 5,
      getExtraFields: (page) => [page.frontmatter.tags], // 将页面的标签加入搜索索引
      searchOptions: {
        limit: 10, // 搜索结果的最大数量
        threshold: 0.2, // 搜索匹配的阈值
      },
      locales: {
        '/': {
          placeholder: '搜档',
        },
      },
    }),
```



### 打包成静态网页，配置项中增加base配置

#### 重要：base值为打包后，放入网站跟目录下的文件夹名

```javascript
  lang: 'zn-CH',
  title: '溧阳妇幼保健院',
  description: '常见问题处理方法',
  // base: '/vuepress-starter/', // 与部署路径一致否则部署时页面错乱
  base: process.env.NODE_ENV === 'production' ? '/vuepress-starter/' : '/',

```



