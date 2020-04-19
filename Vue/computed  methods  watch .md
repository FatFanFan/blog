## Vue.js 的 computed、methods、 watch 用法与区别
## 1. computed 计算属性
> 类型：{ [key: string]: Function | { get: Function, set: Function } }
- 计算属性默认只有 getter
- 计算属性将被混入到 Vue 实例中。所有 getter 和 setter 的 this 上下文自动地绑定为 Vue 实例。
- 计算属性的结果会被缓存，除非依赖的响应式**属性变化**才会重新计算。注意，如果某个依赖 (比如非响应式属性) 在该实例范畴之外，则计算属性是**不会**被更新的。

## 2. methods 方法
>类型：{ [key: string]: Function }
- methods 将被混入到 Vue 实例中。可以直接通过 VM 实例访问这些方法，或者在指令表达式中使用。方法中的 this 自动绑定为 Vue 实例。

## 3. watch 侦听属性
>类型：{ [key: string]: string | Function | Object | Array }
- 一个对象，键是需要观察的表达式，值是对应回调函数。回调函数得到的参数为新值和旧值。值也可以是方法名，或者包含选项的对象。Vue 实例将会在实例化时调用 $watch()，遍历 watch 对象的每一个属性。
### 3.1 vm.$watch( expOrFn, callback, [options] )
- 参数 ：
```
{string | Function} expOrFn
{Function | Object} callback
{Object} [options]
     - {boolean} deep
     - {boolean} immediate
```
- 返回值：{Function} unwatch vm   
 $watch 返回一个取消观察函数，用来停止触发回调
- 用法： 观察 Vue 实例变化的一个表达式或计算属性函数。回调函数得到的参数为新值和旧值。表达式只接受监督的键路径。对于更复杂的表达式，用一个函数取代。



## 4. 计算属性缓存 vs 方法 vs 侦听属性
- 计算属性：基于它们的依赖进行缓存的。只在相关依赖发生改变时它们才会重新求值
- 方法：每当触发重新渲染时，调用方法将总会再次执行函数。
- 侦听属性：使用 watch 选项允许我们执行异步操作 (访问一个 API)，限制我们执行该操作的频率，并在我们得到最终结果前，设置中间状态。这些都是计算属性无法做到的。当需要在数据变化时执行异步或开销较大的操作时，这个方式是最有用的。