# 정규표현식(정규식)

<br/><br/>

## 0. 개요
- 정규표현식은 문자열에서 특정 패턴을 찾거나 변형하는 패턴
- 문자열 검색(search), 추출(extract), 대체(replace) 등 다양한 작업에 사용


<br/>

## 1. 생성
- 생성자 함수 방식
    ```javascript
    const regexp2 = new RegExp("^abc", "gi");
    ```

- 리터럴(Literal) 방식 : `/패턴/플래그` 형식으로 표현
    ```javascript
    const regexp2 = /^abc/gi;
    ```
<br/>

## 2. 메소드
- `정규식.exec(문자열)`: 일치하는 하나의 정보(Array) 반환
- `정규식.test(문자열)`: 일치 여부(Boolean) 반환
- `문자열.match(정규식)`: 일치하는 문자열의 배열(Array) 반환
- `문자열.search(정규식)`: 일치하는 문자열의 인덱스(Number) 반환
- `문자열.replace(정규식,대체문자)`:	일치하는 문자열을 대체하고 대체된 문자열(String) 반환
- `문자열.split(정규식)`: 일치하는 문자열을 분할하여 배열(Array)로 반환
- `생성자_정규식.toString()`: 생성자 함수 방식의 정규식을 리터럴 방식의 문자열(String)로 반환

<br/>

## 3. 플래그
- `g`: 전역 검색, 패턴에 맞는 모든 문자열을 찾음(global)
- `i`: 대소문자를 구분하지 않고 매치.
- `m`: 다중행 검색(multi line)
- `u`: 유니코드(unicode) 

<br/>

## 4. 정규식 패턴 기본(표현식)
- `abc`: a, b, c 중 하나와 매치.
- `^abc`: a, b, c 이외의 문자와 매치.
- `a-z`: a부터 z까지의 문자와 매치.

<br/>

## 5. 정규표현식 테스트 사이트
- https://regex101.com/
- https://regexr.com/
- https://regexper.com/