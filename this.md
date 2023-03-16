g# this

메소드 내에서 메소드가 속한 객체를 참조 할 때 사용하는 키워드 this

this.js

```jsx
var kim = {
    name:'kim',
    first: 10,
    second: 20,
    sum:function(f,s){
        return f+s;
    }

}
console.log(kim.sum("kim.first, kim.second"),kim.sum(kim.first, kim.second));

결과 
kim.sum(kim.first, kim.second) 30
```

이 코드는 그다지 좋은 코드는 아니다. 

kim이라는 변수는 이미 first와 second의 합이 30이라는 것을 알고 있지만, 호출은 그것을 좋은 방향으로 반영하지 못했다. 

```jsx
sum:function(){
        return kim.first + kim.second;
    }
```

만약 여기서 변수의 이름아 kim에서 k로 바뀐다면 작동할까? 하지 않는다. kim.first라는 것은 이제 없는 코드이기 때문이다. 

`kim.first+kim.second`이 친구들이 자신들이 어떤 변수의 이름을 가져갈지 알 수 없는건 마찬가지다.

객체지향을 만든 사람들은 어떤 함수(메소드)가 있으면 그 함수가 자신이 속해 있는 객체를 가리키는 특수한 키워드를 만들기로 약속한다. 

나는, 저는 처럼말이다. = `this`

```jsx
var kim = {
    name:'kim',
    first: 10,
    second: 20,
    sum:function(){
        return this.first + this.second;
    }

}
// console.log("kim.sum(kim.first, kim.second)",kim.sum(kim.first, kim.second));
console.log("kim.sum(kim.first, kim.second)",kim.sum());
```

이 코드는 잘 동작하는 코드가 된다. 

**<핵심>**

<aside>
💡 **this가 속해 있는 함수(메소드)가 속해 있는 객체를 가리키도록 한 특수한 약속이다.**

</aside>

1. 일반 함수에서 this -> window
2. 중첩 함수에서 this -> window
3. 이벤트에서 this -> 이벤트 객체
4. 메소드에서 this -> 메소드 객체
5. 메소드 내부의 중첩 함수에서 this -> window

this는 그 함수 안에서 객체를 가리키는 특수한 약속이다.