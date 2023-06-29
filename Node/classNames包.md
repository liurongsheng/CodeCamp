# classNames包

classnames是一个简单的工具，可以把多个className链接起来，它可以是两个参数以上，类型可以字符串或者对象，如果是字符串，自动合并成多个类名，如果是对象，则只有属性值为true时，类才会显示成功

classNames 函数接受任意数量的参数，这些参数可以是字符串或对象。参数 'foo' 是 { foo: true } 的缩写。如果与给定键关联的值为假值，则该键将不会包含在输出中。

```jsx
classNames('foo', 'bar'); // => 'foo bar'
classNames('foo', { bar: true }); // => 'foo bar'
classNames({ 'foo-bar': true }); // => 'foo-bar'
classNames({ 'foo-bar': false }); // => ''
classNames({ foo: true }, { bar: true }); // => 'foo bar'
classNames({ foo: true, bar: true }); // => 'foo bar'
classNames('foo', { bar: true, duck: false }, 'pig', { bird: true }); // => 'foo bar pig bird'
```

数组将按照上述规则递归平展：

```jsx
const arr = ['b', { c: true, d: false }];
classNames('a', arr); // => 'a b c'
```

[三千字详解 classnames，精读源码](https://juejin.cn/post/7170882996977795086)
