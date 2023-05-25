# nrm

`nrm ls` 报错，提示 `const open = require('open'); Error [ERR_REQUIRE_ESM]: require() of ES Module`

解决方式，指定open的版本，使用 `npm install -g nrm open@8.4.2 --save`

网络上修改 nrm 文件夹下，cli.js 的 17 行，不起作用，不是一个问题
