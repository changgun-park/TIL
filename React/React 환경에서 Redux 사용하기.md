### React 환경에서 Redux 사용하기

---



1. redux, react-redux 패키지 설치

   ```bash
   npm install redux, react-redux
   ```

   * react-redux는 react환경에서 redux를 사용하는 것을 상당히 쉽게 해준다!



2. store 셋팅하기

   ```react
   import { createStore } from "redux";
   
   const counterReducer = (state = { value: 0, showCounter: false }, action) => {
     if (action.type === "toggle") {
       return {
         ...state,
         showCounter: !state.showCounter,
       };
     }
     if (action.type === "increment") {
       return {
         ...state,
         value: state.value + 1,
       };
     }
     if (action.type === "decrement") {
       return {
         ...state,
         value: state.value - 1,
       };
     }
     return state;
   };
   
   export const store = createStore(counterReducer);
   
   ```

   * :exclamation: 하면 안되는 것

     ```react
     const counterReducer = (state = { value: 0, showCounter: false }, action) => {
       if (action.type === "increment") {
         // 이런식으로 기존의 state를 변경해서는 안된다.
         state.value++;
         return state;
       }
       ...
     ```

     기존 state를 변경하는 행위는 <strong>절대로</strong> 해서는 안된다.

     항상 새로운 객체를 생성해서 반환해야 한다.

     

2. store Providing

   index.js파일에서 App 컴포넌트를 react-redux의 Provider를 통해 wrapping 해주기

   ```react
   import React from "react";
   import ReactDOM from "react-dom";
   import { store } from "./store";
   import { Provider } from "react-redux";
   import "./index.css";
   import App from "./App";
   
   ReactDOM.render(
     <Provider store={store}>
       <App />
     </Provider>,
     document.getElementById("root")
   );
   ```

   * react-redux의 Provider컴포넌트는 store속성을 가지고 있음
   * 위에서 만들어 두었던 store를 Provider에 전달



4. 컴포넌트에서 redux store의 state에 접근하기

   ```react
   import classes from "./Counter.module.css";
   import { useSelector } from "react-redux";
   import { useDispatch } from "react-redux";
   
   const Counter = () => {
     const showCounter = useSelector((state) => state.showCounter);
     const value = useSelector((state) => state.value);
     const dispatch = useDispatch();
     const toggleCounterHandler = () => {
       dispatch({ type: "toggle" });
     };
   
     const incrementCounterHandler = () => {
       dispatch({ type: "increment" });
     };
     const decrementCounterHandler = () => {
       dispatch({ type: "decrement" });
     };
   
     return (
       <main className={classes.counter}>
         <h1>Redux Counter</h1>
         <div className={classes.value}>{showCounter && value}</div>
         <button onClick={toggleCounterHandler}>Toggle Counter</button>
         <div>
           <button onClick={incrementCounterHandler}>+</button>
           <button onClick={decrementCounterHandler}>-</button>
         </div>
       </main>
     );
   };
   
   export default Counter;
   ```

   * useSelector

     store의 state에 접근하여, state의 특정 속성값을 빼올 수 있다.

     state가 업데이트되면, useSelector를 통해 store의 state를 "구독" 중인 컴포넌트의 코드는 다시 한줄 한줄 읽히고, DOM에 변화가 있으면 다시 렌더링될 것이다. 

     :exclamation: <strong>마치 useState 처럼! </strong>

   * useDispatch()는 redux store의 dispatch 메소드의 참조값을 반환한다.

     dispatch는 action 오브젝트를 인자로 받는다.

