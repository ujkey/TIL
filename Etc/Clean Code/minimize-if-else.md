# if-eles 최소화하여 유연성 높이기

<br/><br/>


## Bad
결정 지점에 if-else 잠금을 사용하면 `코드 적응성`이 떨어진다
- 코드 적응성: 변경, 수정 또는 확장될 수 있는 능력

```javascript
if(array.length === 0) {
    throw new Error("Empty array nor allowed");
} else {
    return array.reduce((a, b) => a+b, 0) / array.length;
}
```

<br/>

## Good
Opt-functions 적용
- 코드 조각을 캡슐화하고 모듈화하기 위해 함수 또는 메서드를 사용하도록 권장하는 코딩 관행

```javascript
function assertNotEmpty(array) {
    if(array.length === 0) throw new Error("Empty array nor allowed");
}

function average(array) {
    assertNotEmpty(array);
    return array.reduce((a, b) => a+b, 0) / array.length;
}
```