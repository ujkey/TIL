# React의 조건부 렌더링
- 특정 조건이 충족될 때에만 컴포넌트를 렌더링하는 기술
- 컴포넌트의 상태나 속성을 기반으로 UI를 조작할 때 유용
- 다른 컴포넌트를 특정 상황에 맞게 보여줄 때 유용

<br/><br/>

## 1. why?
- undefined 가능성 때문에 초기화되기 전의 상태에서 오류가 발생할 가능성이 있어, 이를 방지하기 위해 조건부 렌더링을 사용

<br/>

## 2. 방법
### 옵션A : 삼항 연산자를 이용한 조건부 렌더링
```` jsx
{isLoggedIn ? <UserProfile /> : <Login />}
``````

### 옵션B : 논리 연산자를 이용한 조건부 렌더링
```` jsx
{isAdmin && <AdminPanel />}
``````

### 옵션C : if문을 활용한 조건부 렌더링
- 조건이 많고 복잡할때 활용하면 가독성을 높일 수 있다
```` jsx
if (isLoggedIn) {
    return UserProfile();
  } else if (!isLoggedIn) {
    return Login();
  } else if (isAdmin) {
    return AdminPanel();
  } else {
    return <></>
  }
``````
