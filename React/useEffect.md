### useEffect

---



#### 1. Side Effect란 무엇인가?

useEffect는 React의 side Effect를 관리하기 위해 탄생한 hook이다.

side Effect를 이해하기 위해서는 side Effect가 아닌 것, 즉 React의 주요 임무(main job)를 먼저 짚어야한다.

React의 주요 임무는 <strong>화면에 UI를 state 변화에 따라 렌더링하고, 사용자와의 상호작용을 감지하는 것이다.</strong>

 즉, JSX코드를 평가, 렌더링 / state와 prop 관리 / 사용자의 인풋, 이벤트에 반응 / 컴포넌트 재평가가 React의 main job이라고 할 수 있다.

<strong>Side Effect는 이를 제외한 모든 것들이다.</strong>

http request를 보내거나, 브라우저 스토리지에 데이터를 저장하거나, 타이머를 만드는 등이 포함된다.



#### 2. useEffect

useEffect는 콜백 함수와 의존성 배열을 매개변수로 가진다.

```react
useEffect(() => { ... }, [dependencies])
```

콜백함수는 의존성 배열에 포함된 요소에 변화가 있으면 실행된다.

빈 배열을 전달하면, 컴포넌트가 처음 렌더링 된 뒤에 한 번만 실행된다.

배열을 전달하지 않으면, 매 렌더링 마다 실행된다.



#### 3. cleanUp Function

useEffect는 return문을 가질 수 있다.

return문은 함수 형태로 작성해야 한다.

해당 함수는 useEffect가 처음 실행될때(첫번째 렌더링 이후)를 제외하고 useEffect가 실행될 때마다 useEffect의 코드 이전에 먼저 실행된다.

<strong>컴포넌트가 unmount될 때도 실행된다.</strong>



#### 4. 예시

간단한 인풋을 받고, 유효성을 검사하는 부분을 useEffect를 통해 처리하고 있다.

```react
import React, { useState, useEffect, useRef } from 'react';
import './App.css';

function App() {
  const [inputValue, setInputValue] = useState('');
  const [inputValidity, setInputValidity] = useState(null);
  const firstRender = useRef(0);

  function inputChangeHandler(e) {
    setInputValue(e.target.value);
  }

  useEffect(() => {
    // 첫번째 렌더인 경우에는 PASS
    if (firstRender.current === 0 || firstRender.current === 1) {
      firstRender.current += 1;
      return;
    }
    // 유효성 검사
    // setTimeout은 timeoutID를 반환하여, 생성한 타이머를 식별할 수 있다.
    const identifier = setTimeout(() => {
      console.log('check');
      setInputValidity(inputValue.includes('valid'));
    }, 500);

    // 클린업
    // useEffect가 실행되기 전 먼저 실행된다.
    // useEffect가 처음 실행될 때는 실행되지 않는다.
    return () => {
      clearTimeout(identifier);
    };
  }, [inputValue]);

  return (
    <div>
      <input type='text' value={inputValue} onChange={inputChangeHandler} />
      <p>{inputValidity === false ? 'input is invalid' : ''}</p>
    </div>
  );
}

export default App;
```



