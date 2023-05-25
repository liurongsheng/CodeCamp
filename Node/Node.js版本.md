# Node.js版本

[Node.js 对 各个 ECMAScript 支持情况](https://node.green/)

[ECMAScript版本信息](/JS%E4%B8%93%E9%A2%98/ECMAScript.md)

## path

path 模块用于处理文件与目录的路径

- path.normalize(path) // 规范化 path，并处理 '..' 和 '.' 片段
- path.join([...paths]) // 使用平台特定的分隔符把所有 path 片段连接到一起，并规范化生成的路径，会调用 path.normalize(path)
- path.resolve([...paths]) // 将路径或路径片段处理成绝对路径
- path.basename(path[, ext]) // 返回 path 文件名，ext 拓展名
- path.dirname(path) // 返回 path 的目录名
- path.extname(path) // 返回 path 的扩展名

- path.parse(path) // 返回一个对象
- path.format(pathObject) // 将一个对象格式化为一个路径字符串

- path.sep // 返回平台特定的路径片段分隔符
- path.delimiter // 返回平台特定的路径分隔符
- path.win32 // 返回为 Windows 实现的 path 方法
- path.posix // 返回为 POSIX 实现的 path 方法

```node
path.resolve('/foo/bar', './baz');
// 返回: '/foo/bar/baz'

path.resolve('/foo/bar', '/tmp/file/');
// 返回: '/tmp/file'

path.resolve('wwwroot', 'static_files/png/', '../gif/image.gif');
// 如果当前工作目录是 /home/myself/node，则返回 '/home/myself/node/wwwroot/static_files/gif/image.gif'

path.parse('/home/user/dir/file.txt');
// 返回:
// { root: '/',
//   dir: '/home/user/dir',
//   base: 'file.txt',
//   ext: '.txt',
//   name: 'file' }
```
