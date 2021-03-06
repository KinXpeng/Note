#### v-if和v-for的那个优先级更高，如果两个同时出现，应该怎么优化得到更好的性能？

- 先上结论：

  - **2.x 当 v-if 与 v-for 一起使用时，v-for 具有比 v-if 更高的优先级。**
- **3.x当 v-if 与 v-for 一起使用时，v-if 具有比 v-for 更高的优先级**。

- vue2：
  - v-for优先于v-if被解析。
  - 如果同时出现，每次渲染都会先执行循环在判断条件，无论如何循环都不可避免，浪费了性能。
  - 要避免出现这种情况，在外层嵌套`template`，在这一层进行v-if判断，然后在内部进行v-for循环

- vue3：
  - 可以一起使用，但不建议。

####  vue组件data为什么必须是个函数，而vue根实例则没有此限制？

- **1、data必须是个函数是保证在多实例的时候，为了保护相互之间的状态不干扰，不污染**

- **2、每次在创建根实例的时候，使用new的方式，全局的范围内只创建一个，不会创建多个，不会存在污染的问题，因此可以不使用函数**
  - 函数每次执行都会返回全新的data对象实例

- 结论：

  vue组件可能存在多个实例，如果使用对象形式定义data，则会导致他们共用一个data对象，那么状态变更将会影响所有的组件实例，这是不合理的；  采用函数形式定义没在initData是会将其作为工厂函数返回全新data对象，有效规避多实例之间的状态污染问题，  而在vue根实例创建过程中则不存在改限制，也是因为根实例只能有一个，不需要担心这种问题。

#### key工作原理

- 可以唯一确定一个dom元素，从而执行diff算法更高效

- 结论：

  1、key的作用主要是为了高效的更新虚拟DOM，其原理是vue在patch过程中通过**key可以精准的判断两个节点是否是同一个，从而避免频繁更新不同元素，使得整个patch过程更加高效，减少了dom的操作量**，提高性能

  2、如果不设置key可能在列表更新时引发一些隐藏的bug 比如说更新和不更新看不出来。

  3、vue中在使用相同标签名元素的过渡切换是，也会用到key属性，其目的也是为了让vue可以区分他们，否则vue只会替换其内部属性而不会触发过渡效果。需要用key来作为唯一性的判断。

#### 怎么理解vue中的diff算法

- 总结：

  diff算法：并非vue中专用，凡是涉及到虚拟dom中都有diff算法
  必要性：diff算法能精确的比较新旧虚拟DOM中的key的变化，从而提高更新效率
  执行方式：深度优先，同级比较
  高效性：查看源码得知

- 11