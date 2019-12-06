# 냥터레스트와 MobX
냥터레스트는 React와 Mobx 상태관리 라이브러리 제작된 유기묘리스트 웹프로젝트입니다.

조윤우님과 함께 둘이서 진행하고 있습니다.

## React란
리액트는 페이스북에서 제공해주는 프론트엔드 라이브러리입니다.
`컴포넌트`기반으로 되어있어서 `컴포넌트`에 `데이터`를 내려주면 개발자가 설계한대로 UI가 만들어져 사용자에게 보여집니다.


## React의 데이터 흐름은 단방향이다.
리액트의 데이터 흐름은 한방향으로만 흐릅니다. 부모컴포넌트에서 자식컴포넌트로 데이터를 보내며, 자식컴포넌트에서 부모컴포넌트로 데이터를 올려줄 수 없습니다.

컴포넌트간의 데이터는 `props`를 사용해 전달시킬 수 있으며 부모의 데이터를 바꿔주기 위해서는 `state`를 이용해야합니다.

### Props와 State
리액트에서 다루는 데이터이며 데이터의 용도에 따라 다르게 사용됩니다.

#### Props
props란 부모 컴포넌트에서 자식 컴포넌트로 전달해 주는 데이터를 말하며 변동되지 않는 데이터를 전달할 때 사용됩니다.
자식컴포넌트에서는 받은 props를 변경할 수 없으며 전달해준 최상위 부모컴포넌트만 props를 변경할 수 있습니다.

#### State
state는 유저와 상호작용을 하며 변동가능한 동적인 데이터를 다룰때 사용됩니다.
state를 변경하기 위해서는 `setState`를 사용해야합니다.
다른 컴포넌트에서의 직접적인 변경은 불가능하지만 자신보다 상위에 있는 state는 변경이 가능한데, state를 변경해주는 함수를 상위컴포넌트에서 props로 받는다면 state의 변경이 가능합니다.


## MobX란?
- Simple, Scalable State Management
- `state`를 관리해주는 간단하고 쉬운 라이브러리
- 비슷한 라이브러리로는 `redux`가 있음
- 타입스크립트기반

상태 관리 라이브러리의 역할에 대해 간단히 말하자면 react의 트리 구조의 props 전달과 state가 아닌, 특정한 저장소에 데이터를 따로 모아놓고 관리하는 것

### 냥터레스트는 왜 Redux가 아닌 MobX인가?
#### 냥터레스트 상태관리 고민의 시작
리액트로 작업을 하다보니 자연스럽게 여러 컴포넌트 단위로 나누어 UI작업을 하게되었고, 자식컴포넌트에서 부모컴포넌트의 데이터를 컨트롤해야되는 상황이 계속되었습니다. 그럴때마다 부모컴포넌트에서 데이터를 컨트롤하는 함수를 만들어 자식컴포넌트에게 props로 넘겨주었습니다.
이런 단방향성의 데이터 흐름이 답답하여 이 상황을 해결하는 법을 구글링해보았지만 자식컴포넌트에서 부모컴포넌트의 데이터를 컨트롤하는 방법은 위 방법을 제외하고는 없었습니다.
(구글링하며 Redux, Context API 등 상태관리 라이브러리에 대해서 분명히 키워드가 나왔을텐데 기억이나지 않습니다. 어렵고 복잡한 내용일거라 생각하고 자체스킵한것이 틀림없습니다.)

멘토링시간에 무작정 멘토님께 이럴땐 어떻게해야돼요? 라고 물어보았고(ㅎㅎ)
멘토님께서는 `Redux`를 소개해주셨습니다. 저는 이때 처음 Redux를 알게되었던것같습니다.

#### MobX를 선택한 이유
처음엔 협의를 통해 냥터레스트도 `Redux`를 사용하여 상태관리를 해야겠다 했습니다.
React에서 상태관리 라이브러리를 사용한다하면 대부분 Redux를 사용하기때문에 자연스러운 과정이었습니다.
그럼에도 불구하고 MobX를 선택하게된 이유에는 같이 프로젝트를 진행하시는 윤우님께서 MobX라는 흑마법을 들고 나타나셨기 때문입니다.

- MobX는 Redux보다 간결하다.
- MobX는 Redux보다 난이도가 쉽다.

처음은 위의 두가지의 단순하고도 강력한 이유때문에 MobX를 선택하였습니다.
초보프론트엔드 입문자인 저희의 프로젝트에는 쉽고 간결한 MobX가 더 맞다고 생각했습니다.

Redux가 좋다! MobX가 좋다! Context API가 좋다!가 아닌
프로젝트의 목적과 상황에 맞는 선택이었습니다.

#### 왜 MobX가 간결하고 쉬울까?
- `Redux`는 Flux개념을 바탕으로한 React에서 현재 가장 많이 사용되는 State 관리 라이브러리 입니다.
- Redux는 많은 라이브러리가 필요하지만 MobX는 필요없음
  ![리덕스라이브러리](http://woowabros.github.io/img/2019-01-02/redux-with-libs.png)

     MobX는 `mobx`,`react-mobx` 필요

- Redux의 flow보다 MobX의 flow가 간결합니다.
- redux에서 해줘야했던 action 선언, connect, mapStateToProps, mapDispatchToProps등 번거로운 작업들은 데코레이터로 간단하게 대체되어 특정 개체를 감시할 수 있습니다.
    - `Redux Flow`
    ![redux flow](https://fullest-sway.me/blog/2017/06/21/redux-use/redux-cycle.png)

        [redux 사용법](https://fullest-sway.me/blog/2017/06/21/redux-use/)
    - `MobX Flow`
    ![mobx flow](https://bumbu.me/assets/images/2016/10/mobx-diagram-300x144.png)
- Redux는 단일스토어지만 MobX는 스토어를 여러개 만들 수 있습니다. 따라서 기능별,로직별로 원하는대로 store를 분리하여 깔끔하게 비즈니스로직을 작성할 수 있습니다.
    - **Store란** 
      - Global영역에서 애플리케이션의 State와 비즈니스로직을 가지고 있고 있는 주체를 Store라고 합니다.
      - State를 Global한 영역에서 관리한다는 말은 즉 State관리 라이브러리 사용의 목적중 한가지 입니다.

      - Redux에서는 State와 State를 핸들링하는 비즈니스로직을 가지고 있는 Reducer, Action등을 포함하는 의미 이기도 하지만, Mobx에서 Store는 명확히 State와 비즈니스로직을 포함하는 Class를 Store라고 부릅니다.

### 데코레이터 (Decorator)
MobX의 특징이라 하면 위에서 언급한 내요처럼 데코레이터`@`만으로 특정개체를 감시한다는 점이라 할 수 있습니다.
Decorator는 ES7에 정의되어 있습니다. 아직은 어떠한 브라우저에서도 지원하지 않고, 심지어 정식으로 채택된 Spec도 아니지만, 사실상 많은 곳에서 이미 polyfill을 거쳐 사용되고 있다고 합니다.

Java를 사용해 보셨다면 적어도 한번은 (@Override public void..) 봤을 눈에 익은 패턴인 Decorator가 Javascript에 들어왔습니다. 물론 아직은 정식 스펙이 아니기 때문에 Babel 이나 Typescript 와 같은 Transpiler를 거쳐 사용해야 합니다.

```javascript
class MyObservable {
  @observable myValue = 5;
}
```
#### @observable
Mobx에서 Rerendering 대상이 되는 state(상태, 값)를 관찰 대상(observable value)라고 칭하며 @observable 데코레이터로 지정한 State는 관찰대상으로 지정되고 그 State는 값이 변경될 때 마다 Rerendering됩니다.

#### @observer
observer는 react에서 state가 변경되면 리렌더링을 하듯이, 스토어에서 obserbvable로 선언해서 가져온 값이 변경될 때 컴포넌트를 리렌더링을 해주는 기능입니다.

#### @action
observable 값을 변경해주는 함수입니다. (setter)

#### @computed
getter에 해당하는 함수입니다. 특징으로는 미리 값을 계산하고 캐싱해둔다는 점이 있어 성능을 최적화시킬 수 있습니다.

### 사용법
#### 로그인
 `Stores/loginStore.js`

```javascript
import { observable, action } from "mobx";

export default class loginStore {
    // @observable 데코레이터를 사용하여 stete를 생성
	@observable userId = "";
	@observable userState = localStorage.getItem('userInfo')?"login":"logout"

	constructor(root) {
		this.root = root;
	}

    // MobX state를 변경할 함수에 @action 데코레이터를 사용하여 선언
	@action
	changeUserState = ()=>{
		if(this.userState === "logout"){
			this.userState = "login"	
		}else {
			this.userState = "logout"
		}
	}

	@action
	changeUserId = (name)=>{
		this.userId= name
	}
}
```

`Stores/index.js`
```javascript
import ListStore from "./listStore";
import SearchStore from "./searchStore";
import BtnStore from "./btnStore";
// Stores/loginStore.js 가져오기
import loginStore from "./loginStore";
import PopupStore from "./popupStore";

class RootStore {
	constructor() {
		this.listStore = new ListStore(this);
		this.searchStore = new SearchStore(this);
		this.btnStore = new BtnStore(this);
        // 생성한 loginStore를 binding시켜준다
		this.loginStore = new loginStore(this);
		this.popupStore = new PopupStore(this);
	}
}

export default RootStore;
```

`index.js`
```javascript
import React from "react";
import ReactDOM from "react-dom";
import { Provider } from "mobx-react";
import App from "./Components/App";
import * as serviceWorker from "./serviceWorker";
// Stores/index.js 가져오기
import RootStore from "./Stores";

// 스토어 인스턴스 생성
const root = new RootStore();

ReactDOM.render(<Provider {...root}><App /></Provider>, document.getElementById("root"));

serviceWorker.unregister();

```

`Components/popup/LayerLogin.js`
```javascript
import React, { Component } from "react";
import { observer, inject } from "mobx-react";

// @inject 데코레이터로 사용할 Store를 가져와 연결
@inject('loginStore')
// 변화감지에 따라 변경될 컴포넌트에 @observer 데코레이터를 선언
@observer
class LayerLogin extends Component {
    ...생략

    sendUserInfo = () => {
        const {changeUserId,changeUserState} = this.props.loginStore

        if ( state.userIdValidate && state.userPasswordValidate ){
            fetch('/login',{
                headers: {
                    'Accept': 'application/json',
                    'Content-Type': 'application/json'
                },
                method: 'POST',
                body: stateTojson,
            })
            .then(res=>res.json()).then(json=>{
                if(!json.sucess){
                    console.log('로그인실패')
                }else {
                    console.log('로그인성공')
                    console.log(json._userId)
                    // MobX @action을 사용한 예시
                    changeUserState()
                    changeUserId(json._userId)
                    localStorage.setItem(
                        "userInfo",
                        JSON.stringify(json._userId)
                    )
                    
                    onClose()
                }
            })

        }else {
            alert("아이디와 패스워드를 알맞게 입력해주세요")
        }
    }

    render(){
         ...생략
        )
        
    }
}

export default LayerLogin;
```
## 마치며
아직 Redux를 사용해보지않아서 MobX와의 차이점을 직접적으로 느끼진 못했지만 둘다 상태관리 라이브러리의 장단점이 존재한다는건 확실하다고 생각합니다.
일단 MobX의 가장 매력적이고 인상적인 부분은 `데코레이터`가 아닐까 싶습니다.
일단 저의 기준에서는 자바스크립트에서 데코레이터를 사용한다는 개념은 생각하지도 못했기 때문입니다.

부모컴포넌트의 상태값에 접근하는게 어려운거구나라고만 생각을 했는데 MobX는 그런 생각을 산산조각 내준 진짜 `흑마법`이었습니다. 이렇게 쉽단말이야? 하며 약간 허무하기도 했습니다.(ㅎㅎ)

진작 상태 관리의 개념을 알았더라면 설계 단계에서부터 라이브러리는 어떤 걸 쓰고 어떻게 접근해야 될지 계획이 잘 잡혔을 텐데라는 아쉬움도 많았습니다.
하지만 이런 시행착오를 겪는 과정이 있어 더 발전할 수 있는 공부가 되었다고 생각합니다.

### 참조
- [Learn React by creating a comment app(By Mohd Saqueib)](https://www.qcode.in/learn-react-by-creating-a-comment-app/)
- [[React.JS] 강좌 5편 컴포넌트의 State 와 Props 사용하기(By velopert)](https://velopert.com/921)
- [Redux 코드로 이해하기 (By Jei's blog)](https://fullest-sway.me/blog/2017/06/21/redux-use/)
- [우아한형제들 블로그](http://woowabros.github.io/experience/2019/01/02/kimcj-react-mobx.html)
- [MobX 내부 살펴보기](http://www.secmem.org/blog/2019/03/09/mobx-internals/)
- [MobX (By 박스여우)](https://boxfoxs.tistory.com/383)