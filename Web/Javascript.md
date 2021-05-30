### Prefix & Postfix

> const a = 6;

```
const output = ++a; // output = a = 7

1: +1 cho a -> a = a + 1 = 7
>> 2: Trả về a sau khi +1
3: Gán output = a = 7;
```

```
const output = a++; // output = 6, a = 7

1: `a copy` = 6
2: +1 cho a => a = a + 1 = 7
>> 3: Trả về `a copy`
4: Gán output = `a copy` = 6
```

```
const output = a++ * 2 - a-- + ++a;

// a++ * 2  -> 6 * 2 = 12, a = 7
// a--      ->          7, a = 6 
// ++a      ->          7, a = 7
```

> x ** y = x<sup>y</sup>

### Convert to Boolean

- 0
- false
- ''
- undefined
- NaN
- null
> 6 giá trị trên -> false
>> còn lại -> true

### Toán tử logical
```
'A' && 1 > 0 && 'C'; // 'C'
'A' && NaN && 'C'; // NaN
Toán tử && chạy từ trái sang phải
nếu gặp kết quả của phép so sánh là "1 trong 6 ký tự false" -> trả về ký tự đó
nếu k gặp -> trả về kết quả của phép so sánh cuối cùng
```

```
'A' || 1 > 0 || 'C'; // 'A'
NaN || 'B' || 'C'; // 'B'
Toán tử || chạy từ trái sang phải, ngược lại
nếu gặp kết quả của phép so sánh là "không thuộc 6 ký tự false" -> trả về ký tự đó
nếu k gặp -> trả về kết quả của phép so sánh cuối cùng
```

### Data Type

1. Primitive Data - Dữ liệu nguyên thuỷ
   - Number
   - String
   - Boolean
   - Undefined
   - Null
   - Symbol   
  
```
    typeof null = object

    const id = Symbol('id); // unique
    const id2 = Symbol('id); // id sẽ khác id2
```

2. Complex Data - Dữ liệu phức tạp
   - Function
   - Object

> *"CPU để xử lý, RAM để lưu trữ giá trị khi phần thực thi"*

1. Primitive:

    let a = 1; 
    tạo ra vùng nhớ địa chỉ x -> lưu giá trị 1,
    không thể sửa lại giá trị ở vùng nhớ x nữa
    
    a = 2; 
    tạo ra vùng nhớ y khác -> lưu giá trị 2

2. Complex:


### Function

>   Delaration function có thể gọi trước khi khai báo (hoisting)

>   còn Expression function thì không

```javascript
    declarationFunc(); // ok

    function declarationFunc () {}

    const expressionFunc = function () {}
    setTimeout(function() {}) // Expression function
    const myObject = {
        expressionFunc: function () {}
    }

    const arrowFunc = () => {}
```

### Object

```javascript
    const ageKey = 'age';

    myObject = {
        name: 'Nhan'
        'e-mail': 'test@mail.com',
        [ageKey]: 18,
        getName: function () {
            return this.name;
        }
    }
    myObject.name = myObject['name'];
    myObject.age = myObject[ageKey];

    delete myObject.age;
```

### Object constructor

```javascript
    function User (firstName, lastName) {
        this.firstName = firstName;
        this.lastName = lastName;

        this.getName = function () {
            return `${this.firstName} ${this.lastName}`;
        }
    }

    const user = new User('Nhan', 'Nguyen');

    /**
     * prototype
     * 
     * dùng để thêm property/method cho constructor
     * 
     * console.log thì thấy nó nằm trong __proto__ 
     * chứ không nằm trên như các property/method đã định nghĩa trong constructor
     * 
     * user.hasOwnProperty(firstName); // true
     * user.hasOwnProperty(age); // false
     * 
     * xem hình để thấy thêm chi tiết
     * */ 

    User.prototype.age = 18;
    User.prototype.getAge = function () {
        return this.age;
    }
```
![alt text](./images/object-constructor-prototype.png)

### Loop
 - for 
 - for/in
 - for/of
 - do/while
 - while
  
```javascript
    for(let i = 0; i < array.length; i++) {}

    // Tránh mỗi lần loop phải đi tính lại array.length thì:
    const arrayLength = array.length;
    for(let i = 0; i < arrayLength; i++) {}

    // key
    for (const property in object) {}
    for (const index in array) {}
    for (const index in string) {}

    // value
    for (const value of array) {}
    for (const element of array) {}
    for (const char of string) {}

    // break, continue

    /**
     * nên for/in để tránh case length > độ dài thực tế
     * 
     * const array = new Array(10);
     * array empty nhưng length = 10
     * 
     * hoặc bị ai đó set lại length
     * array.length = 10;
     * */
```
