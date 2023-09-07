# Composition API에서 emit 사용법
여러 컴포넌트를 조합하는 경우, 하위 컴포넌트로 데이터를 전달하고 하위 컴포넌트에서 발생한 이벤트를 상위 컴포넌트에서 처리해야 할 때가 있다. 이런 상황에서 Composition API 환경에서 $emit을 사용하여 데이터를 상위 컴포넌트로 전달하는 방법을 알아보자.

<br/><br/>


## 하위 컴포넌트 : 이벤트 발생(Emit event)
### 이벤트 발생 형식
`$emit` 메서드를 사용하여 커스텀 이벤트 생성
```vue
sendData() {
    $emit('이벤트 명', 전달할 데이터);
}
```
### 커스텀 이벤트를 트리거할 시기를 결정
버튼 클릭시, 특정 조건을 충족되었을 때 등
``` vue
<button @click="sendData">Click!</button>
```
### 하위 컴포넌트 전체보기
```vue
import { ref } from 'vue';

<template>
  <button @click="sendData">Click!</button>
</template>

<script>
    export default {
        emits: [customEvent],
        setup(props, {emit}) {
            const message = ref('Hello from Child!');

            const sendData = () => {
                // Emit the custom event 'customEvent' with data
                emit('customEvent', message.value);
            };

            return {
                message,
                sendData,
            };
        },
    };
</script>
```

<br/>

## 상위 컴포넌트 : 이벤트 수신
### 이벤트 수신 형식
`@eventName` 구문을 사용하여 커스텀 이벤트를 수신
```vue
<child-component @이벤트명="상위 컴포넌트의 메서드명"></child-component>
``` 
### 상위 컴포넌트 전체보기
```vue
<template>
  <child-component @customEvent="handleEvent"></child-component>
  <p>{{ receivedData }}</p>
</template>

<script>
    import { ref } from 'vue';
    import ChildComponent from './ChildComponent.vue';

    export default {
        components: {
            ChildComponent,
        },
        setup() {
            //data
            let receivedData = ref("");

            //methods
            const handleEvent = (data) => {
                // Handle the custom event and received data
                receivedData.value = data;
            },
        }
    }
</script>
```