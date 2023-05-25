# nrm

`nrm ls` 报错

- 查看 npm 全局安装路径- - -npm root -g
- 到路径对应的文件夹 `C:\Program Files\nodejs\node_modules\nrm`
- nrm 文件夹下面 `cli.js` 文件
修改 cli.js 文件的第 17 行：
const NRMRC = path.join(process.env.HOME, ‘.nrmrc’);
修改为
const NRMRC = path.join(‘HOMEs’, ‘.nrmrc’);