### Redux 기초

---



1. 리덕스란?

   <strong>리덕스는 리액트의 상태관리 라이브러리이다.</strong>

2. 세 가지 State
   * Local State: 하나의 컴포넌트에서 관리
   * Cross-Component State: 여러 개의 컴포넌트에서 공유. prop을 통해 전달
   * App-Wide State: 전체 어플리케이션에서 사용(혹은 거의 모든 컴포넌트가 사용)



3. React Context 대신 Redux를 사용하는 이유는?

   :cry: Context의 단점 2가지

   * 복잡한 어플리케이션을 개발할 때, Context를 사용하는 것은 유지 보수하기에 너무 어렵다(코드가 지저분 해진다.)
* 성능: Context는 자주 변하는 state에 대응할 때 퍼포먼스가 떨어진다.



4. How Redux Works

   ![리덕스의 작동 방식](https://i0.wp.com/hanamon.kr/wp-content/uploads/2021/07/%E1%84%85%E1%85%B5%E1%84%83%E1%85%A5%E1%86%A8%E1%84%89%E1%85%B3-%E1%84%89%E1%85%A1%E1%86%BC%E1%84%90%E1%85%A2%E1%84%80%E1%85%AA%E1%86%AB%E1%84%85%E1%85%B5-%E1%84%83%E1%85%A1%E1%86%AB%E1%84%80%E1%85%A8.png?resize=919%2C492&ssl=1)

   	* 반드시 <strong>하나의</strong> central store를 가진다.
   	
   	* reducer를 통해서 store의 state를 조작(mutate)한다.
   	* 컴포넌트는 스토어에 바로 접근하여 state를 조작할 수 없다.
   	* 컴포넌트는 action을 dispatch하여 reducer를 통해 state를 조작할 수 있다.



5. Reducer

   Input: state, action

   output: new state

   반드시 <strong>순수 함수</strong>여야만 한다.
   
   ```javascript
   const counterReducer = (state = { counter: 0 }, action) => {
     if (action.type === "increment") {
       return {
         counter: state.counter++,
       };
     } else if (action.type === "decrement") {
       return {
         counter: state.counter--,
       };
     }
   };
   
   // redux toolkit을 사용하면 위와 같이 코드를 작성해도 괜찮다.
   ```



6. Store

   * createStore 메소드에 reducer를 인자로 전달하여 생성한다.

   ```javascript
   const store = redux.createStore(reducer : {counterReducer, authReducer});
   ```

   

7. Subscribe

   * getState() 메소드를 통해 스토어의 state를 가져온다.

   * subscribe()메소드를 통해 state가 변할 때 counterSubscriber가 실행될 수 있도록 전달해준다.

     (구독!)

   ```javascript
   const counterSubscriber = () => {
     const getLatestState = store.getState();
     console.log(getLatestState);
   };
   
   store.subscribe(counterSubscriber)
   ```



8. Dispatch

   * dispatch()에 action 오브젝트를 전달한다.
   * type을 통해 reducer에서 어떤식으로 state를 조작할지 알린다.

   ```javascript
   store.dispatch({ type: "increment" });
   store.dispatch({ type: "decrement" });
   ```

   