# 리덕스에서 사용되는 키워드 숙지하기
>## 👉🏻 액션 (Action)
>상태에 변화가 필요할 때 액션을 발생시킨다. (객체하나로 표현)<br/>
>type을 필수로 그외의 값들은 개발자 마음대로 생성가능하다.
```
{
  type: "TOGGLE_VALUE"
}
```
```
{
  type: "ADD_TODO",
  date: {
    id: 0,
    text: "리덕스 배우기"
  }
}
```

<br/>

>## 👉🏻 액션 생성함수 (Action Creator)
>액션을 만드는 함수<br/>
>parameter를 받아와 액션 객체 형태로 만들어준다.<br/>
>**액션 생성함수를 만드는 이유?**<br/>
>=> 컴포넌트에서 더욱 쉽게 액션을 발생시키기 위함이다.<br/>
>보통 함수 앞에 export 키워드를 붙여서 다른 파일에서 불러와 사용한다.<br/>
>**필수 아님**
```
export default addTodo(data) {
  return {
    type: "ADD_TODO",
    data
  };
}

// or

export const changeInput = text => ({
  type: "CHANGE_INPUT",
  text
});
```

<br/>

> ## 👉🏻 리듀서 (Reducer)
>변화를 일으키는 함수이다.<br/>
>현재의 상태, 전달 받은 액션을 참고하여 새로운 상태를 만들어 반환한다.
```
// 두가지의 parameter를 받아온다.
function reducer(state, action) {
  // 상태 업데이트 로직
  return aleredState;
}

// 카운터를 위한 리듀서를 작성한다면 다음과 같이 작성가능하다.
function counter(state, action) {
  switch(action.type) {
    case 'INCREASE':
      return state + 1;
    case 'DECREASE':
      return state - 1;
    default:
      return state;
```
>useReducer에서는 default:에 throw new Error('Unhandled Action') 같이 에러를 발생시키도록 처리하는게 일반적이다.<br/>
>redux의 reducer에선 기존 state를 그대로 반환하도록 작성해야 한다. <br/>여러개의 reducer를 만들고 이를 합쳐서 Root Reducer를 만들 수 있다. <br/>Root Reducer 안의 작은 reducer 들은 sub reducer라 한다.

<br/>

> ## 👉🏻 스토어 (store)
>리덕스에서는 한 애플리케이션 당 하나의 스토어를 만들게 됨<br/>
>스토어 안에는 현재의 앱 상태, 리듀서가 들어있고 추가적으로 몇가지 내장 함수들이 존재한다.

<br/>

> ## 👉🏻 디스패치 (dispatch)
>스토어의 내장함수, 액션을 발생시킨다.<br/>
>이 함수에는 액션을 파라미터로 전달한다.<br/>
>dispatch(action) 이런식으로!<br/>
>호출을 하면 스토어는 리듀서 함수를 실행시켜 해당 액션을 처리하는 로직이 있다면 액션을 참고하여 새로운 상태를 만들어 준다.

<br/>

> ## 👉🏻 구독 (subcribe)
>스토어의 내장함수, 함수 형태의 값을 파라미터로 받아온다.<br/>
>이 함수에 특정 함수를 전달해주면 액션이 디스패치 되었을 때 마다 전달해준 함수가 호출된다.<br/>
>리액트에서는 react-redux 라이브러리에서 제공하는 connect함수나 useSelector Hook 을 사용하여 리덕스 스토어의 상태에 구독한다.
