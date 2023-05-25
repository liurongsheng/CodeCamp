# pnpm

两个版本

- pnpm 是 pnpm 的普通版本，需要 Node.js 才能运行 `npm install -g pnpm`

- @pnpm/exe 与 Node.js 一起打包到可执行文件中，因此它可以在没有安装 Node.js 的系统上使用 `npm install -g @pnpm/exe`

在 PowerShell: `iwr https://get.pnpm.io/install.ps1 -useb | iex`

## 设置别名

在具有管理员权限的 Powershell 窗口中，执行：

`notepad $profile.AllUsersAllHosts`

在打开的 profile.ps1 文件中，输入：

`set-alias -name pn -value pnpm`

保存文件并关闭窗口。可能需要关闭任何打开的 Powershell 窗口才能使别名生效

## 命令

- `pnpm add -g pnpm` 自更新
- `pnpm ls -g` 列出每个全局的包
