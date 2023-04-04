# 动态计算根元素fontSize值

## 方案一

```js
// common.js 自执行

(function (win, doc) {
  function change() {
    doc.documentElement.style.fontSize =
      `${(doc.documentElement.clientWidth * 50) / 414}px`;
  }
  change();
  win.addEventListener('resize', change, false);
  win.addEventListener('orientationchange', change, false);
}(window, document));
```

`${(doc.documentElement.clientWidth * 50) / 414}px`;

这的 50 代表制作页面时设置 html 根元素的 font-size 的值为 50px，可以自主选择
414 表示使用 iPone 6/7/8 Plus 的尺寸 414*736，可以自主选择

Eslint 严格模式过不去，需要添加规则

```js
'func-names': 0, // 匿名函数
'no-param-reassign': 0, // 修改 doc 
```

如果在 vue 中使用只需要在 main.js 文件中引用 即可
`import './assets/js/common';`

## 方案二

```js
//当前屏幕宽度 / 750 = 当前屏幕宽度的font-size / 100
//代码如下
(function (doc, win) {
    var docEl = doc.documentElement,
    resizeEvt = 'orientationchange' in window ? 'orientationchange' : 'resize',
    reCalc = function () {
      var clientWidth = docEl.clientWidth;
      if (!clientWidth) return;
      docEl.style.fontSize = 100 * (clientWidth / 750) + 'px';
    };
   
    if (!doc.addEventListener) return;
       win.addEventListener(resizeEvt, reCalc, false);
       doc.addEventListener('DOMContentLoaded', reCalc, false);
})(document, window);
```
