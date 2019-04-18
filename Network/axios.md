# axios.md

form 提交
```
let data = new FormData();
data.append('amount',this.amount);
data.append('paymentCodeNo',this.paymentCodeNo);
let config = {
  headers: {
    'Content-Type': 'multipart/form-data'
    //'Content-Type': 'application/x-www-form-urlencoded'
  }
};

this.$http.post(`${this.$config.host}/${this.url}`, JSON.stringify(data))
  .then((res) => {
    if (res.data.return_code === 'FAIL') {
      this.$vux.toast.text(res.data.content);
    } else if(res.data.return_code === 'SUCCESS') {
      this.$vux.toast.text(res.data.return_msg);
    }
  })
  .catch(error =>
    catchError.call(this, error),
  );
```
json 提交
```
let data = {
  'amount':this.amount,
  'paymentCodeNo':this.paymentCodeNo
};
let config = {
  headers: {
    'Content-Type': 'application/json'
  }
};
this.$http.post(`${this.$config.host}/${this.url}`, data, config)
  .then((res) => {
    if (res.data.return_code === 'FAIL') {
      this.$vux.toast.text(res.data.content);
    } else if(res.data.return_code === 'SUCCESS') {
      this.$vux.toast.text(res.data.return_msg);
    }
  })
  .catch(error =>
    catchError.call(this, error),
  );
```

拦截器
```
axios.interceptors.request.use((config) => { // 请求拦截器，自动添加token
  if (config.method==="get"){
    config.params = {
      _t: Date.parse(new Date())/1000,
      ...config.params
    }
  }
  return config
});
```
