# for...of와 for...in 비교
JavaScript의 for...of와 for...in 루프는 둘 다 반복문이지만, 다루는 대상과 동작 방식에 차이가 있다

<br/><br/>

## for...of
- for...of 루프는 `반복 가능한 iterable 객체를 대상으로 순회`한다. (배열, 문자열, Map, Set, NodeList 등)
- 반복 변수는 객체의 요소 값
- 배열의 각 요소나 문자열의 각 문자 등을 순차적으로 처리할 때 유용

    ```javascript
    const arr = [1, 2, 3, 4, 5];
    for (let element of arr) {
        console.log(element); // [1, 2, 3, 4, 5]
    }
    ```
<br/>

## for...in
- for...in 루프는 `객체의 속성(프로퍼티)을 순회`할 때 사용된다
- 반복 변수는 속성(프로퍼티)의 이름 또는 키 값
- 배열과 문자열에도 사용할 수 있지만, 일반적으로 객체의 속성을 순회하는 용도로 사용

    ```javascript
    const obj = { a: 1, b: 2, c: 3 };
    for (const key in obj) {
        const value = obj[key];
        console.log(key, value);
    }
    ```