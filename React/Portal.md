## React Portal?

공식 문서에 따르면

```
Portal은 부모 컴포넌트의 DOM 계층 구조 바깥에 있는 DOM 노드로 자식을 렌더링하는 최고의 방법을 제공합니다.
```

이라고 하는데... 설명이 무척 어렵게 느껴진다. :sweat:

예시를 통해 무엇을 의미하는지 알아보자



## 모달 컴포넌트 만들기

다음과 같이 간단히 모달 컴포넌트를 만들어 보았다.

```react
import React from 'react';
import styled from 'styled-components';

const BackDrop = styled.div`
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  z-index: 10;
  background: rgba(0, 0, 0, 0.75);
`;

const ModalBody = styled.div`
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 100;
  overflow: hidden;
`;

const Modal = (props) => {
  return (
    <>
      <BackDrop onClick={props.closeModal} />
      <ModalBody>
        <button onClick={props.closeModal}>close modal</button>
      </ModalBody>
    </>
  );
};

export default Modal;

```

App.js에서 모달이 열려있는지(modalOpen) 상태관리를 하며 렌더링 해준다.

```react
import { useState } from 'react';
import styled from 'styled-components';
import Modal from './components/Modal';

const Wrapper = styled.div`
  margin: auto;
  width: 500px;
  height: 500px;
  display: flex;
  justify-content: center;
  align-items: center;
`;

function App() {
  // 모달이 열려있는지
  const [modalOpen, setModalOpen] = useState(false);

  return (
    <Wrapper>
      {modalOpen && (
        <Modal
          closeModal={() => {
            setModalOpen(false);
          }}
        />
      )}
      <button
        onClick={() => {
          setModalOpen(true);
        }}
        type='button'
      >
        Open Modal
      </button>
    </Wrapper>
  );
}

export default App;
```

