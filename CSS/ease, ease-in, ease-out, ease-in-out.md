### ease, ease-in, ease-out, ease-in-out

---



CSS에서 애니메이션을 구현할 경우, transition과 animation 속성에서 'ease*'값을 줄 때가 있다. 



```css
.Modal {
    transition: all 0.3s ease-in-out;
}
```

```css
.Modal {
	animation: openModal 0.3s ease-in-out forward;
}
```





막연하게 애니메이션을 부드럽게 해준다는 개념만 알고있었는데, 더 이상 헷갈리지 않게 각각의 속성값을 정리 해보겠다.

![css transition](data:image/png;base64,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)



<strong>위 그래프를 보면, 조금 직관적으로 와닿을 것이다.</strong>

가로축이 시간, 세로축이 결과값이다.

설명을 덧붙이자면 다음과 같다.



ease: 천천-빠름-천천

ease-in: 보통-빠르게

ease-out: 보통-느리게

ease-in-out: 천천-보통-천천(ease와 그래프 모양이 같은데, 기울기 변화 속도는 다르다)