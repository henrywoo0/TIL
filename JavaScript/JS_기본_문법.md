# JavaScript 기본 문법

### 변수
```javascript
var a = 10 // 변수
let b = 20 // 변수
const c = 30 // 상수 (객체 내용은 바꿀 수 있음)
const str = 'Hello'

let a = 2 + 3
console.log(a)
console.log(a == 5)
```

### 객체
```javascript
const c = {
  name: '강준호',
  emain: 'tteulttak@gmail.com',
  age: 17,
  address: {
    city: 'Daegu',
    state: 'Guji'
  }
}

console.log(c)
console.log(c.name)
console.log(c.address.city)
```

### 배열
```javascript
const list = [1, 2, 3, 4, 5]

console.log(list)
console.log(list[1]) // 인덱스 1은 2번째 요소
```

### 함수
```javascript
function addThree(number) {
  return number + 3;
}

let result = addThree(1)
console.log(result)
```
```javascript
const f = (n) => {
  return n + 3;
}

let result = f(1);
console.log(result);
```

### 템플릿 문자열
```javascript
// 적용 전
let name = 'USER';
let message = 'Hello ' + name;
console.log(message);

// 적용 후
let name = 'USER';
let grade = 'A'
let message = `Hello ${name} (${grade})`;
console.log(message);
```

### if문
```javascript
let a = 0;
if (a < 0) {
  console.log('negative');
} else if (a == 0) {
  console.log('zero');
} else {
  console.log('positive');
}
```

### for문
```javascript
for (let i = 0; i < 5; i++) {
  console.log(i);
}

// 구구단
for (let i = 1; i <= 9; i++) {
  console.log(`2 * ${i} = ${2 * i}`);
}

const arr = [1, 3, 5, 7, 9]

for(let i = 0; i < arr.length; i++) {
  console.log(arr[i])
}

// 향상된 for문
for (let i of arr) {
  console.log(i)
}
```
