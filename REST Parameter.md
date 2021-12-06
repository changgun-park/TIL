### REST Parameter

---



인자를 모두 더한 값을 리턴하는 함수를 작성해보자.

```javascript
function add() {
  let sum = 0;
  for (var i = 0; i < arguments.length; i++) {
    sum += arguments[i];
  }
  return sum;
}

console.log(add(1));
console.log(add(1, 2));
```

몇 개의 인자를 받을지 사전에 알 수 없으므로, 가변인자 arguments를 활용해야 한다.

<strong>문제는, arguments는 배열이 아니라 object이다. 따라서, 배열 메소드를 사용할 수 없다. </strong>



arguments는 다음과 같이 유사 배열의 형태를 띄고 있다.

```javascript
function lookArguments() {
  console.log(arguments);
}

lookArguments(1, 2, 3); // [Arguments] { '0': 1, '1': 2, '2': 3 }
```



REST 파라미터를 이용하면 이런 문제점을 해결하면서 코드를 작성할 수 있다.

```javascript
function add(...args) {
  let sum = 0;
  for (var i = 0; i < args.length; i++) {
    sum += args[i];
  }
  return sum;
}

console.log(add(1));
console.log(add(1, 2)); // args === [1, 2]
```

REST 파라미터는, 함수의 파라미터로 오는 값을 모아서 하나의 배열에 집어 넣는다.