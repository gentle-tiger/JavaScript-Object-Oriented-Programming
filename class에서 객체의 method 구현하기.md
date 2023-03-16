# class에서 객체의 method 구현하기

class를 통해서 객체를 생성할 때 모든 객체가 공유하는 공통(prototype)의 객체를 생성하는 방법을 소개한다. 

기존에 constructor function은 이러한 방식으로 구현하였다.

```jsx
function Person(name, first, second, third){
    this.name=name;
    this.first=first;
    this.second=second;   
}
 
Person.prototype.sum = function(){         // sum이라는 함수를 생성자의 prototype으로 정의
    return 'prototype : '+(this.first+this.second);
}                
```

**class에서는 어떻게 구현할까?** 

- class 함수 내에 위치시켜서 사용하는 방법이 있다.
- 여기서 `sum` 은 같은 class에 속해있는 모든 객체가 공유하는 함수가 된다.

```jsx
class Person{
    constructor(name, first, second){
        this.name = name;
        this.first = first;
        this.second = second;
    }
    sum(){
        return 'prototype : '+(this.first+this.second);
    }
}
```

**만약 `kim` 이라는 객체만 다르게 작동시키고 싶다면?** 

- 

```jsx
class Person{
    constructor(name, first, second){
        this.name = name;
        this.first = first;
        this.second = second;
    }
    sum(){
        return 'prototype : '+(this.first+this.second);
    }
}
 
var kim = new Person('kim', 10, 20);
kim.sum = function(){
    return 'this : '+(this.first+this.second);
}                                    
// kim이라는 객체체에 sum이라는 함수를 포함시키면 된다. javascript는 kim이라는 객체에 sum이라는 함수가 있는지 우선적으로 확인하고 실행한다.

var lee = new Person('lee', 10, 10);
console.log("kim.sum()", kim.sum());
console.log("lee.sum()", lee.sum());

결과 
kim.sum() this : 30
lee.sum() prototype : 20
```