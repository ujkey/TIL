# 제어 컴포넌트와 비제어 컴포넌트 비교
제어 컴포넌트와 비제어 컴포넌트는 데이터 입력을 다루는 방식에 차이가 있다.

<br/><br/>

## 제어 컴포넌트(Controlled Component)
[제어 컴포넌트](https://ko.legacy.reactjs.org/docs/forms.html#controlled-components)는 React의 `state` 를 사용하여 사용자 입력을 제어하고 동기화시키는 방식이다<br/>
사용자 입력은 보통 `onChange` 이벤트 핸들러를 통해 업데이트하고, 그에 따라 화면이 다시 렌더링된다. 주로 사용자의 입력 값이 `state` 와 동기화되어야 할때 사용한다.
이로 인해 React 애플리케이션에서 사용자 입력을 추적하고 관리하기가 용이하며, 폼의 유효성 검사나 제출 처리와 같은 작업을 쉽게 구현할 수 있다.

```jsx
export default function App() {
  const [input, setInput] = useState("");

  const onChange = (e) => {
    setInput(e.target.value);
  };

  return (
    <div className="App">
      <input onChange={onChange} />
    </div>
  );
}
```

<br/>

## 비제어 컴포넌트(Uncontrolled Component)
비제어 컴포넌트는 `state` 를 직접 사용하지 않고, DOM 요소에 직접 접근하여 사용자 입력을 처리한다.<br/>
`state`를 사용하지 않으므로, 실시간으로 동기화 되지 않는다.
비제어 컴포넌트는 사용자가 직접 트리거 하기 전까지는 리렌더링을 발생시키지도 않는다.
주로 외부 라이브러리나 DOM 조작이 필요한 경우, 또는 state를 사용하지 않는 상황에서 사용된다.
```jsx
export default function App() {
  const inputRef = useRef(); // ref 사용

  const onClick = () => {
    console.log(inputRef.current.value);
  };

  return (
    <div className="App">
      <input ref={inputRef} />
      <button type="submit" onClick={onClick}>
        전송
      </button>
    </div>
  );
}
```