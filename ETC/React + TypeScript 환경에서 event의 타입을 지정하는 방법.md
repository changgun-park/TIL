#### React + TypeScript 환경에서 event의 타입을 지정하는 방법

---



타입스크립트 환경에서 작업을 한다면, 함수 혹은 함수의 매개변수에 반드시 타입을 지정해야 한다.

그렇다면 React를 사용할 때, event를 받는 함수가 있다면, event의 타입은 어떻게 지정해야 할까?



* 답은 바로 event를 매개변수로 받는 함수의 타입을 지정해주는 것이다.

  ```react
  const Navigation: React.FC = () => {
    const [keyword, setKeyword] = useState("");
    const router = useRouter();
  
    
  
    const keywordChangeHandler: React.ChangeEventHandler<HTMLInputElement> =
      function (e) {
        setKeyword(e.target.value);
      };
      
    return (
      
          <form>
            <MagnifyingGlass className={styles.searchIcon} />
            <input
              onChange={keywordChangeHandler}
              value={keyword}
              type="text"
            />
          </form>
          
    );
  };
  
  export default Navigation;
  
  ```

  VScode 환경에서 함수의 타입을 알고 싶다면 이벤트(onChange, onSubmit 등)에 커서를 올려보면 된다.

  함수에 타입을 지정하면, event는 자동으로 필요한 타입을 참조(infer)하게 된다!

