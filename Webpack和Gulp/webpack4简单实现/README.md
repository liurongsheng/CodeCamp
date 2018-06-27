###
```
├── dist                      打包输出目录，只需部署这个目录到生产环境
├── package.json              项目配置信息
├── node_modules              npm 安装的依赖包都在这里面
├── src                       我们的源代码
│   ├── components            可以复用的模块放在这里面
│   ├── index.html            入口 html
│   ├── index.js              入口 js
│   ├── shared                公共函数库
│   └── views                 页面放这里
└── webpack.config.js         webpack 配置文件
```

```sh
npm run dev
```

来启动开发环境。

执行

```sh
npm run build
```


编译成功了，我们可以在浏览器打开 `http://localhost:8080/` 看看效果