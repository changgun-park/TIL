#### Index_Signature



* keyof 연산과 함께 쓸 때 주의 사항

  ```typescript
  type Arrayish = { [n: number]: unknown };
  type A = keyof Arrayish;
  
  type Mapish = { [k: string]: boolean };
  type M = keyof Mapish;
  // type M = string | number
  ```

  Mapish에서 프로퍼티 타입을 string으로 지정했음에도 number까지 포함되는 이유가 뭘까?

  자바스크립트의 객체는 프로퍼티로 문자형, 심볼형을 가질 수 있다. 다른 타입은 문자열로 자동 형 변환된다.

  예를 들어 숫자 0을 넣으면 문자열 '0'으로 자동 변환 된다.

  

  다시 코드로 돌아와서, ```[k: string]```이므로 string 타입은 확실히 포함된다.

  그리고 모든 number 타입은 프로퍼티로 추가되면서 문자형으로 바뀔 수 있기 때문에 number 타입도 함께 포함된다.



* 인덱스 시그니처를 두 개 이상 쓸 때 주의사항

  ```typescript
  interface Animal {
      name: string;
  }
  
  interface Dog extends Animal {
      breed: string;
  }
  
  interface NotOkay {
    	// 'number' index type 'Animal' is not assignable to 'string' index type 'Dog'
      [x: number]: Animal;
      [y: string]: Dog;
  }
  ```

  오류 메세지를 잘 읽어보자. number의 인덱스 타입이 string의 인덱스 타입에 할당 할 수 없다고 한다.

  keyof 연산에서도 봤듯이, 자바스크립트 객체의 프로퍼티는 문자열이나 심볼형이 아니면 자동으로 형변환이 된다.

  따라서, number 프로퍼티의 타입은 반드시 string 프로퍼티 타입의 하위 집합이어야 한다.

  예제는 다음과 같이 Animal과 Dog의 위치를 바꿔야 할 것이다.

  ```typescript
  interface NotOkay {
    	// 'number' index type 'Animal' is not assignable to 'string' index type 'Dog'
      [x: number]: Animal;
      [y: string]: Dog;
  }
  ```

  
