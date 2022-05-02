## 타입스트립트 환경에서 getElementById 사용 시 주의 점



### 오류 상황

리액트로 프로젝트를 하면서 모달 컴포넌트를 만들 때 생각지 못한 부분에서 오류가 났습니다.



아래 코드는 모달 컴포넌트를 [portal](https://velog.io/@pcg0527/React-Portal)을 통해 root가 아닌 다른 요소에 렌더링하고 있습니다.

```react
// 모달 컴포넌트
function TopModal({ children }: ModalProps) {
  // 모달을 닫기 위해 redux로 state 관리
  const dispatch = useRootDispatch()
  const modalOpen = useRootSelector((state) => state.modalOpen);

  // modalRoot : index.html에서 모달이 렌더링될 요소
  // modalNode : BackDrop(배경)과 ModalBody(모달 본체)
  const modalRoot = document.getElementById('modal');
  const modalNode = (
    <BackDrop onClick={() => dispatch(closeModal())}>
      <ModalBody onClick={(e) => e.stopPropagation()}>{children}</ModalBody>
    </BackDrop>
  );

  return modalOpen ? ReactDOM.createPortal(modalNode, modalRoot) : null;
}

export { TopModal };
```



다만, 다음과 같이 오류가 발생합니다.

```bash
Argument of type 'HTMLElement | null' is not assignable to parameter of type 'Element'. Type 'null' is not assignable to type 'Element'
```



### 원인

 <strong>getElementById의 반환 값은 HTMLElement | null 인데, createPortal()은 인자로 Element 타입만을 받기 때문입니다. </strong>



### 해결방법

우리는 분명히 index.html에 id가 modal인 요소를 만들어 놨습니다.

따라서, 이런 경우에 한에서는 [타입 표명(캐스팅)](https://radlohead.gitbook.io/typescript-deep-dive/type-system/type-assertion) 을 적절히 활용해도 괜찮을 것 같습니다.

추가된 부분은 'as HTMLElement' 뿐입니다!



```react
function TopModal({ children }: ModalProps) {
  const dispatch = useRootDispatch();
  const modalOpen = useRootSelector((state) => state.modalOpen);

  // getElementById의 반환 타입이 HTMLElement || null
  // CreatePortal은 null타입을 인자로 받지않으므로 타입캐스팅이 필요
  const modalRoot = document.getElementById('modal') as HTMLElement;
  const modalNode = (
    <BackDrop onClick={() => dispatch(closeModal())}>
      <ModalBody onClick={(e) => e.stopPropagation()}>{children}</ModalBody>
    </BackDrop>
  );

  return modalOpen ? ReactDOM.createPortal(modalNode, modalRoot) : null;
}
```



### 참고자료

[스택오버플로우](https://stackoverflow.com/questions/63520680/argument-of-type-htmlelement-null-is-not-assignable-to-parameter-of-type-el)