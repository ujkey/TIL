# Set

<br/><br/>

## 1. Set?
고유한 값을 저장할 수 있는 특별한 유형의 컬렉션(중복된 값을 허용하지 않음)

<br/>

### 생성
Set 객체 생성자 사용
```javascript
const mySet = new Set();
```

<br/>

### 값 추가
add 메소드를 사용하여 세트에 값을 추가
```javascript
mySet.add(1);
mySet.add(2);
mySet.add(3);
```

<br/>

### 값 제거
delete 메소드를 사용하여 세트에서 값을 제거
```javascript
mySet.delete(2);
console.log(mySet); //Set {1, 3}
```
<br/>

### 존재 확인
has 메소드를 사용하여 세트에 값이 존재하는지 확인
```javascript
console.log(mySet.has(1)); //true
console.log(mySet.has(4))l //false
```
<br/>

### 반복
for...of 루프를 사용하여 집합의 값을 반복할 수 있다
```javascript
for(const value of mySet) {
    console.log(value);
}
```
<br/>

### 크기 확인
size 속성을 사용하여 세트에 고유한 값이 몇 개 있는지 확인
```javascript
console.log(mySet.size); //2
```

<br/><br/>

## 2. Set은 어떻게 고유한 값을 가질까?
Set은 요소를 추가하거나 확인할 때 `SameValueZero 알고리즘`을 자동으로 활용하여 값의 고유성을 유지하므로 중복 값이 ​​허용되지 않는다

- `SameValueZero 알고리즘`
    -  JavaScript에서 값의 동일성을 확인하는 데 사용되는 비교 알고리즘
    - NaN !== NaN 이지만, 그럼에도 NaN은 NaN과 일치한다고 간주한다
    - 다른 모든 값에 대해서는 === 연산자(엄격한 동등)와 거의 유사하게 작동

<br/><br/>

## 3. 활용 사례
고유성이 우선시되는 데이터 컬렉션으로 작업해야 할 때 유용
- 고유한 값 저장
- 값 존재 여부 확인
- 배열에서 중복 항목 제거 : 배열을 세트로 변환한 다음 다시 배열로 변환하면 중복 항목을 쉽게 제거할 수 있다
- 사용자 입력의 고유성 관리 : 사용자가 등록 양식에 사용자 이름이나 이메일 주소와 같은 중복 데이터를 제출하지 않도록 하는 데 도움이 될 수 있다