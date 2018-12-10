
前端适配器模块 jar 包地址

`keycloak-4.7.0.Final\modules\system\layers\keycloak\org\keycloak\keycloak-js-adapter\main\keycloak-js-adapter-4.7.0.Final.jar` 解压后可得`keycloak.js`


keycloak 服务端需要新建 clientId, 并进行配置

Access Type: public,
Valid Redirect URIs: http://localhost*,
Web Origins: http://localhost*

```
import keycloak from '../../utils/keycloak'

let instance = new keycloak({ url:userConfig.host+'/auth', realm: 'upaypal-operations', clientId: 'config-center'});
instance.onTokenExpired = function() {
  instance.updateToken();
};
instance.init({
  onLoad: 'login-required'
}).success(function (authenticated) {
  console.log(authenticated)
}).error(function () {
  alert('failed to contact authentication server');
});;
```

