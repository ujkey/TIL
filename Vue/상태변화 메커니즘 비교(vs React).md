# React와 Vue의 상태변화 메커니즘 비교

React와 Vue는 모두 상태변화를 감지하여 화면을 업데이트하는 방식을 사용한다. 하지만 두 라이브러리는 상태변화를 감지하는 방식이 다르다. 둘의 차이를 이해하기 전까지, React 유저였던 나는 의도대로 동작하지 않는 Vue가 불편하게 느껴졌다.

<br/><br/>

## 차이점

`React`는 상태변화를 감지하기 위해 `Virtual DOM`을 활용한다. Virtual DOM은 이전 상태와 현재 상태를 비교하여 상태변화를 감지한다. 이 과정에서 원시 타입은 값을 비교하고 객체는 참조값(reference)을 비교한다. 따라서 참조값이 동일하면 React는 상태변화가 없다고 판단하기 때문에 배열의 `상태를 변경할 때는 기존 배열을 복사`하여 새로운 배열을 만들어야 한다. 그렇지 않으면 React는 배열의 변화를 감지하지 못한다.

반면에 `Vue`는 배열의 상태변화를 감지하기 위해 `Observer 패턴`을 사용한다. Observer 패턴은 객체의 상태변화를 감지하기 위해 객체를 감싸는 Proxy를 사용한다. Proxy는 객체에 가해지는 작업을 가로채는 객체이다. 이를 통해 기존 배열을 복사하지 않고도 setter가 발생하는 것을 추적하여 배열에 값을 추가하고 리렌더링 할 수 있다.

<br/>

## Array의 상태 변경으로 비교해보기

### React

빈 배열을 통해 상태를 선언하고, 버튼을 클릭하면 setState로 배열에 값을 추가하는 코드이다.
새로운 배열에 값을 추가할 때마다 재랜더링 하기 위해 기존 배열을 복사하여 새로운 배열을 만들었다.
배열 복사에는 가장 간단한 방법인 spread operator를 사용했다.

```javascript
export default function App() {
  const [list, setList] = React.useState([]);
  const onClick = () => setList([...list, "a"]);

  return (
    <div className="App">
      <h1>List: {list.join(", ")}</h1>
      <button type="button" onClick={onClick}>
        add
      </button>
    </div>
  );
}
```

### Vue - reactive

하지만 Vue에서는 React와 달리 배열을 복사할 필요가 없다. Vue는 Proxy를 통해 배열의 상태변화를 감지하기 때문이다.
따라서 reactive 함수를 통해 배열을 선언하고, push와 같은 메서드를 통해 기존 배열에 값을 추가하면 Vue는 자동으로 배열의 상태변화를 감지하여 재랜더링 한다.

```javascript
<script setup>
    import { reactive } from 'vue'

    // 객체를 Proxy로 감싸는 reactive
    const list = reactive([]);
    const onClick = () => {
        list.push('a')
    }
</script>

<template>
  <h1> List: {{ list.join(', ')  }} </h1>
  <button @click='onClick'>add</button>
</template>
```

<br/>

## reactive로 원시타입의 상태 관라히기

reactive는 객체를 Proxy로 감싸는 함수이기 때문에 원시타입을 인자로 넘기면 리랜더링이 되지 않는다.

```javascript
<script setup>
    import { reactive } from 'vue'
    const msg = reactive("")
</script>

<template>
  <h1>msg = {{ msg }}</h1>
  <input v-model="msg">
</template>
```

### 해결방법

reactive를 사용하여 원시타입의 상태를 관리하려면, 해당 원시타입을 object로 감싸서 reactive의 인자로 전달하면 된다. 이렇게 하면 참조를 가지고 있는 객체가 되어 상태변화를 감지할 수 있게된다.

```javascript
<script setup>
    import { reactive } from 'vue'
    const msg = reactive({value:""})
</script>

<template>
  <h1>msg = {{ msg.value }}</h1>
  <input v-model="msg.value">
</template>
```

<br/>

## Ref

ref를 사용하면 간편하게 원시타입을 상태로 관리할 수 있다. ref는 원시 타입을 감싸는 객체로, value라는 프로퍼티를 가진다. 위의 해결방법과 동일한 것을 알 수 있는데, 실제로 ref의 내부 동작은 reactive와 유사하게 작동한다.<br/>
직접 object로 감싸주는 것보다 편한 점은 Vue의 template 안에서는 msg.value로 접근하지 않고 msg로 사용할 수 있다는 점이다.

> 다만, ref는 Vue3에서 composition API를 사용할 때만 사용할 수 있다

```javascript
<script setup>
    import { ref } from 'vue'
    const msg = ref("")
</script>

<template>
  <h1>msg = {{ msg }}</h1>
  <input v-model="msg">
</template>
```
