# 컴포넌트의 상태 관리를 위한 React Hooks

## Hooks 등장하기 전

컴포넌트의 상태 관리를 하려면 클래스 기반 리액트 컴포넌트를 작성해야 했다. 

this.state 필드에 이름을 저장한다면, 사용자가 이 값을 변경할 때마다 이 값이 갱신되고 다시 화면에 반영하는 Class 기반 컴포넌트 방식이였다. 

그렇기 때문에 함수 기반 컴포넌트를 작성하여 유지 보수를 쉽게 하도록 Hooks를 만들었다.

## Hooks란 ?

---

> 리액트 v16.8 에 새로 도입된 기능으로, 함수형 컴포넌트에서 state와 생명주기 기능을 연동할 수 있게 해주는 함수
> 

쉽게 말해, 함수형 컴포넌트에서 상태 값 및 다른 여러 기능을 사용하기 편리하게 해주는 메소드이다.

기존 라이프 사이클 메소드 기반이 아닌 로직 기반으로 나눌 수 있기 때문에, 컴포넌트를 함수 단위로 잘게 나눌 수 있다. 

함수 컴포넌트에서 state을 가질 수 있게 되었다.

만일 앱을 react hook을 사용하여 만든다면 class component, render 등을 안해도 된다는 뜻이다.

- class 안에서 동작하지 않으므로 class 없이 리액트를 사용할 수 있게 한다.

→ 모든 것은 하나의 function이 되는 것, 함수형 프로그래밍이 가능해지는 것

기능

- 함수형 컴포넌트에서도 상태 관리를 할 수 있는 **useState**
- 렌더링 직후 작업을 설정하는 **useEffect** 등

→ 기존의 함수형 컴포넌트에서 할 수 없었던 다양한 작업을 할 수 있게 해준다.

### 주의사항

- Hook 사용 시에 최상위(반복문, 조건문, 중첩된 함수 x)에서 그리고 자바스크립트 함수가 아닌 리액트 함수 컴포넌트에서만 Hook을 호출해야 한다. 컴포넌트가 렌더링될 때마다 항상 동일한 순서로 Hook이 호출되게 된다.

### useState

---

> 함수형 컴포넌트에서도 가변적인 상태를 지니고 있을 수 있게 해주는 가장 기본적인 Hook
> 

- state를 함수 컴포넌트 안에서 사용할 수 있게 한다.
- 함수형 컴포넌트에서 상태를 관리해야 되는 일이 발생할 때 사용
- 여러번 사용하기
    - 하나의 useState 함수는 하나의 상태값만 관리할 수 있으므로 컴포넌트에서 관리해야 할 상태가 여러개인 경우에도 여러번 사용하면 된다.
    

### useEffect

---

> 리액트 컴포넌트가 렌더링 될 때마다 특정 작업을 수행하도록 설정 할 수 있는 Hook
> 

클래스형 컴포넌트의 componentDidMount 와 componentDidUpdate 를 합친 형태로 보아도 무방하다.

- 마운트 될 때만 실행하고 싶을 때
- 특정 값이 업데이트 될 때만 실행하고 싶을 때
- 컴포넌트가 언마운트되기 전이나, 업데이트 되기 직전에 어떠한 작업을 수행하고 싶다면 useEffect 에서 뒷정리(cleanup) 함수를 반환해주어야 합니다

### useReducer

---

> useState 보다 컴포넌트에서 더 다양한 상황에 따라 다양한 상태를 다른 값으로 업데이트해주고 싶을 때 사용하는 Hook
> 

Reducer 

- 현재 상태와, 업데이트를 위해 필요한 정보를 담은 액션(action) 값을 전달 받아 새로운 상태를 반환하는 함수
- 리듀서 함수에서 새로운 상태를 만들 때는 꼭 불변성을 지켜주어야 합니다.

### useMemo

---

> 특정 값 재사용하고자 할 때 사용하는 Hook (= 리턴값 재사용)
> 

- 함수형 컴포넌트 내부에서 발생하는 연산을 최적화 할 수 있게 한다.
    - 함수형 컴포넌트: 렌더링 될 때마다 함수 컴포넌트가 호출된다는 뜻
    - 즉, 함수가 호출되면 모든 내부 변수가 초기화된다
        - 컴포넌트 내부에 여러 개의 함수가 있을 경우, 하나의 값만 바뀌어도 모든 함수가 호출되어 불필요한 연산이 다시 이루어짐
- 복잡한 연산의 중복을 피하고 React앱의 성능을 최적화한다.

### useCallback

---

> 특정 함수를 새로 만들지 않고 재사용하고 싶을때 사용하는 Hook (= 함수 재사용)
> 

- 주로 렌더링 성능을 최적화해야 하는 상황에서 사용한다.
- 이벤트 핸들러 함수를 필요할 때만 생성 할 수 있다.

### useContext

---

> 함수형 컴포넌트에서 Context 를 보다 더 쉽게 사용하게 해준다.
> 

### useRef

---

> 함수형 컴포넌트에서 ref 를 쉽게 사용 할 수 있게 해준다.
> 

참고문헌

[https://velog.io/@velopert/react-hooks](https://velog.io/@velopert/react-hooks)

[https://velog.io/@soshin0112/React-리액트-Hooks](https://velog.io/@soshin0112/React-%EB%A6%AC%EC%95%A1%ED%8A%B8-Hooks)
## Hooks 등장하기 전

컴포넌트의 상태 관리를 하려면 클래스 기반 리액트 컴포넌트를 작성해야 했다. 

this.state 필드에 이름을 저장한다면, 사용자가 이 값을 변경할 때마다 이 값이 갱신되고 다시 화면에 반영하는 Class 기반 컴포넌트 방식이였다. 

그렇기 때문에 함수 기반 컴포넌트를 작성하여 유지 보수를 쉽게 하도록 Hooks를 만들었다.

## Hooks란 ?

---

> 리액트 v16.8 에 새로 도입된 기능으로, 함수형 컴포넌트에서 state와 생명주기 기능을 연동할 수 있게 해주는 함수
> 

쉽게 말해, 함수형 컴포넌트에서 상태 값 및 다른 여러 기능을 사용하기 편리하게 해주는 메소드이다.

기존 라이프 사이클 메소드 기반이 아닌 로직 기반으로 나눌 수 있기 때문에, 컴포넌트를 함수 단위로 잘게 나눌 수 있다. 

함수 컴포넌트에서 state을 가질 수 있게 되었다.

만일 앱을 react hook을 사용하여 만든다면 class component, render 등을 안해도 된다는 뜻이다.

- class 안에서 동작하지 않으므로 class 없이 리액트를 사용할 수 있게 한다.

→ 모든 것은 하나의 function이 되는 것, 함수형 프로그래밍이 가능해지는 것

기능

- 함수형 컴포넌트에서도 상태 관리를 할 수 있는 **useState**
- 렌더링 직후 작업을 설정하는 **useEffect** 등

→ 기존의 함수형 컴포넌트에서 할 수 없었던 다양한 작업을 할 수 있게 해준다.

### 주의사항

- Hook 사용 시에 최상위(반복문, 조건문, 중첩된 함수 x)에서 그리고 자바스크립트 함수가 아닌 리액트 함수 컴포넌트에서만 Hook을 호출해야 한다. 컴포넌트가 렌더링될 때마다 항상 동일한 순서로 Hook이 호출되게 된다.

### useState

---

> 함수형 컴포넌트에서도 가변적인 상태를 지니고 있을 수 있게 해주는 가장 기본적인 Hook
> 

- state를 함수 컴포넌트 안에서 사용할 수 있게 한다.
- 함수형 컴포넌트에서 상태를 관리해야 되는 일이 발생할 때 사용
- 여러번 사용하기
    - 하나의 useState 함수는 하나의 상태값만 관리할 수 있으므로 컴포넌트에서 관리해야 할 상태가 여러개인 경우에도 여러번 사용하면 된다.
    

### useEffect

---

> 리액트 컴포넌트가 렌더링 될 때마다 특정 작업을 수행하도록 설정 할 수 있는 Hook
> 

클래스형 컴포넌트의 componentDidMount 와 componentDidUpdate 를 합친 형태로 보아도 무방하다.

- 마운트 될 때만 실행하고 싶을 때
- 특정 값이 업데이트 될 때만 실행하고 싶을 때
- 컴포넌트가 언마운트되기 전이나, 업데이트 되기 직전에 어떠한 작업을 수행하고 싶다면 useEffect 에서 뒷정리(cleanup) 함수를 반환해주어야 합니다

### useReducer

---

> useState 보다 컴포넌트에서 더 다양한 상황에 따라 다양한 상태를 다른 값으로 업데이트해주고 싶을 때 사용하는 Hook
> 

Reducer 

- 현재 상태와, 업데이트를 위해 필요한 정보를 담은 액션(action) 값을 전달 받아 새로운 상태를 반환하는 함수
- 리듀서 함수에서 새로운 상태를 만들 때는 꼭 불변성을 지켜주어야 합니다.

### useMemo

---

> 특정 값 재사용하고자 할 때 사용하는 Hook (= 리턴값 재사용)
> 

- 함수형 컴포넌트 내부에서 발생하는 연산을 최적화 할 수 있게 한다.
    - 함수형 컴포넌트: 렌더링 될 때마다 함수 컴포넌트가 호출된다는 뜻
    - 즉, 함수가 호출되면 모든 내부 변수가 초기화된다
        - 컴포넌트 내부에 여러 개의 함수가 있을 경우, 하나의 값만 바뀌어도 모든 함수가 호출되어 불필요한 연산이 다시 이루어짐
- 복잡한 연산의 중복을 피하고 React앱의 성능을 최적화한다.

### useCallback

---

> 특정 함수를 새로 만들지 않고 재사용하고 싶을때 사용하는 Hook (= 함수 재사용)
> 

- 주로 렌더링 성능을 최적화해야 하는 상황에서 사용한다.
- 이벤트 핸들러 함수를 필요할 때만 생성 할 수 있다.

### useContext

---

> 함수형 컴포넌트에서 Context 를 보다 더 쉽게 사용하게 해준다.
> 

### useRef

---

> 함수형 컴포넌트에서 ref 를 쉽게 사용 할 수 있게 해준다.
> 

참고문헌

[https://velog.io/@velopert/react-hooks](https://velog.io/@velopert/react-hooks)

[https://velog.io/@soshin0112/React-리액트-Hooks](https://velog.io/@soshin0112/React-%EB%A6%AC%EC%95%A1%ED%8A%B8-Hooks)