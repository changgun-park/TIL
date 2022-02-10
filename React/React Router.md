### React Router

---



현재 진행 중인 프로젝트는 NextJS를 기반이다. NextJS에서 링크 컴포넌트를 사용해 페이지 라우팅을 구성하고 있는데, 라우터라는 개념을 분명히 배웠음에도 기억이 가물가물하다. 

React를 배울 땐 "클라이언트 사이드" 라우팅이라고는 배웠는데, 그 개념도 확실하지 않고.



이번에는 리액트 라우터가 어떻게 동작하는지, 그리고 NextJS에서는 어떤 차이점이 있는지 알아보겠다.



#### 1. Link(react-router-dom) VS anchor tag

react-router-dom 패키지를 이용하여 라우터를 구성할 때 페이지를 전환하려면 Link 컴포넌트를 사용하게 된다.

아래 코드는 아주 간단한 네비게이션이다.

리스트 아이템이 각각 '/welcome'과 '/products'로 페이지 전환을 하도록 한다.

```javascript
// MainHeader.js

import React from "react";
import { Link } from "react-router-dom";

const MainHeader = () => {
  return (
    <nav>
      <ul>
        <li>
          <Link to="/welcome">Welcome</Link>
        </li>
        <li>
          <Link to="/products">Products</Link>
        </li>
      </ul>
    </nav>
  );
};

export default MainHeader;

```

그런데 다음과 같이, Link를 a태그로 대체하는 것과 무슨 차이가 있을까?

```javascript
import React from "react";
import { Link } from "react-router-dom";

const MainHeader = () => {
  return (
    <nav>
      <ul>
        <li>
          <a href="/welcome">Welcome</Link>
        </li>
        <li>
          <a href="/products">Products</Link>
        </li>
      </ul>
    </nav>
  );
};

export default MainHeader;

```

<strong>a 태그를 사용하면, 서버에 request를 보내고 새로운 html 파일을 받아 페이지에 렌더링하는 과정을 거치게 된다.</strong> 

반면에 Link 컴포넌트를 사용하면, a태그를 생성하지만, a태그의 default behavior인 서버에 request를 보내는 과정을 제거한다. 그 대신, route에 등록된 컴포넌트를 렌더링하게 된다!

```javascript
// App.js

import { Route } from "react-router-dom";
import Welcome from "./pages/Welcome";
import Products from "./pages/Products";
import MainHeader from "./components/MainHeader";

function App() {
  return (
    <div>
      <header>
        <MainHeader />
      </header>
      <main>
        <Route path="/welcome">
          <Welcome />
        </Route>
        <Route path="/products">
          <Products />
        </Route>
      </main>
    </div>
  );
}

export default App;

// our-domain.com/welcome => Component Welcome
// our-domain/products => Component Products
```

첫번째 링크를 클릭하면 url이 '/welcome'으로 바뀌게 된다. 바뀐 url에 따라 서버에 새로운 페이지를 요청하는 것이 아니라, Route 중에서 path가 현재 url과 일치하는 것을 찾아 렌더링하게 되는 것이다.

