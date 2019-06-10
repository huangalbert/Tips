# Tips

整理一些文章與小知識，以供複習或尋找solution


## React Component
1. 程式碼 .bind(this)優化，使用arrow function 取代 -- [1](https://segmentfault.com/q/1010000017412221) , [2](https://carsonwah.github.io/react-native-arrow-function-and-this.html) 

> ant design 的範例都是使用這種寫法

2. PureComponent 謹慎使用，讓性能優化

> 比對前後props、state是否有改變，沒有改變shouldComponentUpdate會return false，則物件不會再次執行render()

3. 由於Immutable data structures的關係，使用PureComponent的shallowEqual可能會出錯(不如預期)，所以在setState之前，不能直接引用props或state，必須創建一個新的物件 -- [1](https://blog.techbridge.cc/2018/01/05/react-render-optimization/)

> 習慣必須養成不要直接調用props、state，需另創一個物件，如:const arr = [...this.state.array]

4. 在react中如果function想要傳遞參數，有兩種方法 [1]onClick={()=>this.myFunction(params)}, [2]onClick={this.myFunction.bind(this,params)} --[詳解arrow function in react](https://frontarm.com/james-k-nelson/when-to-use-arrow-functions/)

> 由於兩種方法都會創造新的函數，如果在render()中使用，每次重新render都會重新創造函數，會造成些許的效能問題

> 如果是用這兩種方法傳遞給child component 或 purecomponent，由於每次都創造新的函數，會使得purecomponent失效，解法如下-[1](https://stackoverflow.com/questions/39226757/react-passing-parameter-with-arrow-function-in-child-component)

> 不需要排斥使用這樣的寫法，但在撰寫程式時可以盡量縮減，當網頁有效能問題時，可以再回來構思如何修改。

5. 卸除component時(componentWillUnmount階段)，不要有setState()的執行

> 雖然有此情況不會造成程式崩壞，但會有warning，本次經驗是在使用者請求資料後，突然放棄等候而跳頁產生。

6. 承5，必須在componentWillUnmount階段剔除listener或者setInerval等等--[1](https://www.robinwieruch.de/react-warning-cant-call-setstate-on-an-unmounted-component/)

7. 

## React Router
1. 頁面傳值有三個方法： 1. props.params, 2. query, 3. state --[1](https://blog.csdn.net/qq_23158083/article/details/68488831)

> 文章說明query方法類似get，會併接url，而state類似post，不會以明文傳遞，但不知原因為何，實際使用兩者的url都沒有顯示，還是推薦使用state。

## Axios
1. 在IE中使用axios，安裝babel-polyfill，在import時必須擺在第一個。

> 由於IE沒支援promise語法，需要使用額外套件編譯。

## javascript

1. 提升(Hoisting)，若是某行程式碼需要取得的變數宣告在其後執行，編譯器會自動幫程式碼在最上頭加上var x，此時值為undefined，直到程式執行給值那行--[1](https://ithelp.ithome.com.tw/articles/10191549)

> 函數物件同樣會被hoisting, 如: var x = function(){...}, 單純函數不會。

2. callback function 與 IIEF --[1](https://ithelp.ithome.com.tw/articles/10192739)

> 把函數當成另一個函數的參數，主要作用在制定函數執行順序，徹底理解文章中舉的例子。

3. 同步(Synchronous) 與 非同步(Asynchronous)--[1](https://ithelp.ithome.com.tw/articles/10194569)

> Callback Hell : 大量使用非同步且又想要依照固定的順序來執行時， 就可能會出現

> 使用promise語法來避免callback hell --[1 promise語法使用概念](https://codertw.com/%E7%A8%8B%E5%BC%8F%E8%AA%9E%E8%A8%80/148940/)

4. 非侵入式javascript --[1](https://segmentfault.com/a/1190000008820759)

> 這樣的寫法可以分離HTML與javascript，達成視圖與邏輯分離的架構，程式碼便不會全部混雜在一起。但如此一來，單看HTML的element無法知道他被綁定了甚麼事件，必須要去查詢js document中的所有監聽事件。

> React 中的 JSX寫法反其道而行，兩者互相結合，將component合適的切割分層，程式碼便不會看起來混亂。

5. Pass by value、 Pass by reference 、Pass by sharing(scope的關係) --[1](https://ithelp.ithome.com.tw/articles/10191057)

> 物件、陣列可變，基本型不可變

6. 事件的註冊綁定-[1] on-event(HTML屬性), [2] on-event (非HTML屬性), [3] EventTarget.addEventListener()

7. event capturing & event bubbling (event flow)--[1](https://ithelp.ithome.com.tw/articles/10191970)

> 必須深刻了解其傳遞方式

8. 阻擋事件冒泡 e.stopPropagation() --[1](https://ithelp.ithome.com.tw/articles/10192015)

> e.stopPropagation()、this的導向、event.currentTarget、Event Delegation

> 文章中所提到的重點：e.target 其實是「觸發事件的元素」，而 this 指的是「觸發事件的目標」元素，也就是 event.currentTarget

9. event.preventDefault() 可在addEventListener使用，讓element的原始動作失效。

> return false也能有同樣效果

10. rest operate &　spread orperate --[1](https://pjchender.blogspot.com/2017/01/es6-spread-operatorrest-operator.html)

11. lodash & lazy 提升js程式碼可維護性、效能。

> 注意不要過早優化程式效能，初期開發階段，可維護性、可讀性、可測試性更為重要。

12. clean code for js --[1](https://github.com/ryanmcdermott/clean-code-javascript#use-promises-not-callbacks)

13. map & reduce --[1](http://fred-zone.blogspot.com/2017/01/javascript-mapreduce.html)

#moment.js

1. moment.js 函數整理(中文) --[1](https://my.oschina.net/Tsybius2014/blog/724293)










