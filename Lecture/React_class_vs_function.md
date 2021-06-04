# React: class vs. function

## 1. 소개

- class 컴포넌트
  - `React.Component`와 `React.PureComponent`를 기반으로 만든 컴포넌트를 말한다.
  - Life-cycle method를 사용하여 `state`값이 바뀌면 렌더링을 다시 한다.
  - 클래스 스타일로 만드는 컴포넌트는 함수 스타일 컴포넌트보다 여러가지 문법이나 관련 지식이 상대적으로 더 많이 필요하다.
- function 컴포넌트
  - `state`와 Life-cycle method 사용이 불가능하다.
  - 함수를 만드는 문법만 알고 있으면 만들 수 있다.

> 👉 **`hooks`**의 등장으로 함수 스타일 컴포넌트도 `state`와 Life-cycle method 사용이 가능해졌다!

## 2. 개발환경 세팅

### 2-1. React app 설치

```powershell
PS C:\Studying\react-class-vs-function> npx create-react-app .
```

### 2-2. React app 실행

```powershell
npm start
```

### 2-3. Class Component와 Function Component 세팅

- `App.js`

  ```react
  import React from 'react';
  import './App.css';
  
  function App() {
    return (
      <div className="container">
        <h1>Hello World!</h1>
        <FuncComp></FuncComp>
        <ClassComp></ClassComp>
      </div>
    );
  }
  // Function Component
  function FuncComp() {
    return (
      <div className="containter">
        <h2>Function style component</h2>
      </div>
    )
  }
  //Class Component
  class ClassComp extends React.Component {
    render() {
      return (
        <div className="container">
          <h2>Class style component</h2>
        </div>
      )
    }
  }
  export default App;
  ```

- `App.css`

  ```css
  .container {
      border: 5px solid red;
      margin: 5px;
      padding: 5px;
  }
  ```

- 화면 출력

  ![image-20210604123710904](../../md-img/image-20210604123710904.png)

## 3. Class Component와 Function Component에서의 `props` 사용

```react
import React from 'react';
import './App.css';

function App() {
  return (
    <div className="container">
      <h1>Hello World!</h1>
      <FuncComp initNumber={2}></FuncComp>
      <ClassComp initNumber={2}></ClassComp>
    </div>
  );
}
// props를 함수에 인자로 넣어주고, props.initNumber로 받아올 수 있다.
function FuncComp(props) {
  return (
    <div className="container">
      <h2>Function style component</h2>
      <p>Number : {props.initNumber}</p>
    </div>
  );
}

class ClassComp extends React.Component {
  render() {
    return (
      <div className="container">
        <h2>Class style component</h2>
        <!-- 함수처럼 인자를 받아올 필요 없이 this.props.initNumber로 받아올 수 있다. -->
        <p>Number : {this.props.initNumber}</p>
      </div>
    )
  }
}

export default App;
```

## 4. Class Component: `state` 사용법

- 클래스 컴포넌트에서는 `props`를 `state`로 받아와서 `setState()` 메소드를 이용하여 `state`값을 변경할 수 있다.
- `state`값이 변경될 때마다 클래스 컴포넌트 내부의 `render()`함수가 호출되어 매번 리렌더링된다.

```react
class ClassComp extends React.Component {
  // props를 state로 받아온다.
  state = {
    number:this.props.initNumber
  }
  render() {
    return (
      <div className="container">
        <h2>Class style component</h2>
        <p>Number : {this.state.number}</p>
        <!-- 버튼을 클릭할 때마다 값이 랜덤으로 바뀌는 함수를 사용해서 setState()로 state값을 변경해준다. -->
        <input type="button" value="random" onClick= {
          function() {
            this.setState({number:Math.random()})
          }.bind(this)
        }></input>
      </div>
    )
  }
}

```

