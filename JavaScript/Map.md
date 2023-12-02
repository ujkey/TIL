# Map

<br/><br/>

## 1. Map?

자바스크립트의 Map은 `키-값` 쌍을 저장하는 자료구조로, `해시 테이블`을 구현하는데 사용된다.<br/>
저장 순서를 보장한다

<br/>

### 생성

Map 객체 생성자 사용

```javascript
const myMap = new Map();
```

<br/>

### 값 추가

set 메소드를 사용하여 맵에 값을 추가

```javascript
myMap.set("key1", "value1");
myMap.set("key2", "value2");
```

<br/>

### 값 얻기

get 메소드를 사용하여 세트에서 값 얻기

```javascript
const value = myMap.get("key1"); //'value1'
```

<br/>

### 값 확인

has 메소드를 사용하여 맵에 값이 존재하는지 확인

```javascript
const hasKey = myMap.has("key2"); //true
```

<br/>

### 값 삭제

delete 메소드를 사용하여 맵에서 값을 제거

```javascript
myMap.delete("key2");
```

<br/>

### 크기 확인

size 속성을 사용하여 맵에 저장된 키-값의 쌍의 개수를 반환

```javascript
const size = myMap.size; //2
```

<br/>

### 모든 키나 값 가져오기

`keys` 메서드를 사용하여 `모든 키 배열`을 반환<br/>
`values` 메서드를 사용하여 `모든 값 배열`을 반환

```javascript
const keys = myMap.keys(); //[ key1, key2 ]
const values = myMap.values(); //[ value2, value2 ]
```

### 순회하기

`forEach`를 사용하여 맵을 순회할 수 있다

```javascript
myMap.forEach((value, key) => {
  console.log(`키: ${key}, 값: ${value}`);
});
```

<br/>

## 객체(Object) vs Map

일반적으로 키-값 데이터를 저장하고 관리하는 경우, 특별한 요구사항이 없다면 `Map`을 사용하는 것이 객체보다 더 다양한 데이터 타입과 순서를 보장하는 측면에서 유용하다.

### 키의 타입

- 객체(Object): 객체의 키(key)는 문자열 또는 심볼(Symbol)만 사용할 수 있다.
- Map: Map은 어떤 데이터 타입도 키(key)로 사용할 수 있다.(숫자, 객체, 함수 등)

### 순서 보장

- 객체(Object): 객체는 키-값 쌍을 저장하는데 순서를 보장하지 않는다. 즉, 키-값 쌍이 추가된 순서대로 반드시 순회되지 않는다.
- Map: Map은 키-값 쌍을 저장한 순서대로 순회한다. (데이터의 순서가 유지됨)

### 크기 확인

- 객체(Object): 객체의 크기(프로퍼티 수)를 확인하기 위한 내장 메서드나 속성이 없기 때문에 직접 반복문을 사용하여 크기를 계산해야 한다.
- Map: Map은 size 프로퍼티를 통해 크기를 쉽게 확인할 수 있다.

### 키의 연관성 유지

- 객체(Object): 객체의 프로퍼티 키는 항상 문자열로 변환되므로, 다른 데이터 타입의 키에 대한 연관성을 유지하기 어려울 수 있다.
- Map: Map은 키의 데이터 타입을 유지하므로, 연관성을 더 잘 유지할 수 있다.

### 반복 가능한(iterable) 객체

- 객체(Object): 객체는 직접 반복할 수 있는 내장 메서드가 없기때문에 반복을 위해서는 for...in 루프나 Object.keys() 등을 사용해야 한다.
- Map: Map은 반복 가능한(iterable) 객체이므로 for...of 루프나 forEach 메서드를 사용하여 편리하게 순회할 수 있다.
