# NodeLinux 环境

执行安装
```
cd /usr/local
mkdir node
cd node
wget https://nodejs.org/dist/v10.15.3/node-v10.15.3-linux-x64.tar.xz
tar -xvf node-v10.15.3-linux-x64.tar.xz
cd node-v10.15.3-linux-x64
mv * ../
ln -s /usr/local/node/bin/npm /usr/local/bin/
ln -s /usr/local/node/bin/node /usr/local/bin/
```
验证安装：
npm -v
//6.4.1

node -v
// v10.15.3
