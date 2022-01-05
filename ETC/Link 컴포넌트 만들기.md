### Styled-Component Transient Prop

---



리액트, 타입스크립트 환경에서 스타일드 컴포넌트를 이용하여 커스텀 링크 컴포넌트를 만들어 보겠습니다.



* 스타일드 컴포넌트를 import합니다.

* Link 컴포넌트를 import 합니다. DefaultLink라고 다른 이름을 붙여줍니다.

  우리가 만들 놈 이름을 깔끔하게 Link라고 하기 위함입니다.

```react
import styled from 'styled-components';
import { Link as DefaultLink } from 'react-router-dom';
```



* Link라는 새로운 컴포넌트를 만들어 줍니다.

* className의 경우 optional로 타입을 정의해야 합니다.

  왜냐하면, 타입스크립트가 className이라는 Prop이 스타일드 컴포넌트에 의해서 전달된다는 것을 모르기 때문입니다.

* 이런식으로 Link를 재정의하는 이유는 Link 자체를 스타일드 컴포넌트에 넣었을 때 a태그가 지원하지 않는 prop을 전달할 수 있기 때문입니다. 다음 코드에서 설명을 보충하겠습니다.

```react
interface LinkProps {
  to: string;
  className?: string;
  children: string;
}

Link.defaultProps = {
  className: '',
};

function Link({ to, className, children }: LinkProps) {
  return (
    <DefaultLink className={className} to={to}>
      {children}
    </DefaultLink>
  );
}
```



* StyledLink에서 Link 컴포넌트를 스타일링하고 있습니다.

* isActive라는 prop을 추가적으로 받고 있기 때문에 type을 boolean으로 지정해줍니다.

* 만약 위에서 Link를 재정의하지 않고, 'react-router-dom'의 기본 Link를 그대로 가져와 스타일링하게 되면

  a태그에 isActive가 전달됩니다.

```react
const StyledLink = styled(Link)<{ isActive: boolean }>`
  color: black;
  font-size: 1.5rem;
  font-weight: ${(props) => (props.isActive ? '700' : '400')};
  text-decoration: ${(props) => (props.isActive ? 'underline' : 'none')};
`;
```



* 다른 방법으로는 <strong>Transient Prop</strong>을 이용할 수 있습니다. Transient는 '일시적인'이라는 뜻입니다. styled component에만 전달하고, DOM 요소에 주입되는 것을 막으려면 Transient Prop을 사용하면 됩니다.
* 간단하게 '$'를 붙여주면 됩니다. 적용한 코드는 다음과 같습니다.

```react
import React from 'react';
import styled from 'styled-components';
import { Link } from 'react-router-dom';

const StyledLink = styled(Link)<{ $isActive: boolean }>`
  color: black;
  font-size: 1.5rem;
  font-weight: ${(props) => (props.$isActive ? '700' : '400')};
  text-decoration: ${(props) => (props.$isActive ? 'underline' : 'none')};
`;

export default StyledLink;
```



* CSS Helper를 이용하여 조금 더 깔끔하게 코드를 구성해보았습니다.

```react
import styled, { css } from 'styled-components';
import { Link } from 'react-router-dom';

interface StyledLinkProps {
  $isActive: boolean;
}

const activeStyle = ({ $isActive }: StyledLinkProps) => {
  if ($isActive) {
    return css`
      font-weight: 700;
      text-decoration: underline;
    `;
  }
  return css`
    font-weight: 400;
    text-decoration: none;
  `;
};

const StyledLink = styled(Link)<StyledLinkProps>`
  color: black;
  font-size: 1.5rem;
  ${activeStyle}
`;

export default StyledLink;
```

