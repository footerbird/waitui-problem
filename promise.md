# Promise示例

Promise有各种开源实现，在ES6中被统一规范，由浏览器直接支持

```
// 0.5秒后返回input*input的计算结果:
function multiply(input) {
    return new Promise(function (resolve, reject) {
        console.log('calculating ' + input + ' x ' + input + '...');
        setTimeout(resolve, 500, input * input);
    });
}

// 0.5秒后返回input+input的计算结果:
function add(input) {
    return new Promise(function (resolve, reject) {
        console.log('calculating ' + input + ' + ' + input + '...');
        setTimeout(resolve, 500, input + input);
    });
}

var p = new Promise(function (resolve, reject) {
    console.log('start new Promise...');
    resolve(123);
});

p.then(multiply)
    .then(add)
    .then(multiply)
    .then(add)
    .then(function (result) {
        console.log('Got value: ' + result);
    });

console.log('hello world');
```

打印输出结果

```
start new Promise...
hello world
calculating 123 x 123...
calculating 15129 + 15129...
calculating 30258 x 30258...
calculating 915546564 + 915546564...
Got value: 1831093128
```
