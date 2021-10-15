# Checklist do react-redux

***1.** Antes de começar*
- [ ] pensar como será o *formato* do seu estado global
- [ ] pensar quais actions serão necessárias na sua aplicação

***2.** Instalação*
- [ ] npx create-react-app my-app-redux;
- [ ] npm install --save redux react-redux;
- [ ] npm install.

 **Se a sua aplicação não terá outras páginas, não é necessário configurar as rotas. Caso contrário:**
- [ ]  npm install react-router-dom;
Em *src/index.js*: 
- [ ] Definir o BrowserRouter,  `<BrowserRouter>` ;
No arquivo *App.js*: 
- [ ]  Definir o Switch,  `<Switch>`  ;
- [ ] Definir a Route,  `<Route>`  .

***3.** Criar dentro do diretório src:*
- [ ] diretório actions;
- [ ] diretório reducers;
- [ ] diretório store.

***4.** Criar dentro do diretório actions:*
- [ ] arquivo index.js.

***5.** Criar dentro do diretório reducers:*
- [ ] arquivo index.js.

***6.** Criar dentro do diretório store:*
- [ ] arquivo index.js.

***7.** No arquivo App.js:*
- [ ] definir o Provider, `<Provider store={ store }>`, para fornecer os estados à todos os componentes encapsulados em `<App />`. `import { Provider } from  'react-redux'` (caso possua testes, isso deverá ser feito em index.js);

***8.** No arquivo store/index.js:*
- [ ] importar o rootReducer e criar a store
- [ ] se precisar instalar o Redux DevTools: `npm install --save redux-devtools-extension` 
- [ ] configurar o [Redux DevTools](https://github.com/reduxjs/redux-devtools)
```
import { createStore } from 'redux';
import { composeWithDevTools } from 'redux-devtools-extension';
import rootReducer from  '../reducer';

const store = createStore(rootReducer, composeWithDevTools());
export default store;
```
**Para actions assíncronas, usar redux-thunk (npm i redux-thunk)**
```
import { createStore, applyMiddleware } from 'redux';
import { composeWithDevTools } from 'redux-devtools-extension';
import thunk from 'redux-thunk';
import rootReducer from '../reducers';

const store = createStore(
  rootReducer,
  composeWithDevTools(
    applyMiddleware(thunk),
  ),
);

export default store;
```
***9.** Na pasta reducers:*
- [ ] criar os reducers necessários
```
import { MY_CASE } from  '../action';
import anyData from  '../data';

const  INITIAL_STATE = {
// myKey1: myValue,
// myKey2: someValueFromData,
// ....
};
const  myReducer = (state = INITIAL_STATE, action) => {
	switch (action.type) {
	case MY_CASE_ACTION_X:
		return {
			...state,
			myKey1: action.payload.myKey1,
			myKey2: action.payload.myKey2,			
	};
	default:
		return state;
	}
};
export default myReducer;
```
- [ ] configurar os exports do arquivo index.js
```
import { combineReducers } from  'redux';
import myReducer from  './myReducer';

const  rootReducer  =  combineReducers({
	mySemanticKey: myReducer,
});

export default rootReducer;
```

***10.** Na pasta actions:*
- [ ] criar os actionTypes, por exemplo: `const MY_CASE_ACTION_X = 'MY_CASE_ACTION_X';`
- [ ] criar os actions creators necessários
```
export const myActionFunction = (myKey1, myKey2) => ({
	type: MY_CASE_ACTION_X,
	payload: {
		myKey1,
		myKey2,
	},
});
```
***11.** Nos componentes:*
- [ ] import no component:
```
import { connect } from 'react-redux';
import { myActionFunction as myActionFunctionAction } from '../action';
```
- [ ] criar a função mapStateToProps
```
const  mapStateToProps  = (state) => ({
	myKey1: state.mySemanticKey.myKey1,
	myKey2: state.mySemanticKey.myKey2,
// ...
});
```
- [ ] criar a função mapDispatchToProps
```
const mapDispatchToProps = (dispatch) => ({
	myActionFunction: (myKey1, myKey2) => dispatch(myActionFunctionAction(myKey1, myKey2)),
});
```
- [ ] fazer o connect
```
export default connect(mapStateToProps, mapDispatchToProps)(MyComponent);
```
##
*Texto adaptado de Tiago Sathler e Diego Campos* 
