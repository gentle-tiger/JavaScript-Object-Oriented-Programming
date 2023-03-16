# prototype

**prototype based language**

JavaScript의 prototype이 필요한 이유와 prototype을 통해서 코드의 재사용성과 성능을 향상시키는 방법을 알려드립니다.

[[Javascript ] 프로토타입 이해하기](https://medium.com/@bluesh55/javascript-prototype-이해하기-f8e67c286b67)

## prototype이 필요한 이유

kim이라는 객체를 생성할 때  Person이라고 하는 함수를 생성자로 동작시켰다. 

다만 , this.sum은 조금 좋지 못했다. 새로운 객체에 sum이라는 이름의 함수가 호출될 때마다 새로 만들어지고 있었다. 메모리 낭비가 되는 것이다.  이는 성능저하의 요소이다. 

생성자 안에서 메소드를 만드는 것이 갖는 단점이다. 이는 생산성 하락으로 이어진다. 

- prototype.js ([변경사항](https://github.com/codingeverybody/javascript-object_oriented_programming/commit/0ee2e0070b1172e5bf65ba32616db859d7a2d13e))

```jsx
function Person(name, first, second, third) {
    this.name=name;
    this.first= first;
    this.second= second;
    this.third= third;
    this.sum = function(){
        return this.first + this.second+this.third;
    }

}

var kim = new Person('kim', 10, 20, 30); 
kim.sum = function(){
 return 'modified : '+ (this.first + this.second+this.third); 
}              // **이러한 코드를 객체마다 일일이 추가해야하는 번거로움이 생긴다**

var lee = new Person('lee', 10, 10, 10); 
kim.sum = function(){
    return 'modified : '+ (this.first + this.second+this.third);
   }

console.log("kim.sum()",kim.sum()); // kim.sum() 60
console.log("lee.sum()",lee.sum()); // lee.sum() 30
```

Person이라고 하는 생성자(}contructor)를 이용해서 만든 모 객체가 공통적으로 사용하는 함수가 있다면? 

## prototyoe을 이용해서 재사용성을 높이기

- 객체들 모두가 공통적으로 사용하는 코드를 만들어보자.

```jsx
function Person(name, first, second, third){
    this.name=name;
    this.first=first;
    this.second=second;   
}
 
Person.prototype.sum = function(){         // sum이라는 함수를 생성자의 prototype으로 정의
    return 'prototype : '+(this.first+this.second);
}                                         // 한번만 정의되기 때문에 효율적으로 변한다. 
 
var kim = new Person('kim', 10, 20);
kim.sum = function(){
    return 'this : '+(this.first+this.second);
}
var lee = new Person('lee', 10, 10);
console.log("kim.sum()", kim.sum());
console.log("lee.sum()", lee.sum());
```

<aside>
💡 JavaScript는 kim이라는 객체에 sum이라는 메소드를 호출할 때, 그 객체 자신이 sum이라는 속성을 가지고 있는지를 우선적으로 찾는다. 그리고 있다면 그것을 실행시키고 종료된다. lee라고 하는 객체는 sum이라는 메소드를 정의한 적이 없기 때문에 lee 객체를 생성하는 생성자인 Person의 prototype이라는 것에 sum이라는 메소드가 정의되어 있는지 찾고 그것을 실행하고 종료된다.

</aside>

변수들은 생성자 안에 넣는 것이 일반적이고, 함수는 특별한 이유가 없다면 prototype을 사용한다. 

내 답변

```elm
1. prototype이란 무엇인가? 
: prototype은 객체를 대량생산 할 때 사용되는 생성자 함수의 효율성을 증대시키는 목적으로 사용된다. 대량의 객체를 생성할 때마다 지속적으로 실행되므로써 발생되는 메모리 사용과 요구사항 변경 시에 재사용하기 힘들다는 단점을 prototype을 사용해서 한번 정의한 것을 모두가 사용할 수 있게끔 하여 코드를 재활용성을 높이고 불필요한 메모리 사용을 차단하는 데에 도움을 준다. 

2. prototype을 사용하지 않고 생성자 안에서 메소드나 속성을 직접적으로 정의하게 되면 어떠한 비효율이 발생하고 그것을 prototype을 통해서 어떻게 극복했는지? 
: 대량의 객체를 만들 때 사용하는 것이 생성자함수(constructor function)이다. 생성자 함수는 대량의 객체를 속성값만 바꿔서 새로운 객체를 만들기 편하다는 장점이 있다. 하지만 적절하지 못한 코드를 구성하게 되면 객체를 생성할 때마다 실행되는 생성자함수로 인해 불필요한 메모리 사용이 발생할 수 있으며, 유지보수에도 많은 노동이 필요하게 된다. 이럴 때 사용하는 것이 prototype이다. 생성자 함수 안에서 반복적으로 실행되는 함수들을 빼내와 prototype을 사용하여 한 번의 정의로 끝낼 수 있게 하여 비효율을 최소화 할 수 있다.  
```

댓글

```elm
1. 프로토타입의 의미란?
: 객체들이 공통으로 사용하는 속성값이다.

2.프로토타입이 없을 떄의 비효율적인 점은 무엇인가? 
:객체를 생성할 떄마다 같은 동작을 하는 중복적인 메소드가 메모리에 계속 생긴다. => 성능 저하, 메모리 낭비 생김.

3. 프로토타입을 사용하면 좋은 점은 무엇인가?
객체들이 공통으로 사용하는 속성값을 정의해서 객체가 생성할때 마다 같은 속성 값을 만드는 과정을 생략해, 성능 향상과 메모리를 효율적으로 이용할 수 있게 해준다.

문법
: 생성자 함수명.prototype.함수명 =  function(){  } 로 한번만 정의.

보충 설명
: 프로토타입은 객체를 정의하는 시점이 아닌, 자신이 필요한 시점에서 정의 할 수 있기때문에 메모리의 이점이 있다. 또한 프로토타입은 생성된 모든 객체가 공통으로 사용할 수 있고 재정의가 가능하기 떄문에 커스터마이징이 가능하다.

예제로 만들어주신 코드에서는 kim.sum 선언문이 Person.prototype.sum 선언문이 보다 아래에 있기 때문에 우선한 것이 아닌가 했는데 직접 순서를 바꿔봐도 kim.sum이 우선되어 적용되네요~
```