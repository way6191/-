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
      reject('error message');
    }, 1000);
  });
}).catch((error) => {
  console.log(error);
});

// 结果
1
2
3
error message
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

async function fn4() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      reject('error message');
    }, 1000);
  });
}

async function run() {
  try {
    console.log(await fn1());
    console.log(await fn2());
    console.log(await fn3());
    await fn4();
  } catch (error) {
    console.log(error);
  }
}

run();

// 结果
1
2
3
error message
```

```javascript
const fs = require('fs')
const promisify = require('util').promisify;
const readFile = promisify(fs.readFile)

async function run() {
  try {
    const res1 = await readFile('./1.txt', 'utf8');
    const res2 = await readFile('./2.txt', 'utf8');
    const res3 = await readFile('./3.txt', 'utf8');
    console.log(res1);
    console.log(res2);
    console.log(res3);
    const res4 = await readFile('./不存在.txt', 'utf8');
  } catch (error) {
    console.log(error);
  }

}

run();

// 结果
1
2
3
[Error: ENOENT: no such file or directory, open 'E:\js\不存在.txt'] {
  errno: -4058,
  code: 'ENOENT',
  syscall: 'open',
  path: 'E:\\js\\不存在.txt'
}
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

