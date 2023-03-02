# node 版本管理器 nvm

nvm 是 Node.js 的版本管理器 (version manager)，可在同一台主机上安裝多个版本的 Node.js 环境，通过一个版本管理器来切换不同的 Node.js 版本

// 安装 nvm
npm i -g nvm

// 查看可安装的 node 版本
nvm list available

// 查看已经按照的 node 版本
nvm list

// 安装指定版本的 node
nvm install 14.15.0

// 指定本机运行指定的 node 版本
nvm use 14.15.0

// 卸载指定的 node 版本
nvm uninstall 14.13.1
