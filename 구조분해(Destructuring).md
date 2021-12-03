### 구조분해(Destructuring)

---



구조분해를 사용하면 배열이나 객체의 요소를 효율적으로 추출할 수 있다. 

```javascript
var arr1 = [1, 2, 3];
var [a, b] = arr1;

console.log(a); // 1
console.log(b); // 2
```



다양한 방식으로 활용이 가능하다.

```javascript
var arr1 = [1, 2, 3, 4, 5, 6];
var [a, b, ...rest] = arr1

console.log(a); // 1
console.log(b); // 2
console.log(rest); // [3, 4, 5, 6]
```

