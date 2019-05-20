# Tips


## React Component
1. 程式碼 .bind(this)優化，使用arrow function 取代 -- [1](https://segmentfault.com/q/1010000017412221) , [2](https://carsonwah.github.io/react-native-arrow-function-and-this.html) 

> ant design 的範例都是使用這種寫法

2. PureComponent 謹慎使用，讓性能優化

> 比對前後props、state是否有改變，沒有改變shouldComponentUpdate會return false，則物件不會再次執行render()

3. 由於Immutable data structures的關係，使用PureComponent的shallowEqual可能會出錯，所以在setState之前，不能直接引用props或state，必須創建一個新的物件 -- [1](https://blog.techbridge.cc/2018/01/05/react-render-optimization/)

> 習慣必須養成不要直接調用props、state，需另創一個物件，如:const arr = [...this.state.array]