使用"android": "node node_modules/react-native/local-cli/cli.js run-android",运行时
进度条读取到一半，node弹框自动消失，这个时候无论如何项目都不会成功跑起，最后会红屏显示
```
unable to load script from assets 'index.android.bundle'.
Make sure your bundle ispackged correctly or you are running a packger server.
```

解决方法是进入\android\app\src\main
删除assets文件夹

使用react-native run-android运行项目即可