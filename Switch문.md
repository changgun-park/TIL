### Switch문

---

​	Switch문은 주어진 표현식을 평가하고 그 값과 일치하는 표현식을 갖는 case 문으로 실행 흐름을 옮긴다. 일치하는 case문이 없다면 default문으로 이동한다. default문은 사용할 수도 있고, 사용하지 않을 수도 있다.



```javascript
var month = 2;
var monthName;

switch (month) {
  case 1:
    monthName = "january";
    break;
  case 2:
    monthName = "Feburary";
    break;
  case 3:
    monthName = "March";
    break;
  case 4:
    monthName = "April";
    break;
  case 5:
    monthName = "May";
    break;
  case 6:
    monthName = "June";
    break;
  default:
    monthName = "cannot Find month name";
}

console.log(monthName);

```



위 코드를 분석해보자.

1. 주어진 표현식 month가 2로 평가된다.
2. case 문 중 값이 일치하는 값이 나올 때까지 폴스루(fall through)가 일어난다.
3. case 2의 실행문이 실행된다.
4. break를 통해 switch 문을 빠져나간다.

break를 통해 switch문을 빠져나가지 않으면 폴스루 때문에 default문이 실행된다. 따라서 break 문을 꼭 명시해야한다.



* 웬만한 상황에선 switch문보다는 if...else문을 사용하는 것이 좋다. 하지만, 조건이 너무 많은 경우에는 switch를 쓰는 것이 가독성 측면에서 더 좋을 수도 있다.