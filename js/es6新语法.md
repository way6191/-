### 解构赋值

- 数组

```javascript
let [a, b, c] = [1, 2]
console.log(a)
console.log(b)
console.log(c)

//结果
1
2
undefined
```

- 对象

```javascript
let {name, age, sex} = {name: "zs", age: 18}

console.log(name)
console.log(age)
console.log(sex)

// 结果
zs
18
undefined
```

### 箭头函数中的this指向

- `this`指向外层函数的`this`

```javascript
function fn() {
  console.log(this);
  return () => console.log(this);
}

const retFn = fn.call({name: "zs"});
retFn();

// 结果
{ name: 'zs' }
{ name: 'zs' }
```

### 剩余参数

```javascript
let [a, ...b] = [1, 2, 3]
console.log(a)
console.log(b)

// 结果
1       
[ 2, 3 ]
```

```javascript
function max(...x) {
  return Math.max.apply(Math, x);
}
console.log(max(1, 2, 3));

// 结果
3
```

### 扩展运算符

```javascript
let arr1 = [1, 2, 3];
let arr2 = [4, 5, 6];

console.log([...arr1, ...arr2]);
arr1.push(...arr2)
console.log(arr1);

// 结果
[ 1, 2, 3, 4, 5, 6 ]
[ 1, 2, 3, 4, 5, 6 ]
```

```javascript
// 将伪数组转换成数组
let lis = document.querySelectorAll('li');
let lisArr = [...lis];

console.log(lis);
console.log(lisArr);

// 结果
NodeList(3)
0: li.liactive
1: li
2: li
length: 3
__proto__: NodeList

Array(3)
0: li.liactive
1: li
2: li
length: 3
__proto__: Array(0)
```

### 数组方法

- `Array.from`

```javascript
let a = {
  "0": 1,
  "1": 2,
  "length": 2
}

let arr = Array.from(a, item => item * 2);
console.log(arr);

// 结果	
[ 2, 4 ]
```

- `Array.find`

```javascript
let arr = [{
  id: 1,
  name: "zx"
}, {
  id: 2,
  name: "ls"
}];
let ret = arr.find(item => item.id == 2);

console.log(ret);

// 结果	
{ id: 2, name: 'ls' }
```

- `Array.findIndex`

```javascript
let arr = [{
  id: 1,
  name: "zx"
}, {
  id: 2,
  name: "ls"
}, {
  id: 3,
  name: "ww"
}];
let ret = arr.findIndex(item => item.id > 1);

console.log(ret);

// 结果	
1
```

- `Array.includes`

```javascript
let arr = [1, 2, 3];
let ret = arr.includes(1);

console.log(ret);

// 结果	
true
```

### 模板字符串

```javascript
const fn = () => {
  return `模板字符串可以换行和
`
}
console.log(`${fn()}执行函数`);

// 结果	
模板字符串可以换行和
执行函数
```

### 字符串方法

- `String.startsWith` | `String.endsWith`

```javascript
let s = `hello world`;

console.log(s.startsWith(`hello`));
console.log(s.endsWith(`world`));

// 结果	
true
true
```

- `String.repeat`

```javascript
let s = `<input /><br />`;

console.log(s.repeat(2));

// 结果	
<input /><br /><input /><br />
```

### Set

- 数组重复数据去重

```javascript
const set = new Set(['a', 'a', 'b', 'b']);

console.log([...set]);

// 结果	
[ 'a', 'b' ]
```

- 操作Set

```javascript
const set = new Set();

set.add('a').add('b');
console.log(set);

console.log(set.has('a'));

set.delete('a');
console.log(set);

set.clear();
console.log(set.size);

// 结果	
Set { 'a', 'b' }
true
Set { 'b' }
0
```

- Set遍历

```
const set = new Set(['a', 'a', 'b', 'b']);

set.forEach(item => console.log(item));

// 结果	
a
b
```

