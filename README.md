# docsify的使用

## [快速开始]()

推荐全局安装 `docsify-cli` 工具，可以方便地创建及在本地预览生成的文档。

```bash
npm i docsify-cli -g
```

## [初始化项目](https://docsify.js.org/#/zh-cn/quickstart?id=初始化项目)

如果想在项目的 `./docs` 目录里写文档，直接通过 `init` 初始化项目。

```bash
docsify init ./docs
```

## [开始写文档](https://docsify.js.org/#/zh-cn/quickstart?id=开始写文档)

初始化成功后，可以看到 `./docs` 目录下创建的几个文件

- `index.html` 入口文件
- `README.md` 会做为主页内容渲染
- `.nojekyll` 用于阻止 GitHub Pages 忽略掉下划线开头的文件

直接编辑 `docs/README.md` 就能更新文档内容，当然也可以[添加更多页面](https://docsify.js.org/#/zh-cn/more-pages)。

## [本地预览](https://docsify.js.org/#/zh-cn/quickstart?id=本地预览)

通过运行 `docsify serve` 启动一个本地服务器，可以方便地实时预览效果。默认访问地址 http://localhost:3000 。

```bash
docsify serve docs
```



### 部署至nginx，nginx.conf需如下配置：

```
server {
        listen       80;
        server_name  localhost;

        #charset koi8-r;

        #access_log  logs/host.access.log  main;
        #root 代表根目录
        #try_files  解决页面刷新，却提示404

        location / {
            root   html/docs;
            index  index.html index.htm;
	        try_files $uri $uri/ /index.html;
        }
```

#### 如果我单击左边的目录能正常显示对应的页面，显示后在当前页面刷新，却提示404？



> 这通常是由于单页面应用（SPA）的路由机制和服务器配置不匹配导致的。`docsify` 是一个单页面应用，它使用前端路由来处理页面导航，当你点击目录时，前端路由会更新页面内容而不向服务器发送新的请求。但当你刷新页面时，浏览器会向服务器发送一个新的请求，而服务器可能没有正确配置来处理这些前端路由。
>
> - `root` 指定了 `docsify` 项目的根目录。
> - `index` 指定了默认的索引文件。
> - `location /` 匹配所有请求。
> - `try_files` 指令会按顺序尝试查找请求的文件或目录，如果都找不到，则返回 `/index.html`。

### 三级biaot

# 一级标题

## 二级标题

### 三级标题







