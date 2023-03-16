# class

## Classes

클래스 문법에 대한 오리엔테이션이다.

JavaScript ES6부터 포함된 Class 에 대한 소개

[Can I use... Support tables for HTML5, CSS3, etc](https://caniuse.com/)

코드를 작성하면 그것을 모든 웹브라우저에서 사용가능한 과거의 코드로 재구성해준다. 

## Classes의 생성

클래스를 생성하고, 객체를 만드는 방법을 소개합니다.

저번 cnostructor function을 사용하는 방법을 다르게 한다. 

<aside>
💡 class를 통해서 생성자함수를 만들며, 그 속에서 생성자를 함수 안에 초기값은 어떻게 설정하는지 알아보는 것이다. 이번 시간에는 class Person이 객체인지 확인하는 것으로 마무리 하고 다음 시간에 더 구체적으로 알아볼 것이다.

</aside>

class.js ([변경사항](https://github.com/codingeverybody/javascript-object_oriented_programming/commit/40b9ea32b4af71f504855d1fb8cd251eeac6df46))

```jsx
class Person{
 
}
 
var kim = new Person();
console.log('kim', kim);
 
결과 
kim Person {} // 객체가 만들어진 것을 볼 수 있다. 

// kim.sum = function(){
//     return 'this : '+(this.first+this.second);
// }
// var lee = new Person('lee', 10, 10);
// console.log("kim.sum()", kim.sum());
// console.log("lee.sum()", lee.sum());
```