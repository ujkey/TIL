# 메소드 체이닝(Method Chaining)
- `단일 코드라인 형식`으로 배열이나 객체의 `메소드를 연속적(순차적)으로 호출`하는 코딩 패턴
- 객체 생성과 설정을 동시에 처리하거나, 데이터를 연속적으로 가공할 때 유용하게 사용

<br/><br/>

### Bad
```javascript
const arr = [1, 2, 3];
const squared = arr.map(x => x * x);
const evens = squared.filter(x => x % 2 === 0);
```

<br/>

### Good
- 간결한 코드 + 가독성 향상
    - 중간 변수가 필요하지 않음
    - 복잡한 작업을 일련의 메서드 호출로 해결
```javascript
const result = [1, 2, 3].map(x => x * x).filter(x => x % 2 === 0);
```