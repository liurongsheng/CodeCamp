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