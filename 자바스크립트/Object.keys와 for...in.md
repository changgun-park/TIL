# Object.keys와 for...in



### 공통점

Object.keys메소드를 호출하면 객체의 프로퍼티를 열거할 수 있다.

for...in 구문을 사용해도 객체의 프로퍼티를 열거할 수 있다.

```javascript
person = {
  name: 'changgun',
  job: 'developer',
};

console.log(Object.keys(person));

for (const key in person) {
  console.log(key);
}

```



### 차이점

상속받은 프로퍼티를 열거하느냐에 있다.

Object.keys는 상속받은 프로퍼티는 열거하지 않는다.

반면, for...in 구문은 상속받은 프로퍼티도 열거한다.

```javascript
const citizen = {
  nationality: 'korea',
};

const me = {
  name: 'changgun',
  __proto__: citizen,
};

Object.keys(me).forEach((key) => console.log(key)); // name

for (const key in me) {
  console.log(key);
}
/*
name
nationality
*/

```





### 그럼 프로토타입 체인 상의 수 많은 프로퍼티가 다 열거되나?

모든 객체는 프로토타입 체인 상 Object의 자식이다.

그럼에도 for ...in 구문을 통해 Object의 수 많은 프로퍼티가 열거되지 않는 이유는

해당 프로퍼티 어트리뷰트 enumerable이 false이기 때문이다.