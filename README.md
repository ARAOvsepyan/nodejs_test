# Вопросы:
1) Разница между var, let и const. Когда и что лучше использовать?
2) Как создать копию объекта, какие способы имеются?
3) Как лучше всего выполнить и обработать множество промисов одновременно?
4) Как в Node.js выполнить HTTP запрос к стороннему ресурсу?
5) Написать функцию, вычисляющую длину последнего слова в строке.

# Ответы:
1) Разница между var, let и const. Когда и что лучше использовать?
- var
  - Глобальная переменная, которая доступна везде. При попытке вызова переменной до ее обьявляения, возвращается undefined.
  - Лучше не использовать, т.к. может привести к ошибкам.
- let
  - Локальная переменная, которая доступна только внутри блока. При попытке вызова переменной до ее обьявляения, возвращается ReferenceError.
  - Лучше использовать вместо var.
- const:
  - Константа, так же доступна только внутри блока, не может быть изменена(TypeError). При попытке вызова переменной до ее обьявляения, возвращается ReferenceError.
  - Лучше использовать вместо let, если переменная не будет изменяться.
2) Как создать копию объекта, какие способы имеются?
- Object.assign({}, obj)
``` js
let obj = {
   a: 1,
   b: 2,
};
let objCopy = Object.assign({}, obj); // { a: 1, b: 2 }
objCopy.b = 3;
console.log(obj, objCopy); // { a: 1, b: 2 } { a: 1, b: 3 }
```
  - При попытке глубокого копирования, необходимо использовать рекурсию.
2) JSON.parse(JSON.stringify(obj))
``` js
let obj = { 
  a: 1,
  b: { 
    c: 2,
  },
}
let newObj = JSON.parse(JSON.stringify(obj));
obj.b.c = 3;
console.log(obj, newObj); // {a: 1, b: {c: 3}} {a: 1, b: {c: 2}}
```
  - Не подходит для копирования функций.
3) Как лучше всего выполнить и обработать множество промисов одновременно?
- Promise.all()
``` js
var p1 = Promise.resolve(1);
var p2 = 2;
var p3 = new Promise((resolve, reject) => {
  setTimeout(resolve, 100, "3");
});

Promise.all([p1, p2, p3]).then(values => {
  console.log(values); // [1, 2, "3"]
});
```
4) Как в Node.js выполнить HTTP запрос к стороннему ресурсу?
- request
``` js
const request = require('request');
request('https://https://dzen.ru', (error, response, body) => {
  console.log('error:', error);                                // Вывод ошибки, если есть 
  console.log('statusCode:', response && response.statusCode); // Вывод кода ответа, если есть
  console.log('body:', body);                                  // Вывод тела ответа
});
```
- axios
``` js
const axios = require('axios');
axios.get('https://https://dzen.ru')
  .then(response => {
    console.log(response); // Вывод ответа
  })
  .catch(error => {
    console.log(error);    // Вывод ошибки, если есть
  });
```
5) Написать функцию, вычисляющую длину последнего слова в строке.
``` js
function lastWordLength(str) {
  return str.split(' ').pop().length;
}
console.log(lastWordLength('Hello world')); // 5
```

