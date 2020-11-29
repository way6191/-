### `promise`

- 解决异步嵌套难以阅读问题

```javascript
function fn1() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve(1);
    }, 3000);
  });
}

function fn2() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve(2);
    }, 2000);
  });
}

function fn3() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve(3);
    }, 1000);
  });
}

fn1().then((result) => {
  console.log(result);
  return fn2();
}).then((result) => {
  console.log(result);
  return fn3();
}).then((result) => {
  console.log(result);
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      reject(4);
    }, 1000);
  });
}).catch((error) => {
  console.log(error);
});

// 结果
1
2
3
4
```

### `async`|`await`

- `async`将返回值自动包装成`promise`
- `await`后面接`promise`函数，等待`promise`结果
- `await`必须在`async`函数中使用

```javascript
async function fn1() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve(1);
    }, 3000);
  });
}

async function fn2() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve(2);
    }, 2000);
  });
}

async function fn3() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve(3);
    }, 1000);
  });
}

async function run() {
  console.log(await fn1());
  console.log(await fn2());
  console.log(await fn3());
}

run();

// 结果
1
2
3
```

```javascript
const fs = require('fs')
const promisify = require('util').promisify;
const readFile = promisify(fs.readFile)

async function run () {
  const res1 = await readFile('./1.txt', 'utf8');
  const res2 = await readFile('./2.txt', 'utf8');
  const res3 = await readFile('./3.txt', 'utf8');
  console.log(res1);
  console.log(res2);
  console.log(res3);
}

run();

// 结果
1
2
3
```

```javascript
const fs = require('fs')

function run() {
  const res1 = fs.readFileSync('./1.txt', 'utf8');
  const res2 = fs.readFileSync('./2.txt', 'utf8');
  const res3 = fs.readFileSync('./3.txt', 'utf8');
  console.log(res1);
  console.log(res2);
  console.log(res3);
}

run();

// 结果
1
2
3
```

