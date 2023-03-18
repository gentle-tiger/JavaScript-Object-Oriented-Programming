# super

서브(자식) 클래스에서 상위 클래스를 호출할 때 사용하는 super 키워드를 소개한다. 

기능 도입 → 기능의 장점 + 기능의 복잡성(ex) super 등)

[super - JavaScript | MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/super)

- 부모 클래스가 가지고 있는 기능을 실행할 수 있다.
- 부모가(Person) 가지고 있는 기능과 나도(PersonPlus) 가지고 있는 기능에서 공통적으로 가지고 있는 기능을 제거할 때 사용한다. `super()` 이다.  suer의 사용법은 크게 두 가지이다.

### 1. **super(property)** : 부모 클래스의 생성자를 호출한다.

```jsx
class PersonPlus extends Person{
    constructor(name, first, second,third){
        this.name = name;
        this.first = first;
        this.second = second;
        this.thrid =third;
    }

----------------------------------------↓↓
class PersonPlus extends Person{
    constructor(name, first, second,third){
        super(name,first,second)
        this.thrid =third;
    }
```

<aside>
💡 person 클래스의 부모 클래스의 싱성자가 호출이 되고, 그 생성자 안에 있는 property가 먼저 세팅이 되기 때문에 그 다음에 오는 PersonPlus의 생성자는 "this.third =third"만 해주면 된다.

</aside>

### 2. super : 부모 클래스 그 자체이다.

```jsx
sum(){ 
     return this.first+this.second+this.third;  
}
avg(){
     return  (this.first+this.second+this.third)/2;
}

----------------------------------------↓↓
sum(){ 
    return super.sum()+this.third;
}

avg(){
   return  (super.sum()+this.third)/2;
}

```

부모가 가지고 있는 sum 안의 return 값이 실행되고 그것이 호출되면서 `super.sum()`의 값이 된다. 

---

class.js

```jsx
class Person{
    constructor(name, first, second){
        this.name = name;
        this.first = first;
        this.second = second;
    }
    sum(){
        return this.first+this.second;
    }
}
class PersonPlus extends Person{
    constructor(name, first, second, third){
        super(name, first, second);
        this.third = third;
    }
    sum(){
        return super.sum()+this.third;
    }
    avg(){
        return (this.first+this.second+this.third)/3;
    }
}
 
var kim = new PersonPlus('kim', 10, 20, 30);
console.log("kim.sum()", kim.sum());
console.log("kim.avg()", kim.avg());
```

답변 

```jsx
답변 

1. super는 어떤 용법이 있을까?
부모클래스의 생성자를 호출하는 super()가 있고, 부모클래스 자체를 가져오는 super가 있다. 

2. super가 없다면 어떤 불편함이 있고 super가 있다면 어떤 편리함이 생기는가? 
super를 통해서 부모 클래스가 가지고 있는 생성자의 속성을 중복하지 않고 코드를 구현할 수 있어 코드에 간결함을 주고 재활용성을 높일 수 있다. 

3. 상속이라는 기능으로 인해서 생기는 단점을 어떻게 보완할 수 있는가?
상속을 사용하면 코드의 복잡성이 올라가기 때문에 기능이 다른 코드이지만 부모 클래스의 생성자를 그대로 가져오기 때문에 중복되는 속성의 코드들이 생겨날 수 있다. 이를 super 통해 해결할 수 있다. 
```

댓글

```jsx
super의 용법
1.super() - 부모클래스의 호출 역할, 부모클래스의 property호출
2.super. - 부모의 method 호출 역할 

super가 없다면 코드가 복잡해지고 자식 class와 부모 class의 관계가 무너져 부모 클래스에서 생성한 property method들을 다시한번씩 호출하면서 써야한다.

상속의 개념을 활용한다면 부모에서 받아온 값들을 다시한번 호출해야되는 번거로움을 줄이면서 성능과 메모리를 절약할수 있다.
```