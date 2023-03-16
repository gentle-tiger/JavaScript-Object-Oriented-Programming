# class constructor

## class의 constructor function

자바스크립트의 클래스에서 생성자 함수를 구현하는 방법을 소개합니다.

class로 객체를 만들 때, 그 속에 속하는 메소드는 function을 사용하지 않는다. 

객체를 만들기 위한 초기상태를 정의하는 데에 사용하는 것은 **constructor로 정의**한다. 

이것은 약속이다. 

class.js ([변경사항](https://github.com/codingeverybody/javascript-object_oriented_programming/commit/bf08123256fb456720f76a816a0cd4f3484b4b41))

```jsx
**class Person{
    constructor(name, first, second){
        this.name = name;
        this.first = first;
        this.second = second;
    }
}
 
var kim = new Person('kim', 10, 20);
console.log('kim', kim);**
 
// kim.sum = function(){
//     return 'this : '+(this.first+this.second);
// }
// var lee = new Person('lee', 10, 10);
// console.log("kim.sum()", kim.sum());
// console.log("lee.sum()", lee.sum());
```

- 객체가 생성될 때 자동으로 생성되기 전에 실행되도록 약속되어 있는 함수인 constructor함수를 class 내에서 구현하는 방법이다.