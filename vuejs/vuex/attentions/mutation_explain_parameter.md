### mutations参数说明

mutations.js中的函数可以传一个参数

`[事件名](state)`

参数state 指的是store中state.js的所有的数据信息。


mutations.js中的函数一般是传两个参数

`[事件名](state,data)`

上面的这两个参数，第一个参数是指store中的state.js中的所有的数据信息，而data是指action.js传过来的信息。

```javascript

[CHANGE_CURRENT_POSITION] (state, data) {
        console.log(data);
        if(data){
            _.extend(state.current, data)
        }
    }

```
