# React

리액트는 SPA를 만들 때 사용되는 자바스크립트 기반의 프론트엔드 라이브러리다. 

1. 리액트는 <strong>Virtual DOM</strong>을 사용해 어플리케이션의 성능을 향상시킨다.
2. <strong>CSR, SSR</strong>를 지원한다.
3. <strong>컴포넌트 가독성</strong>이 높고 간단해서 유지보수가 쉽다.
4. 다른 프레임워크와 혼용 가능하다.

## React 의 렌더링, 브라우저 이벤트 처리는?
React는 실제로 DOM을 제어하지 않고 Virtual DOM을 두어서 Virtual DOM이 변경될 때 실제 DOM을 변경하도록 설계되어 있다. 이 작업을 Reconciliation(재조정)이라고 한다. Virtual DOM을 갱신하기 위해서 setState() 메소드를 호출하거나 redux를 사용해 store가 변하면 최상위 컴포넌트의 render()함수를 호출하여 갱신하는 방법이 있다.

</br></br>

## Virtual DOM 이 무엇인가? 장점?
  Virtual DOM은 실제 DOM 변화를 최소화 시켜주는 역할을 한다. 만약 HTML에 20번의 변화가 생기면 Virtual DOM은 변화된 부분만 가려내어 실제 DOM에 전달하기 때문에 실제 DOM은 렌더링을 한 번만 거친다. 실제 DOM을 바꾸는 것보다 Virtual DOM을 생성하는 것이 효율적이다.

</br></br>

## React의 라이프 사이클?
<strong>라이프 사이클은 컴포넌트의 생명주기를 말하며, 컴포넌트 생명주기는 컴포넌트가 생성되고(Mount) 사용되고(Update) 소멸되기(UnMount)까지의 과정을 의미한다.</strong> 라이프 사이클 과정에서 호출되는 메서드 중 
1. <strong>componentDidMount()</strong> 는 컴포넌트가 생성될 때 한 번 호출된다. 
2. <strong>componentDidUpdate()</strong> 는 컴포넌트의 속성 값 혹은 상태 값이 변경되었을 때 한 번 호출된다.
3. <strong>componentWillUnMount() </strong>는 컴포넌트가 소멸될 때 한 번 호출된다.
4. <strong>render()</strong>는 초기 화면을 그려줄 때와 업데이트 시 호출된다.


## state를 직접 변경하지 않고 setState를 사용하는 이유?
<strong>state는 불변성을 유지해야 하기 때문이다.</strong> 컴포넌트는 현재 state와 setState를 비교해 업데이트가 필요한 경우에만 render함수를 호출한다. 하지만 state를 직접 수정 시 변경된 값이 렌더링되지 않는다.

## useMemo? useCallback?
useMemo는 특정 값을 재사용하기 위해 사용하며, useCallback은 특정 함수를 재사용하기 위해 사용한다. 컴포넌트가 리렌더링 될 때마다 불필요하게 재연산되거나 재선언 되는 것을 방지하는 역할을 한다.
