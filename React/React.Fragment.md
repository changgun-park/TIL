### React.Fragment

---



리액트를 사용하다보면, 다음과 같이 '<></>' 혹은 '<React.Fragment><React.Fragment/>'를 사용하는 경우를 자주 볼 수 있다.

```react
import react from 'React'

const App = () => {
    return (
        	<>
    			<div>hi</div>
    			<div>hello<div>
        	</>
            )
}
```



<strong>그렇다면 왜 이렇게 사용해야 할까?</strong>

이유는 에러메세지를 보면 알 수 있다.

```
Adjacent JSX elements must be wrapped in an enclosing tag
```

여러 개의 JSX element를 return 하는 것은, 마치 함수의 반환 값이 여러 개 있는 것과 같다.

따라서, root element에 하나로 담아야 한다.



<strong>그럼, div를 쓰면 안되나?</strong>

div를 쓰게되면, 다음과 같이 불필요한 html 태그를 렌더링하게 될 것이다.

```html
<div>
    <div>
    	<div>
            Unhappy....
        </div>
    </div>
</div>
```



<strong>해결 방법은?</strong>

다음과 같이, children element를 반환하는 컴포넌트를 활용하면 된다.

```react
const Wrapper = (props) => {
	return props.children
}
```

이와 같은 역할을 하는 것이 React Fragment이다.