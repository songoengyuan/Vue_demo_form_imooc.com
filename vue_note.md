Vue 笔记
===    
>数据驱动、组件化、轻量、简介、高效

* 需求分析
* 脚手架工具
* 数据mock
* 架构设计
* 代码编写
    `架构设计  组件抽象 模块拆分 代码风格更统一 js变量命名规范 css代码规范`  
* 自测
* 编译打包

>功能技术分析

* vue-resource ajax通信
* vue-router
* 最大程度组件化 、html5的localstorage 、图标字体的使用、 移动端像素边框、 css sticky footer布局 、flex弹性布局
* WebbPack 构建工具
* es6 + eslint ： eslint：es6代码风格检查工具

### vue-cli 脚手架工具
https://github.com/vuejs/vue-cli
> * 目录结构
* 本地调试
* 代码部署
* 热加载
* 单元测试 

###### 安装vue cli 
1. 安装node
2. 安装 vue-cli  `$ npm install -g vue-cli`
3. 检查是否安装成功  `$ vue  或  $ vue list `
   例如：
``` 
C:\Users\87790>vue

  Usage: vue <command> [options]

  Options:

    -V, --version  output the version number
    -h, --help     output usage information

  Commands:

    init           generate a new project from a template
    list           list available official templates
    build          prototype a new project
    help [cmd]     display help for [cmd]

C:\Users\87790>vue list

  Available official templates:

  ★  browserify - A full-featured Browserify + vueify setup with hot-reload, linting & unit testing.
  ★  browserify-simple - A simple Browserify + vueify setup for quick prototyping.
  ★  pwa - PWA template for vue-cli based on the webpack template
  ★  simple - The simplest possible Vue setup in a single HTML file
  ★  webpack - A full-featured Webpack + vue-loader setup with hot reload, linting, testing & css extraction.
  ★  webpack-simple - A simple Webpack + vue-loader setup for quick prototyping.
```
4. 开始安装webpack模板 `vue init webpack [name]` name:为项目名字
* 完成安装流程
```

PS D:\workspace\Vue_demo> node -v
v6.11.2
PS D:\workspace\Vue_demo> npm -v
5.6.0
PS D:\workspace\Vue_demo>
PS D:\workspace\Vue_demo> npm install  -g vue-cli
npm WARN deprecated coffee-script@1.12.7: CoffeeScript on NPM has moved to "coffeescript" (no hyphen)
D:\Program Files\nodejs\vue-init -> D:\Program Files\nodejs\node_modules\vue-cli\bin\vue-init
D:\Program Files\nodejs\vue-list -> D:\Program Files\nodejs\node_modules\vue-cli\bin\vue-list
D:\Program Files\nodejs\vue -> D:\Program Files\nodejs\node_modules\vue-cli\bin\vue
+ vue-cli@2.9.3
updated 1 package in 141.128s
PS D:\workspace\Vue_demo>
PS D:\workspace\Vue_demo>
PS D:\workspace\Vue_demo>
PS D:\workspace\Vue_demo> vue

  Usage: vue <command> [options]

  Options:

    -V, --version  output the version number
    -h, --help     output usage information

  Commands:

    init           generate a new project from a template
    list           list available official templates
    build          prototype a new project
    help [cmd]     display help for [cmd]
PS D:\workspace\Vue_demo> vue init

  Usage: vue-init <template-name> [project-name]

  Options:

    -c, --clone  use git clone
    --offline    use cached template
    -h, --help   output usage information
  Examples:

    # create a new project with an official template
    $ vue init webpack my-project

    # create a new project straight from a github template
    $ vue init username/repo my-project

PS D:\workspace\Vue_demo>
PS D:\workspace\Vue_demo>
PS D:\workspace\Vue_demo> vue list

  Available official templates:

  ★  browserify - A full-featured Browserify + vueify setup with hot-reload, linting & unit testing.
  ★  browserify-simple - A simple Browserify + vueify setup for quick prototyping.
  ★  pwa - PWA template for vue-cli based on the webpack template
  ★  simple - The simplest possible Vue setup in a single HTML file
  ★  webpack - A full-featured Webpack + vue-loader setup with hot reload, linting, testing & css extraction.
  ★  webpack-simple - A simple Webpack + vue-loader setup for quick prototyping.

PS D:\workspace\Vue_demo> vue bulid sell
PS D:\workspace\Vue_demo> vue init webpack

? Generate project in current directory? Yes
? Project name sell
? Project description sell app
? Author 宋鹏远 <turingmaster@163.com>
? Vue build standalone
? Install vue-router? Yes
? Use ESLint to lint your code? Yes
? Pick an ESLint preset Standard
? Set up unit tests No
? Setup e2e tests with Nightwatch? No
? Should we run `npm install` for you after the project has been created? (recommended) npm

   vue-cli · Generated "Vue_demo".


# Installing project dependencies ...
# ========================

[ .................] - fetchMetadata: sill pacote range manifest for friendly-errors-webpack-plugin@^1.6.1 fetched i
```

5. 启动服务 `$ npm run dev`
`  Your application is running here: http://localhost:8080 `

6. 目录结构详解
   * [build]  用于存放webpack相关配置文件
   * [config]  主要存放配置文件，用于区分开发环境 测试环境 线上环境的不同
   * [src] 项目源码及需要引用的资源文件
   * [static] 不需要webpack 处理的静态文件
   * [test] 用于存放测试文件
   * .babelrc balel 配置
   * .editorconfig 编辑器配置
    ```
        root = true

        [*]
        charset = utf-8
        indent_style = space //缩进风格
        indent_size = 2
        end_of_line = lf 
        insert_final_newline = true // 文件末尾插入空行
        trim_trailing_whitespace = true // 移除行位对于空格
    ```
    * .eslintignore 忽略语法检查的目录文件
    * .eslintrc.js eslint的配置文件
    ```
        // https://eslint.org/docs/user-guide/configuring

        module.exports = {
            root: true,
            parserOptions: {
                parser: 'babel-eslint'
            },
            env: {
                browser: true,
            },
            extends: [
                // https://github.com/vuejs/eslint-plugin-vue#priority-a-essential-error-prevention
                // consider switching to `plugin:vue/strongly-recommended` or `plugin:vue/recommended` for stricter rules.
                'plugin:vue/essential', 
                // https://github.com/standard/standard/blob/master/docs/RULES-en.md
                'standard' // 预先定义的规则 上面链接可以查看
            ],
            // required to lint *.vue files
            plugins: [
                'vue'
            ],
            // add your custom rules here
            rules: {
                //为零 是忽略这些代码检查 可以手动更改规则
                // allow async-await
                'generator-star-spacing': 'off', // 箭头函数允许不写括号 
                // allow debugger during development
                'no-debugger': process.env.NODE_ENV === 'production' ? 'error' : 'off' // 是否允许在代码中使用debugger
            }
        }

    ```
    * .gitignore git仓库忽略的文件
    * index.html 入口文件
    * package.json 项目配置文件 初始化时填入的信息
    ```
        "scripts": { //我们命令行可以执行的命令  例如 $ npm run dev 
            "dev": "webpack-dev-server --inline --progress --config build/webpack.dev.conf.js",
            "start": "npm run dev",
            "lint": "eslint --ext .js,.vue src",
            "build": "node build/build.js"
        },
         "dependencies": { // 生产环境下的一些依赖
            "vue": "^2.5.2", //'^' 表示最低安装的版本
            "vue-router": "^3.0.1"
        },
        "devDependencies": { // 编译过程的一些依赖
            "autoprefixer": "^7.1.2",
            "babel-core": "^6.22.1",
            "babel-eslint": "^8.2.1",
            "babel-helper-vue-jsx-merge-props": "^2.0.3",
            "babel-loader": "^7.1.1"
        }
    ```
    * README.md 项目描述









