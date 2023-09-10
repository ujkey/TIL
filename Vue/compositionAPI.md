# composition API

<br/><br/>

## composition API
옵션을 선언하는 대신 가져온 함수를 사용하여 Vue 구성 요소를 작성할 수 있는 API Style<br/>
setup 함수를 사용하여 컴포넌트의 상태 및 메서드를 정의한다<br/>
setup 함수는 컴포넌트가 생성되고 초기화될 때 실행되며, return으로 반환하여 템플릿에서 사용할 수 있다<br/>
```javascript
import { ref, onMounted } from 'vue';
 
export default {
  setup() {
    const count = ref(0);
 
    const increaseCount = () => {
      count.value++;
    };
 
    onMounted(() => {
      console.log('Mounted: ', count.value);
    });
 
    return {
      count,
      increaseCount
    };
  }
};
```
```html
<template>
  <div>
    <button @click="increaseCount">Increase Count</button>
    <p>Count: {{ count }}</p>
  </div>
</template>
```

<br/>

라이프사이클 훅 사용가능
```javascript
setup() {
    onMounted(() => console.log("component mounted"));
    onUnmounted(() => console.log("component onUnmounted"));
    onUpdated(() => console.log("component onUpdated"));
}
```

<br/>

### Reactivity API(ref vs reactive)
데이터를 ref()나 reactive() 메서드로 감싸면 반응형 데이터로 바뀌게 된다<br/>
컴포넌트의 setup() 함수 내에서 선언하고 반환하면 템플릿에서 엑세스 가능

#### ref()
- ref()는 인수를 가져와서 .value 속성이 있는 ref 객체에 래핑하여 반환
- 타입제한 : String, Number, Object 등 모든 원시 타입에서 사용 가능

    ```javascript
    import { ref } from 'vue';

    export default {
        setup() {
            const count = ref(0); //{ value: 0 }

            function increment() {
                count.value++;
            }

            return {
                count,
                increment
            }
        }
    }
    ```

<br/>

#### reactive()
- reactive()는 인수로 받은 객체 자체를 반응형으로 만든다
- 타입 제한 : Object, array, Map, Set과 같은 객체, 배열 및 컬렉션 타입에만 작동
- 반환 값은 원본 객체를 재정의한 Proxy
- Proxy만 반응형이기 때문에, 객체를 Vue의 반응형 시스템으로 작업할 때 상태를 재정의한 Proxy만 사용하자

    ```javascript
    const raw = {}
    const proxy = reactive(raw)
    console.log(proxy === raw) // false
    ```
    ```javascript
    import { reactive } from "vue";

    export default {
        setup() {
            const name = reactive({
                id: 1,
            });

            const updateName = () => {
                name.id = 2;
            };
            return {
                name,
                updateName,
            };
        },
    };
    ```

<br/><br/>

## 2. option API와 비교
### option API
data 객체를 사용하여 컴포넌트의 상태(변수)를 정의하고, methods 객체에 메서드를 작성한다.<br/>
data 객체의 변수들은 Vue 인스턴스 내부에서 this를 통해 접근할 수 있다.
```javascript
export default {
  data() {
    return {
      count: 0
    };
  },
  mounted() {
    console.log('Mounted: ', this.count);
  },
  methods: {
    increaseCount() {
      this.count++;
    }
  }
};
```

<br/>

### 구조
|API Style|설명|
|------|---|
|`option API`|Options에서 data, computed, methods 등 데이터의 변화에 관련된 로직이 각각 흩어져 있다|
|`composition API`|setup() 메서드 안에서 논리점 관점에서 그룹핑한다|

![APIStyles.png](./APIStyles.png) 