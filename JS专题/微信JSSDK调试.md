# 微信JSSDK调试

微信 JS-SDK https://mp.weixin.qq.com/wiki?t=resource/res_main&id=mp1421141115

## npm 包导入 weixin-js-sdk

`npm install weixin-js-sdk`

支持使用 AMD/CMD 标准模块加载方法加载
```
//main/js
const wx = require('weixin-js-sdk');

wx.config({
  debug: false, // 如果是 true 接口得到的数据都输出来
  appId: '',
  timestamp: '必填',
  nonceStr: '必填'',
  signature: '签名',
  jsApiList: [
    'onMenuShareAppMessage',
    'onMenuShareTimeline',
    'showOptionMenu',
    'hideAllNonBaseMenuItem',
    'showAllNonBaseMenuItem',
  ],
});
Vue.prototype.$wx = wx;

// sharePage.vue
  methods: {
    shareFriend() {
      this.$wx.ready(() => {
        const share = {
          title: '分享请好友帮你拆大红包！',
          desc: '大红包',
          imgUrl: '../../assets/img/share_icon.png',
          link: '分享链接（最好是后台JS安全域名）',
          success() {
            // hideMaskLayer(); // 分享成功，隐藏引导用户分享的浮层
            this.$vux.toast.text('微信分享成功！');
          },
          cancel() {
            this.$vux.toast.text('微信分享取消！');
          },
          error() {
            this.$vux.toast.text('微信分享错误！');
          },
        };
        this.$wx.showOptionMenu();
        this.$wx.onMenuShareAppMessage(share); // 微信好友
        this.$wx.onMenuShareTimeline(share); // 朋友圈
      });
      this.$wx.error((res) => { // config信息验证失败会执行error函数
        this.$vux.toast.text(res);
      });
      this.$vux.toast.text('微信分享！');
    },
  }
```

## jweixin-1.4.0.js?390d:1 Uncaught TypeError: Cannot read property 'title' of undefined

jweixin-1.4.0.js里面的执行方式不适合直接webpack。

在执行this.document.title的时候出的问题，这个js期望实在浏览器全局作用域下执行（this指向window），
但是webpack之后，是在一个function作用域下执行，因此this.document为undefined

因此有几种方式修改：

1. 改源码，将jweixin-1.2.0.js中第一个this改为window

2. 在html中使用script引入

3. webpack有个script-loader可以让模块文件在global环境下执行 
