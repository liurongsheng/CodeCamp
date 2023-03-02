# Base64编码与解码

将ASCII字符转换成普通文本, 是网络上最常见的用于传输8Bit字节代码的编码方式之一

base64由字母a-z、A-Z、0-9以及+和/, 再加上作为垫字的=, 一共65字符组成一个基本字符集, 其他所有字符都可以根据一定规则, 转换成该字符集中的字符

在日常开发中, 最常见的便是将blob和base64之间相互转换

```js
// blob to base64
function blobToBase64(blob) {
  return new Promise((resolve, reject) => {
    const reader = new FileReader();

    reader.onloadend = () => {
      resolve(reader.result);
    };

    reader.onerror = reject;

    reader.readAsDataURL(blob);
  });
}
// base64 to blob
function dataURItoBlob(dataURI) {
  var mimeString = dataURI
    .split(',')[0]
    .split(':')[1]
    .split(';')[0] // mime类型
  var byteString = atob(dataURI.split(',')[1]) //base64 解码
  var arrayBuffer = new ArrayBuffer(byteString.length) //创建ArrayBuffer
  var intArray = new Uint8Array(arrayBuffer) //创建视图
  for (var i = 0; i < byteString.length; i++) {
    intArray[i] = byteString.charCodeAt(i)
  }
  return new Blob([intArray], { type: mimeString }) // 转成 blob
}
```

## 在 HTML5 中新增了 atob 和 btoa 方法来支持 Base64

- atob：将 base64 转成 8bit 字节码
- btoa：将 8bit 字节码转成 base64

window.btoa()：对 base-64 编码的字符串进行解码
[MDN地址：window.btoa()](https://developer.mozilla.org/zh-CN/docs/Web/API/WindowBase64/btoa)

let encodedData = window.btoa(stringToEncode);

- stringToEncode，一个字符串, 其字符分别表示要编码为 ASCII 的二进制数据的单个字节。
- 返回值，一个包含 stringToEncode 的 Base64 表示的字符串

```js
let encodedData = window.btoa("Hello, world"); // base64 编码
let decodedData = window.atob(encodedData); // 解码 成 ASCII
```

window.atob()：对 base-64 编码的字符串进行解码
[MDN地址：window.atob()](https://developer.mozilla.org/zh-CN/docs/Web/API/WindowBase64/atob)

对于不提供 window.btoa 和 window.atob 的浏览器的 Polyfill

<https://github.com/davidchambers/Base64.js#readme>

```js
// 依赖
"dependencies": {
    "Base64": "^1.0.1",
}
// 在项目 index.js 中引用
if (typeof global.btoa === 'undefined') {
    const Base64 = require('Base64')
    global.atoa = Base64.atob
    global.btoa = Base64.btoa
}
```
