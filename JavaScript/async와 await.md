# async와 await

<br/><br/>

## async와 await?
이 비동기 처리 패턴은 기존의 비동기 처리 방식인 콜백 함수와 프로미스의 단점을 보완하고 코드의 가독성을 높여준다.

<br/>

## 비동기 처리 방식 비교 (콜백 vs async/await) 
### 콜백
일반적으로 자바스크립트의 비동기 처리는 아래와 같이 콜백을 사용해서 코드의 살행 순서를 보장받는다.
```javascript
function logName() {
  const product = fetchUser(`${baseUrl}/product/1`, function(product) {
    if (product.id === 1) {
      console.log(product.name);
    }
  });
}
```
### async & await
콜백 없이 비동기 처리를 하고 싶다면, `async`와 `await만` 붙이면 된다.
```javascript
async function logProduct() {
    var product = await fetchUser(`${baseUrl}/product/1`);
    if (product.id === 1) {
        console.log(product.name);
    }
}
```

<br/>

## async & await 사용해보기
### 기본 문법
#### 1. 함수의 앞에 `async` 라는 예약어를 붙인다
#### 2. 함수의 내부 로직 중 HTTP 통신을 하는 비동기 처리 코드 앞에 `await`를 붙인다
- `await` 의 대상이 되는 비동기 처리 코드는 `Axios` 등 프로미스 객체를 반환하는 API 호출 함수여야 의도한대로 동작함

```javascript
async function 함수명() {
  await 비동기_처리_메서드_명();
}
```

<br/>

### 기본 예제
```javascript
function fetchGoods() {
  return new Promise(function(resolve, reject) {
    var goods = [1,2,3];
    resolve(goods)
  });
}

async function logGoods() {
  var resultGoods = await fetchGoods();
  console.log(resultGoods); // [1,2,3]
}
```

<br/>

## 여러개의 비동기 처리 코드 다루기
`async & await` 문법이 가장 유용하게 활용되는 시점은 여러 개의 비동기 처리 코드를 다룰 때이다.<br/>
아래 처럼 `async & await` 문법을 이용하면 콜백이나 프로미스 없이 더 간결하고 가독성이 좋은 코드를 작성할 수 있다.

```javascript
function fetchUser() {
  var url = 'https://jsonplaceholder.typicode.com/users/1'
  return fetch(url).then(function(response) {
    return response.json();
  });
}

function fetchTodo() {
  var url = 'https://jsonplaceholder.typicode.com/todos/1';
  return fetch(url).then(function(response) {
    return response.json();
  });
}

async function logTodoTitle() {
    var user = await fetchUser();
    if (user.id === 1) {
        var todo = await fetchTodo();
        console.log(todo.title); // delectus aut autem
    }
}
```

<br/>

## async & await 예외 처리
프로미스에서 에러 처리를 위해 .catch()를 사용했던 것처럼 async에서는 catch {} 를 사용하여 예외처리를 수행한다.<br/>
발견된 에러는 error 객체에 저장되므로, 에러의 종류에 따라 적절한 에러 코드를 처리할 수 있다.
```javascript
async function logTodoTitle() {
  try {
    var user = await fetchUser();
    if (user.id === 1) {
      var todo = await fetchTodo();
      console.log(todo.title); // delectus aut autem
    }
  } catch (error) {
    console.log(error);
  }
}
```