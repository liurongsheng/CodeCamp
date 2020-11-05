# 获取 cookie
用 JavaScript 操作 Cookie 其实是很麻烦的，并不存在一个简单的 API 能让我们获取或者设置 Cookie。
唯一一个操作 Cookie 的 API 是 document.cookie

```javascript
function getCookie(name) {
  const value = `; ${document.cookie}`;
  const parts = value.split(`; ${name}=`);
  if (parts.length === 2) return parts.pop().split(';').shift();
}
```
# Js清空cookie

```javascript
let cookies = document.cookie.split(";");
for (let i = 0; i < cookies.length; i++) {
  let cookie = cookies[i];
  let eqPos = cookie.indexOf("=");
  let name = eqPos > -1 ? cookie.substr(0, eqPos) : cookie;
  document.cookie = name + "=;expires=Thu, 01 Jan 1970 00:00:00 GMT; path=/";
}
if(cookies.length > 0)
{
  for (let i = 0; i < cookies.length; i++) {
    let cookie = cookies[i];
    let eqPos = cookie.indexOf("=");
    let name = eqPos > -1 ? cookie.substr(0, eqPos) : cookie;
    let domain = location.host.substr(location.host.indexOf('.'));
    document.cookie = name + "=;expires=Thu, 01 Jan 1970 00:00:00 GMT; path=/; domain=" + domain;
  }
}
```
