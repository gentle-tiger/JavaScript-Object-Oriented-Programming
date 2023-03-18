# class 상속

JavaScript에서 클래스를 상속해서 서브 클래스를 만드는 방법을 소개합니다.

class에 기능을 추가하는 일은 다양한 외부적 제약(업데이트, 기본세팅의 무거워짐)을 받을 수 있다.

class의 기본 셋팅은 최소한으로 들고 가면서 다른 외부영향과도 부딪히지 않을 수 있는 방법이 상속이다. 

class.js

```jsx
class Person{
    constructor(name, first, second){
        this.name = name;
        this.first = first;
        this.second = second;
    }
    sum(){ 
        return 'prototyoe :'+ (this.first+this.second);
    }
}
class PersonPlus extends Person{    // Person이라는 class를 extends확장한다는 것.
    avg(){
        return  (this.first+this.second)/2;
    }  
}

var kim = new PersonPlus('kim',10, 200);
console.log('kim.sum :', kim.sum());
console.log('kim.avg :', kim.sum());
```

- 여기서 sum은 sum을 사용하는 모든 new Person에 적용되는 값이다. 그래서 sum을 사용하는 객체들에 대해서 `prototype :` 이라는 문자값을 지우고 싶다면 아래의 내용처럼 지우기만 하면 모든 sum을 사용하는 객체들에게 적용된다.

```jsx
    sum(){ 
        return this.first+this.second;
    }
```

```jsx
class PersonPlus extends Person{       
        return (this.first+this.second)/2;
    }
```

- extends
- Person이라는 class를 extends(확장)한다는 것이다. 그렇게 되면 extends Person에 의해서 Person이 가지고 있는  요소들이 그대로 상속된다.

```jsx
답변
1. 상속이란? 
기존에 구현되어 있는 코드를 재활용하여 추가적인 기능유지보수를 하는 것. 

2. 상속이 없으면 불편한 점 ? 
대량의 객체를 만들 때 중복되는 코드들이 발생하여 코드의 품질을 저하시키고 유지보수에 어려움이 생긴다. 

3. extends를 사용해서 자식 클래스를 구현하는 방법은 어떻게 할까? 
기존 class의 Person에 PersonPlus를  extends하여 원하는 기능을 추가하고 유지보수한다. 
```

```jsx
댓글 
1.상속이란, a라는 클래스를 만들었는데, a와 같은 기능을 기반으로 새로운 기능을 추가한 b라는 클래스를 만들고 싶을 때, b클래스에 a에 기능을 모두 다 옮겨 적지 않고, class b(새로 만드는 클래스명) extends a(베이스 클래스) {b에만 새로 추가하고 싶은 기능} 라는 문법을 사용하여 만드는 것을 뜻합니다.

2.상속이 없을 때 불편한 점은, a 클래스를 기반으로 b,c..클래스를 만들 때 기반이 되는 클래스의 기능을 모두 옮겨 적는 중복이 발생하며, 부모 클래스를 수정하면 자식 클래스 모두 수정을 해야하는 번거로움, 즉 유지보수가 어렵다.

3.상속받는 자식 클래스를 구현하는 방법은, class b(새로 만드는 클래스명) extends a(베이스 클래스) {b에만 새로 추가하고 싶은 기능} 라는 문법을 사용하여 만듭니다.
```