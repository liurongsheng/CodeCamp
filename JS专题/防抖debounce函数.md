# 防抖debounce函数

## 原理

触发事件，但是一定在事件触发 n 秒后才执行，如果在一个事件触发的 n 秒内又触发了这个事件，那就以新的事件的时间为准，
n 秒后才执行，总之，就是要等触发完事件 n 秒内不再触发事件，才执行函数。

## 
```html

<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <title>debounce example</title>
    <!-- <link rel="stylesheet" type="text/css" href="https://unpkg.com/flickity@2/dist/flickity.min.css"> -->
    <!-- <script type="text/javascript" src="https://unpkg.com/flickity@2/dist/flickity.pkgd.min.js"></script> -->
    <style>
        body {
            background: #ccc;
            margin: 0;
            padding: 0;
            border: 0;
        }
        #container {
            width: 100%;
            height: 200px;
            line-height: 200px;
            text-align: center;
            color: #fff;
            background-color: #444;
            font-size: 30px;
        }
    </style>
</head>
<body>
    <div id="container"></div>
    <button id="button">取消防抖</button>
</body>
<script>
var count = 1;
var container = document.getElementById('container');
function getUserAction(e) {
    container.innerHTML = count++;
    console.log(this);
    console.log(e);
};
function getUserAction2() { //配合第五版
    container.innerHTML = count++;
    return "liu"
};
// 第一版 
// 存在this 会指向 Window 对象
function debounce1(func, wait) {
    var timeout;
    return function () {
        clearTimeout(timeout)
        timeout = setTimeout(func, wait);
    }
}
// 第二版 
// 修复this指向 <div id="container"></div>
// 还存在 事件对象 event   
function debounce2(func, wait) {
    var timeout;
    return function () {
        var context = this;
        clearTimeout(timeout)
        timeout = setTimeout(function(){
            func.apply(context)
        }, wait);
    }
}
//<div id="container"></div>

// 第三版
// 修复 事件对象 event 
function debounce3(func, wait) {
    var timeout;

    return function () {
        var context = this;
        var args = arguments;

        clearTimeout(timeout)
        timeout = setTimeout(function(){
            func.apply(context, args)
        }, wait);
    }
}
//MouseEvent {isTrusted: true, screenX: 412, screenY: 244, clientX: 412, clientY: 151, …}

// 第四版 不希望得等到事件停止触发后才执行，我希望立刻执行函数，然后等到停止触发 n 秒后，才可以重新触发执行，添加参数immediate
function debounce4(func, wait, immediate) {
    var timeout;

    return function () {
        var context = this;
        var args = arguments;

        if (timeout) clearTimeout(timeout);
        if (immediate) {
            // 如果已经执行过，不再执行
            var callNow = !timeout;
            timeout = setTimeout(function(){
                timeout = null;
            }, wait)
            if (callNow) func.apply(context, args)
        } else {
            timeout = setTimeout(function(){
                func.apply(context, args)
            }, wait);
        }
    }
}

// 第五版 getUserAction 函数可能是有返回值的，所以我们也要返回函数的执行结果，
// 但是当 immediate 为 false 的时候，因为使用了 setTimeout ，我们将 func.apply(context, args) 的返回值赋给变量，
// 最后再 return 的时候，值将会一直是 undefined，所以我们只在 immediate 为 true 的时候返回函数的执行结果
function debounce5(func, wait, immediate) {
    var timeout, result;

    return function () {
        var context = this;
        var args = arguments;

        if (timeout) clearTimeout(timeout);
        if (immediate) {
            // 如果已经执行过，不再执行
            var callNow = !timeout;
            timeout = setTimeout(function(){
                timeout = null;
            }, wait)
            if (callNow) result = func.apply(context, args) //immediate 为 true 添加返回值
        }
        else {
            timeout = setTimeout(function(){
                func.apply(context, args)
            }, wait);
        }
        return result; //添加return
    }
}
// 第六版 希望能取消 debounce 函数，
// 比如 debounce 的时间间隔是 10 秒钟，immediate 为 true，这样的话，只有等 10 秒后才能重新触发事件，
// 现在希望有一个按钮，点击后，取消防抖，这样再去触发，就可以又立刻执行！
function debounce6(func, wait, immediate) {
    var timeout, result;

    var debounced = function () {
        var context = this;
        var args = arguments;

        if (timeout) clearTimeout(timeout);
        if (immediate) {
            // 如果已经执行过，不再执行
            var callNow = !timeout;
            timeout = setTimeout(function(){
                timeout = null;
            }, wait)
            if (callNow) result = func.apply(context, args)
        }
        else {
            timeout = setTimeout(function(){
                func.apply(context, args)
            }, wait);
        }
        return result;
    };
    debounced.cancel = function() {
        clearTimeout(timeout);
        timeout = null;
    };
    return debounced;
}

// container.onmousemove = getUserAction;
// container.onmousemove = debounce2(getUserAction, 1000);
// container.onmousemove = debounce3(getUserAction, 1000);
// container.onmousemove = debounce4(getUserAction, 1000, 1);
// container.onmousemove = debounce5(getUserAction2, 1000, 1)

var setUseAction = debounce6(getUserAction, 10000, true);//10秒防抖
container.onmousemove = setUseAction;
document.getElementById("button").addEventListener('click', function(){
    setUseAction.cancel();
})
</script>
</html>
```
