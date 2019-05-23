# Tips


## React Component
1. 程式碼 .bind(this)優化，使用arrow function 取代 -- [1](https://segmentfault.com/q/1010000017412221) , [2](https://carsonwah.github.io/react-native-arrow-function-and-this.html) 

> ant design 的範例都是使用這種寫法

2. PureComponent 謹慎使用，讓性能優化

> 比對前後props、state是否有改變，沒有改變shouldComponentUpdate會return false，則物件不會再次執行render()

3. 由於Immutable data structures的關係，使用PureComponent的shallowEqual可能會出錯，所以在setState之前，不能直接引用props或state，必須創建一個新的物件 -- [1](https://blog.techbridge.cc/2018/01/05/react-render-optimization/)

> 習慣必須養成不要直接調用props、state，需另創一個物件，如:const arr = [...this.state.array]

4. 在react中如果function想要傳遞參數，有兩種方法 [1]onClick={()=>this.myFunction(params)}, [2]onClick={this.myFunction.bind(this,params)} --[詳解arrow function in react](https://frontarm.com/james-k-nelson/when-to-use-arrow-functions/)

> 由於兩種方法都會創造新的函數，如果在render()中使用，每次重新render都會重新創造函數，會造成些許的效能問題

> 如果是用這兩種方法傳遞給child component 或 purecomponent，由於每次都創造新的函數，會使得purecomponent失效，解法如下[1](https://stackoverflow.com/questions/39226757/react-passing-parameter-with-arrow-function-in-child-component)

## React Router
1. 頁面傳值有三個方法： 1. props.params, 2. query, 3. state --[1](https://blog.csdn.net/qq_23158083/article/details/68488831)

> 文章說明query方法類似get，會併接url，而state類似post，不會以明文傳遞，但不知原因為何，實際使用兩者的url都沒有顯示，還是推薦使用state。