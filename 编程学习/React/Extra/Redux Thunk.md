- 只有使用 Redux Toolkit 的 dispatch 函数才可以修改 store 中的数据
- dispatch 是 redux-thunk 的内置函数，用于触发 action（这个 action 在 reducers 中）
- 在使用Redux Thunk时，当您在组件中调用`fetchChannlList`函数并将其作为action传递给`dispatch`时，Redux Thunk中间件会自动提供`dispatch`函数作为参数给`fetchChannlList`返回的函数。这样，您就可以在异步操作完成后使用该`dispatch`函数来更新Redux store的状态。
``` js
import { createSlice } from '@reduxjs/toolkit';
const ChannelStore = createSlice({
    name: 'channel',
    //初始化State
    initialState: {
        channelsList: []
    },
    //修改状态的方法 同步方法 支持同步修改
    reducers: {
        addChannel(state, action) {
            state.channelsList.push(action.payload);
        },
        removeChannel(state, action) {
            state.channelsList = state.channelsList.filter(channel => channel.id !== action.payload.id);
        },
        setChannels(state, action) {
            state.channelsList = action.payload;
        }
    }
})

// 异步请求
const fetchChannels = () => {
    return async (dispatch) => {
        const res = await fetch('http://localhost:3000/channels');
        const data = await res.json();
        dispatch(setChannels(data));
    }
}

const { addChannel, removeChannel, setChannels } = ChannelStore.actions;

const ChannelReducer = ChannelStore.reducer;

export { ChannelReducer }

export { addChannel, removeChannel, setChannels }
export default ChannelStore;
```


>- 在 Redux Toolkit 中，通常使用 `createAsyncThunk` 来处理异步逻辑，但是在这个例子中，`fetchChannels` 函数是一个手写的 thunk 函数。Thunk 函数是一种用于延迟执行某个操作的特殊函数，它可以在稍后的某个时间点执行，通常是异步操作完成后。
>- 在 Redux 中，thunk 函数允许你编写包含异步逻辑的 action creators。这些 thunk 函数可以返回一个函数，这个函数接收 `dispatch` 和 `getState` 作为参数。返回的函数可以执行异步操作，并在操作完成后使用 `dispatch` 来分发一个或多个同步 actions。
>- 在这个例子中，`fetchChannels` 函数返回一个匿名函数，这个函数是异步的，它使用 `await` 等待 `fetch` 请求的响应，并将响应数据解析为 JSON。然后，它使用 `dispatch` 分发一个 `setChannels` action，将获取到的频道数据更新到状态树中。
>- 为什么要返回一个函数呢？这是因为 Redux 的 middleware 机制。Redux Thunk middleware 允许 action creators 返回一个函数而不是一个 action 对象。这个 middleware 会检测 action creator 返回的值，如果它是一个函数，middleware 会调用这个函数，并传递 `dispatch` 和 `getState` 作为参数。这样，你就可以在 thunk 函数中执行任何异步操作，并在适当的时候分发 actions。
>- 这种模式的好处是，它允许你在 action creator 中处理异步逻辑，而不需要将异步逻辑放在组件中，这样可以使组件更专注于 UI 的渲染和用户交互，而将数据获取和状态更新的逻辑放在 action creators 中。
