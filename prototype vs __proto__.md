# prototype vs __proto__

### function Person(){} =  var Person = new Function();

### 함수는 객체다. 객체는 프로퍼티를 가질 수 있다.

![Untitled](prototype%20vs%20__proto__%20dbe4d994967b4457b386ab9629d4fc85/Untitled.png)

- 어떤 객체가 자체적으로 가지고 있지 않은 값을 사용하려고 할 때 어떤 데이터를 근거로 해서 어디에서 객체가 가지고 있지 않은 것ex) sum을 찾아낼 수 있는가?

- Person이라고 하는 property와 kim이라고 하는 객체의 생성자 함수를 통해서 만든 객체의 __*proto*__ 가 어떻게 다른가를 설명해보자.