Geolocation API是通过window.navigator.geolocation获得对地理定位的访问的。

该对象有如下三个方法

* getCurrentPosition(showLocation, ErrorHandler, options);
* watchPosition(showLocation, ErrorHandler, options);
* clearWatch(watchId);

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>geolocationAPI</title>
</head>

<body>
  <div>页面显示navigator.geolocation</div>
</body>
<script>
  if (navigator.geolocation) {
    navigator.geolocation.getCurrentPosition(
      function (position) {
        var latitude = position.coords.latitude;
        var longitude = position.coords.longitude;
        alert("Your position: " + latitude + ", " + longitude);
      },
      function (error) {
        if (err.code == 1) {
          alert("Error: Access is denied!");
        } else if (err.code == 2) {
          alert("Error: Position is unavailable!");
        }
      }
    )
  }
</script>

</html>
```