### 拿到一个vue+webpack项目，该如何去看，摸索中

~~首先得知道每个文件夹是干啥的吧：~~

1、先看配置文件package.json，里面定义了这个项目所需要的各个模块，以及项目的配置信息。`scripts`指定了运行脚本命令的npm命令行缩写，比如dev指定了运行`npm run dev`时所要执行的命令。

2、我拿到的这个项目在开发环境下通过命令npm run dev来启动的，所以我去package.json文件里找到了scripts配置，其中有设置dev选项，也就是说在运行命令npm run dev时，启动了webpack-dev-server服务，并指定了配置文件webpack.dev.config.js，所以我们接下来就去看webpack.dev.config.js文件。

```js
"scripts": {
    "dev": "webpack-dev-server --inline --progress --config build/webpack.dev.conf.js",
    "start": "npm run dev",
    "unit": "jest --config test/unit/jest.conf.js --coverage",
    "e2e": "node test/e2e/runner.js",
    "test": "npm run unit && npm run e2e",
    "lint": "eslint --ext .js,.vue src test/unit test/e2e/specs",
    "build": "node build/build.js"
  },
```



