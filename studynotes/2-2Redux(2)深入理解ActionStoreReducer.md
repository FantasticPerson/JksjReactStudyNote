##  Redux(2) 深入理解 Action ，Store ，Reducer

#### 1. 理解 Store

```js
const store = createStore(reducer)
```

Store 对象有三个方法

1. getSate()
2. dispatch(action)
3. subscribe(listener)

#### 2. 理解 Action

一个 Action 其实是描述了一个行为的数据结构

```js
{
    type: ADD_TODO
    text: 'Build my first Redux App'
}
```

#### 3.理解 Reducer

Reducer 里面才是真正更新了 State 并且真正处理了 Action

一个 Action 通过 Store dispatch 出去，所有的 Reducer 都会收到，Reducer 通过 Action.type 来判断自己能不能处理

```js
const counter = (state = initialState, action) => {
    switch (action.type) {
      case "PLUS_ONE":
        return { count: state.count + 1 };
      case "MINUS_ONE":
        return { count: state.count - 1 };
      case "CUSTOM_COUNT":
        return {
          count: state.count + action.payload.count
        };
      default:
        break;
    }
    return state;
  };
```
可以看到 Rducer 每次 action 处理完毕，都是返回的一个新的 state 对象，而不是在原有的 state 对象基础上修改

（state ,action） => new state
这个样保证了一个 Redux 应用是可以很好的被追踪，如果出现了问题，可以很快的定位到是哪个 action 触发了问题

#### 实际使用过程中会使用的几个工具函数

1. combineRducers()  
    多个 reducers 的情况下，通过 combineRducers 进行绑定
    ```js
    combineRducers({
        todos,
        counter
    })
    ```
    会返回一个新的 reduer 对象


2. bindActionCreators() 
    这个是用来帮助我们更好的使用 action ，创建完一步 dispatch
    ```js
    const plusOne = bindActionCreators(action, dispatch)
    ```

