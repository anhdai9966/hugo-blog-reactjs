---
weight: 1
title: "Tìm hiểu ES6 qua Tips và Best pratice"
date: 2022-09-27
lastmod: 2022-09-27
draft: false
authors: [CuongPham]
authorLink: "https://dillonzq.com"
description: Tìm hiểu  nhanh ES6 qua Tips và Best pratice"
images: []
resources:
  - name: "featured-image"
    src: "featured-image1.jpg"

tags: ["javascript", "ES6"]
## categories: ["documentation"]

lightgallery: true
math:
  enable: true
toc:
  auto: true
---

Hôm nay mình sẽ giới thiệu về ES6 và chia sẻ cách mà mình hay học một ngôn ngữ mới, hay một bản update của ngôn ngữ một cách nhanh chóng và hiệu quả .Sự thay đổi và cải thiện là cần thiết ở mọi thứ, nhưng tốc độ thay đổi các ngôn ngữ lập trình là rất nhanh đòi hỏi mọi người phải nắm vững căn bản và update hằng ngày.

Riêng mình lại không thích đọc hết toàn bộ docs của nhà phát hành vì có khi nó quá dài mà mình không đủ thời gian và công lực để đọc nên mình luôn chọn shortcut để đi. Và các từ khóa mình chọn sẽ là “best practice”, “tip”, “cheatsheet” + {vấn đề cần tìm}, đây là những bài viết những nội dung đã được tóm tắt và rất dễ đọc dễ hiểu hơn. Và đương nhiên bạn cũng không thể bỏ qua hoàn toàn docs của nhà phát hành nhưng hãy đụng đến nó khi bạn gặp vấn đề phức tạp cần hiểu sâu về cơ chế của mình.
Và sau đây là cách mình tìm hiểu ES6 Vậy trước tiên hãy biết ES6 là gì ES6 là từ viết tắt cuả ECMAScript6 nó là một scripting language ở đời thứ 6 và ra đời năm 2015. Thực tế thì ES6 và javascript là như nhau các bạn có thể sử dụng nó thay thế cho nhau.

## 1. var, let và const

Bên cạnh bé var huyền thoại và độc nhất es6 đã sinh ra 2 bé mới để mọi người có thể chứa giá trị là let và const. Không giống như bé var, scope của let và const không dựa vào top của {} Sử dụng var

```
var snack = 'Meow Mix';

function getFood(food) {
if (food) {
var snack = 'Friskies';
return snack;
}
return snack;
}

getFood(false); // undefined
```

đổi var thành let trong ES6

```
let snack = 'Meow Mix';

function getFood(food) {
if (food) {
let snack = 'Friskies';
return snack;
}
return snack;
}

getFood(false); // 'Meow Mix'
```

Sự thay đổi ở behavior này chỉ ra là bạn cần phải thật cẩn thận khi refactor lại code mà sử dụng var. Một cách mù quáng mà replace tất cả biến var thành let sẽ quăng ra lỗi Note: let và const là block scoped. Vì thế khi bạn tham chiếu đến nó trước khi nó được định nghĩa sẽ quăng ra lỗi.

```
console.log(x); // ReferenceError: x is not defined

let x = 'hi';
```

Best Practice:
Hãy để tất cả biến var ở trong các đoạn “di sản” code để chỉ ra nó cần cẩn thận khi refactor. Và với es6 thì hãy quên var đi và dùng let thay thế cho var khi biến đó có thể đổi giá trị nhiều lần và const cho biến hằng.

## 2. Strings

Trong Es6 đã hỗ trợ thêm cho chúng ta đó là 2 hàm includes() và repeat() cho chuỗi .includes( )

```
const string = 'food';
const substring = 'foo';

console.log(string.includes(substring)); // true
```

.repeat( )

```
// String.repeat(numberOfRepetitions)
'meow'.repeat(3); // 'meowmeowmeow'
```

Template Literals Sử dụng Template Literals, chúng ta có thể nhập một string với các kí tự đặc biệt một cách dễ dàng hơn không cần thông qua kí tự escape
ES5

```
var text = "This string contains \"double quotes\" which are escaped.";
```

ES6

```
let text = `This string contains "double quotes" which don't need to be escaped anymore.`;
```

Template Literals hỗ trợ chúng ta dễ dàng cộng chuỗi với biến giá trị hơn ES5

```
var name = 'Tiger';
var age = 13;
console.log('My cat is named ' + name + ' and is ' + age + ' years old.');
```

ES6:

```
const name = 'Tiger';
const age = 13;

console.log(`My cat is named ${name} and is ${age} years old.`);
```

Ở ES5, chúng ta phải làm như sau để xuống hàng

```
var text = (
'cat\n' +
'dog\n' +
'nickelodeon'
);
```

hoặc:

```
var text = [
'cat',
'dog',
'nickelodeon'
].join('\n');
```

Template literals có thể xuống hàng mà không cần ‘\n’ rất tốt

```
let text = ( `cat dog nickelodeon`
);
```

Template Literals có thể chấp nhận expressions

```
let today = new Date();
let text = `The time and date is ${today.toLocaleString()}`;
```

## 3. Classes

Class của JavaScript ngày xưa

```
function Person(name, age, gender) {
this.name = name;
this.age = age;
this.gender = gender;
}

Person.prototype.incrementAge = function () {
return this.age += 1;
};
```

Class của ES6 bây giờ đã rất giống với các ngôn ngữ lập trình kahsc

```
class Person {
constructor(name, age, gender) {
this.name = name;
this.age = age;
this.gender = gender;
}

    incrementAge() {
      this.age += 1;
    }

}
```

và bạn còn có thể dụng extends keyword:

```
class Personal extends Person {
constructor(name, age, gender, occupation, hobby) {
super(name, age, gender);
this.occupation = occupation;
this.hobby = hobby;
}

    incrementAge() {
        super.incrementAge();
        this.age += 20;
        console.log(this.age);
    }

}
```

## 4. Parameters

Chúng ta có rất nhiều dạng parameter truyền vào function như là default values, indefinite arguments, và named parameters. ES6 Default Parameters

```
function addTwoNumbers(x=0, y=0) {
return x + y;
}
```

Rest Parameters Ở ES5,

```
function logArguments() {
for (var i=0; i < arguments.length; i++) {
console.log(arguments[i]);
}
}
```

ES6 thông qua rest operator chúng ta có thể đưa một số params không biết trước vào

```
function logArguments(...args) {
for (let arg of args) {
console.log(arg);
}
}
```

Named Parameters ES5 xử lý named parameters thông qua options object

```
function initializeCanvas(options) {
var height = options.height || 600;
var width = options.width || 400;
var lineStroke = options.lineStroke || 'black';
}
```

Và ở ES6 chúng ta có thể làm điều đó ngắn gọn hơn rất nhiều

```
function initializeCanvas(
{ height=600, width=400, lineStroke='black'}) {
// Use variables height, width, lineStroke here
}
```

## 5. Maps

Maps là một kiểu dữ liệu rất cầnt thiết trong Javascript. ES6, Bạn có thể tạo ra hash maps qua Object

```
var map = new Object();
map[key1] = 'value1';
map[key2] = 'value2';
```

Maps hỗ trợ chúng ta các hàm như set, get, search

```
let map = new Map();

> map.set('name', 'david');
> map.get('name'); // david
> map.has('name'); // true
```

Và điều ngon nhất là nó không còn chỉ giới hạn string mà mình có thể sử dụng tất cả kiểu ở key và sẽ không bị chuyển(type-cast) thành string

```
let map = new Map([
['name', 'david'],
[true, 'false'],
[1, 'one'],
[{}, 'object'],

```

```
[function () {}, 'function']]);
for (let key of map.keys()) {
console.log(typeof key); // > string, boolean, number, object, function
}
```

Note: Bạn sẽ không dùng map.get được ở các kiểu dữ liệu phức tạp như object và function. Bạn có thể dùng vòng lặp với map qua .entries()

```
for (let [key, value] of map.entries()) {
console.log(key, value);
}
```

## 6. Getter and setter functions

ES6 đã bắt đầu hỗ trợ cho chúng ta getter và setter cùng với class

```
class Employee {

    constructor(name) {
        this._name = name;
    }

    get name() {
      if(this._name) {
        return 'Mr. ' + this._name.toUpperCase();
      } else {
        return undefined;
      }
    }

    set name(newName) {
      if (newName == this._name) {
        console.log('I already have this name.');
      } else if (newName) {
        this._name = newName;
      } else {
        return false;
      }
    }

}

var emp = new Employee("James Bond");

// uses the get method in the background
if (emp.name) {
console.log(emp.name); // Mr. JAMES BOND
}

// uses the setter in the background
emp.name = "Bond 007";
console.log(emp.name);
```

> Các bạn có thể tham khảo thêm các khóa học [tại đây](https://techmaster.vn/)
