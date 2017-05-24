# 深入响应式原理
- 把一个普通 JavaScript 对象传给 Vue 实例的 data 选项，Vue 将遍历此对象所有的属性，并使用 Object.defineProperty 把这些属性全部转为 getter/setter。
- 每个组件实例都有相应的 watcher 实例对象，它会在组件渲染的过程中把属性记录为依赖，之后当依赖项的 setter 被调用时，会通知 watcher 重新计算，从而致使它关联的组件得以更新。
- Vue 不能检测到对象属性的添加或删除。由于 Vue 会在初始化实例时对属性执行 getter/setter 转化过程，所以属性必须在 data 对象上存在才能让 Vue 转换它，这样才能让它是响应的。
- Vue 不允许在已经创建的实例上动态添加新的根级响应式属性(root-level reactive property)。然而它可以使用 Vue.set(object, key, value) 方法或 vm.$set 实例方法将响应属性添加到嵌套的对象上。
- 由于 Vue 不允许动态添加根级响应式属性，所以你必须在初始化实例前声明根级响应式属性，哪怕只是一个空值。
- 只要观察到数据变化，Vue 将开启一个队列，并缓冲在同一事件循环中发生的所有数据改变。然后，在下一个的事件循环“tick”中，Vue 刷新队列并执行实际（已去重的）工作。
- Vue 在内部尝试对异步队列使用原生的 Promise.then 和 MutationObserver，如果执行环境不支持，会采用 setTimeout(fn, 0) 代替。
- 为了在数据变化之后等待 Vue 完成更新 DOM ，可以在数据变化之后立即使用 Vue.nextTick(callback) 。这样回调函数在 DOM 更新完成后就会调用。
- 在组件内使用 vm.$nextTick() 实例方法特别方便，因为它不需要全局 Vue ，并且回调函数中的 this 将自动绑定到当前的 Vue 实例上。

# 过渡效果
- Vue 提供了 transition 的封装组件，在下列情形中，可以给任何元素和组件添加 entering/leaving 过渡：
    * 条件渲染 （使用 v-if）
    * 条件展示 （使用 v-show）
    * 动态组件
    * 组件根节点
- 有 6 个(CSS)类名在 enter/leave 的过渡中切换：v-enter, v-enter-active, v-enter-to, v-leave, v-leave-active, v-leave-to.
- JavaScript过渡钩子：before-enter、enter、after-enter、enter-cancelled、before-leave、leave、after-leave、leave-cancelled。
- 当只用 JavaScript 过渡的时候， 在 enter 和 leave 中，回调函数 done 是必须的 。 否则，它们会被同步调用，过渡会立即完成。
- 推荐对于仅使用 JavaScript 过渡的元素添加 v-bind:css="false"，Vue 会跳过 CSS 的检测。这也可以避免过渡过程中 CSS 的影响。
- 多元素过渡：当有相同标签名的元素切换时，需要通过 key 特性设置唯一的值来标记以让 Vue 区分它们，否则 Vue 为了效率只会替换相同标签内部的内容。即使在技术上没有必要，给在 <transition> 组件中的多个元素设置 key 是一个更好的实践。
- 这是 <transition> 的默认行为 - 进入和离开同时发生。
- 同时生效的进入和离开的过渡不能满足所有要求，所以 Vue 提供了 过渡模式：in-out、out-in。
- 多个组件的过渡简单很多 - 我们不需要使用 key 特性。相反，我们只需要使用动态组件。
- 列表过渡：使用 <transition-group> 组件。
- <transition-group> 组件还有一个特殊之处。不仅可以进入和离开动画，还可以改变定位。要使用这个新功能只需了解新增的 v-move 特性，它会在元素的改变定位的过程中应用。
- 要创建一个可复用过渡组件，你需要做的就是将 <transition> 或者 <transition-group> 作为根组件，然后将任何子组件放置在其中就可以了。

# 过渡状态
- 通过 watcher 我们能监听到任何数值属性的数值更新。

# Render函数
- Vue 推荐在绝大多数情况下使用 template 来创建你的 HTML。然而在一些场景中，你真的需要 JavaScript 的完全编程的能力，这就是 render 函数，它比 template 更接近编译器。
- createElement()的参数......略
- createElement()的参数中，组件树中的所有 VNodes 必须是唯一的。
- 通过babel-plugin-transform-vue-jsx 插件，可以在Vue中使用JSX。
- 函数化组件（添加functional属性）：无状态的，无实例的。组件需要的一切都是通过context（上下文）传递。
- context包括以下属性：props、children、slots、data、parent、listeners、injections。
- 函数化组件中的slots().default代表匿名slot；children()代表了所有的slot，包括匿名的和具名的。
- 函数化组件渲染开销低，但是无法显示在Vue的Chrome dev tools中。
- Vue 的模板实际是编译成了 render 函数。

# 自定义指令
- 应用场景：需要手动操作DOM的时候。
- Vue.directive定义全局指令；或者用directives选项。
- 勾子函数：bind、inserted、update、componentUpdated、unbind。
- 勾子函数的参数......略

# 混合
- 混合是一种灵活的分布式复用 Vue 组件的方式。混合对象可以包含任意组件选项。
- 当组件和混合对象含有同名选项时，这些选项将以恰当的方式混合。比如，同名钩子函数将混合为一个数组，因此都将被调用。另外，混合对象的 钩子将在组件自身钩子 之前 调用。
- 值为对象的选项，例如 methods, components 和 directives，将被混合为同一个对象。 两个对象键名冲突时，取组件对象的键值对。

# 插件
- Vue.js 的插件应当有一个公开方法 install。
- 通过全局方法 Vue.use() 使用插件。
- 一些插件，如 vue-router 如果 Vue 是全局变量则自动调用 Vue.use() 。不过在模块环境中应当始终显式调用 Vue.use()。

# 单文件组件
- 略。

# 生产环境部署
- 在没有构建工具的情况下，直接引用 vue.min.js 文件即可。
- 在有构建工具的情况下，需要修改 process.env.NODE_ENV 变量。
- 如果在组件渲染时出现运行错误，错误将会被传递至全局 Vue.config.errorHandler 配置函数（如果已设置）。利用这个钩子函数和错误跟踪服务（如 Sentry，它为 Vue 提供官方集成），可能是个不错的主意。
- 使用单文件组件时，<style> 标签在开发运行过程中会被动态实时注入。这样会有移动的运行时开销，并且在做服务端渲染的时候会造成短暂的闪现（因为没有样式）。
- 所以，将所有的CSS抽取出来单独放在一个文件中可以避免上述问题，也方便了CSS压缩和浏览器缓存。

# 路由
- 略。

# 状态管理
- 详见vuex（类Flux实现）。
- Redux 事实上无法感知视图层，所以它能够轻松的通过一些简单绑定和Vue一起使用。vuex区别在于它是一个专门为 vue 应用所设计。这使得它能够更好地和vue进行整合，同时提供简洁的API和改善过的开发体验。

# 单元测试
- 可以使用 Karma 进行自动化测试。
- 由于 Vue 进行 异步更新DOM 的情况，一些依赖DOM更新结果的断言必须在 Vue.nextTick 回调中进行。

# 服务端渲染
- Nuxt 是一个基于 Vue 生态的更高层的框架，为开发服务端渲染的 Vue 应用提供了极其便利的开发体验。更酷的是，你甚至可以用它来做为静态站生成器。
