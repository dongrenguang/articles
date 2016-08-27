—— 摘自：[《ECMAScript 6入门》](http://es6.ruanyifeng.com/) [阮一峰](http://www.ruanyifeng.com/home.html)

# 1. ECMAScript 6简介
略。

# 2. let与const命令
+ let与const：不存在变量提升、暂时性死区、不允许重复声明
+ 块级作用域：允许声明函数
+ let与const声明的全局变量与全局对象（window or global）脱钩
+ ES6中声明变量的6种方法：var、function、let、const、import、class

# 3. 变量的解构赋值
+ 本质上，这种写法属于“模式匹配”，只要等号两边的模式相同，左边的变量就会被赋予对应的值。
+ 事实上，只要某种数据结构具有Iterator接口，都可以采用数组形式的解构赋值。
+ 数组、对象的解构赋值。
+ 字符串也可以解构赋值。这是因为此时，字符串被转换成了一个类似数组的对象。
+ 解构赋值时，如果等号右边是数值和布尔值，则会先转为对象。
+ 解构赋值的规则是，只要等号右边的值不是对象，就先将其转为对象。由于undefined和null无法转为对象，所以对它们进行解构赋值，都会报错。
+ 解构赋值的规则是，只要等号右边的值不是对象，就先将其转为对象。由于undefined和null无法转为对象，所以对它们进行解构赋值，都会报错。
+ 函数参数的解构赋值。“如果解构失败，x和y等于默认值。”
+ [圆括号问题](http://es6.ruanyifeng.com/#docs/destructuring#圆括号问题)：
  - 可以使用圆括号的情况只有一种：赋值语句的非模式部分，可以使用圆括号。
  - 不能使用圆括号的情况：
    * 变量声明语句中，不能带有圆括号。
    * 函数参数中，模式不能带有圆括号。
    * 赋值语句中，不能将整个模式，或嵌套模式中的一层，放在圆括号之中。

# 4. 字符串的扩展
+ codePointAt()：能够正确处理4个字节储存的字符，返回一个字符的码点。
+ String.fromCodePoint()：在作用上，正好与codePointAt方法相反。
+ at()：可以识别Unicode编号大于0xFFFF的字符，返回正确的字符。
+ includes()：返回布尔值，表示是否找到了参数字符串。
+ startsWith()：返回布尔值，表示参数字符串是否在源字符串的头部。
+ endsWith()：返回布尔值，表示参数字符串是否在源字符串的尾部。
+ repeat()：返回一个新字符串，表示将原字符串重复n次。
+ padStart()：用于头部补全。
+ padEnd()：用于尾部补全。
+ 模板字符串。
+ 标签模板，与String.raw()。

# 5. 正则的扩展
略。

# 6. 数值的扩展
+ Number.isFinite()与Number.isNaN()：它们与传统的全局方法`isFinite()`和`isNaN()`的区别在于，传统方法先调用`Number()`将非数值的值转为数值，再进行判断，而这两个新方法只对数值有效，非数值一律返回`false`。
+ Number.parseInt()与Number.parseFloat()：ES6将全局方法`parseInt()`和`parseFloat()`，移植到Number对象上面，行为完全保持不变。这样做的目的，是逐步减少全局性方法，使得语言逐步模块化。
+ Number.isInteger()：`Number.isInteger()`用来判断一个值是否为整数。
+ Number.EPSILON：ES6在Number对象上面，新增一个极小的常量`Number.EPSILON`。
+ 安全整数和Number.isSafeInteger()：JavaScript能够准确表示的整数范围在-2^53到2^53之间（不含两个端点），超过这个范围，无法精确表示这个值。ES6引入了`Number.MAX_SAFE_INTEGER`和`Number.MIN_SAFE_INTEGER`这两个常量，用来表示这个范围的上下限。
+ Math对象的扩展
  - Math.trunc()：用于去除一个数的小数部分，返回整数部分。
  - 其他......

# 7. 数组的扩展
+ Array.from()：Array.from方法用于将两类对象转为真正的数组：类似数组的对象（array-like object）和可遍历（iterable）的对象（包括ES6新增的数据结构Set和Map）。对于还没有部署该方法的浏览器，可以用Array.prototype.slice方法替代。Array.from还可以接受第二个参数，作用类似于数组的map方法，用来对每个元素进行处理，将处理后的值放入返回的数组。
+ Array.of()：Array.of方法用于将一组值，转换为数组。这个方法的主要目的，是弥补数组构造函数Array()的不足。因为参数个数的不同，会导致Array()的行为有差异。
+ 数组实例的copyWithin()：数组实例的copyWithin方法，在当前数组内部，将指定位置的成员复制到其他位置（会覆盖原有成员），然后返回当前数组。也就是说，使用这个方法，会修改当前数组。它接受三个参数。
    - target（必需）：从该位置开始替换数据。
    - start（可选）：从该位置开始读取数据，默认为0。如果为负值，表示倒数。
    - end（可选）：到该位置前停止读取数据，默认等于数组长度。如果为负值，表示倒数。
+ 数组实例的find()和findIndex()：数组实例的findIndex方法的用法与find方法非常类似，返回第一个符合条件的数组成员的位置，如果所有成员都不符合条件，则返回-1。
+ 数组实例的fill()：fill方法使用给定值，填充一个数组。fill方法还可以接受第二个和第三个参数，用于指定填充的起始位置和结束位置。
+ 数组实例的entries()，keys()和values()：ES6提供三个新的方法——entries()，keys()和values()——用于遍历数组。它们都返回一个遍历器对象（详见《Iterator》一章），可以用for...of循环进行遍历，唯一的区别是keys()是对键名的遍历、values()是对键值的遍历，entries()是对键值对的遍历。
+ 数组实例的includes()：Array.prototype.includes方法返回一个布尔值，表示某个数组是否包含给定的值，与字符串的includes方法类似。该方法属于ES7。该方法的第二个参数表示搜索的起始位置，默认为0。如果第二个参数为负数，则表示倒数的位置，如果这时它大于数组长度（比如第二个参数为-4，但数组长度为3），则会重置为从0开始。可正确处理NaN（indexOf方法不能）。
+ 数组的空位：ES6明确将空位转为undefined。由于空位的处理规则非常不统一，所以建议避免出现空位。

# 8. 函数的扩展
+ `函数参数的默认值`：指定了默认值以后，函数的length属性，将返回没有指定默认值的参数个数。也就是说，指定了默认值后，length属性将失真。这是因为length属性的含义是，该函数预期传入的参数个数。某个参数指定默认值以后，预期传入的参数个数就不包括这个参数了。同理，rest参数也不会计入length属性。如果设置了默认值的参数不是尾参数，那么length属性也不再计入后面的参数了。如果参数的默认值是一个函数，该函数的作用域是其声明时所在的作用域。
+ `rest参数`：ES6引入rest参数（形式为“...变量名”），用于获取函数的多余参数，这样就不需要使用arguments对象了。
+ `扩展运算符`：rest参数的逆运算，将一个数组转为用逗号分隔的参数序列。任何Iterator接口的对象，都可以用扩展运算符转为真正的数组。对于那些没有部署Iterator接口的类似数组的对象，扩展运算符就无法将其转为真正的数组（可用Array.from()）。
+ `将类似于数组对象转换成数组的三种方法`：Array.prototype.slice.call()、Array.from()、[...arrayLikeObject]。
+ `name属性`：函数的name属性，返回该函数的函数名。
+ `箭头函数`：由于大括号被解释为代码块，所以如果箭头函数直接返回一个对象，必须在对象外面加上括号。注意点：
    - 函数体内的this对象，就是定义时所在的对象，而不是使用时所在的对象。
    - 不可以当作构造函数，也就是说，不可以使用new命令，否则会抛出一个错误。
    - 不可以使用arguments对象，该对象在函数体内不存在。如果要用，可以用Rest参数代替。
    - 不可以使用yield命令，因此箭头函数不能用作Generator函数。

    this指向的固定化，并不是因为箭头函数内部有绑定this的机制，实际原因是箭头函数根本没有自己的this，导致内部的this就是外层代码块的this。正是因为它没有this，所以也就不能用作构造函数。除了this，以下三个变量在箭头函数之中也是不存在的，指向外层函数的对应变量：arguments、super、new.target。另外，由于箭头函数没有自己的this，所以当然也就不能用call()、apply()、bind()这些方法去改变this的指向。
+ `尾调用优化`：尾调用（Tail Call）是函数式编程的一个重要概念，本身非常简单，一句话就能说清楚，就是指某个函数的最后一步是调用另一个函数。“尾调用优化”（Tail call optimization），即只保留内层函数的调用帧。如果所有函数都是尾调用，那么完全可以做到每次执行时，调用帧只有一项，这将大大节省内存。这就是“尾调用优化”的意义。

# 9. 对象的扩展
+ `Object.is()`: 它用来比较两个值是否严格相等，与严格比较运算符（===）的行为基本一致。不同之处只有两个：一是+0不等于-0，二是NaN等于自身。
+ `Object.assign()`: 拷贝的属性是有限制的，只拷贝源对象的自身属性（不拷贝继承属性），也不拷贝不可枚举的属性（enumerable: false）。Object.assign方法实行的是浅拷贝，而不是深拷贝。也就是说，如果源对象某个属性的值是对象，那么目标对象拷贝得到的是这个对象的引用。对于这种嵌套的对象，一旦遇到同名属性，Object.assign的处理方法是替换，而不是添加。
+ `属性的遍历`：
    - （1）`for...in`:
    for...in循环遍历对象自身的和继承的可枚举属性（不含Symbol属性）。
    - （2）`Object.keys(obj)`:
    Object.keys返回一个数组，包括对象自身的（不含继承的）所有可枚举属性（不含Symbol属性）。
    - （3）`Object.getOwnPropertyNames(obj)`:
    Object.getOwnPropertyNames返回一个数组，包含对象自身的所有属性（不含Symbol属性，但是包括不可枚举属性）。
    - （4）`Object.getOwnPropertySymbols(obj)`:
    Object.getOwnPropertySymbols返回一个数组，包含对象自身的所有Symbol属性。
    - （5）`Reflect.ownKeys(obj)`:
    Reflect.ownKeys返回一个数组，包含对象自身的所有属性，不管是属性名是Symbol或字符串，也不管是否可枚举。

# 10. Symbol
+ `Symbol.for()`: Symbol.for()与Symbol()这两种写法，都会生成新的Symbol。它们的区别是，前者会被登记在全局环境中供搜索，后者不会。Symbol.for()不会每次调用就返回一个新的Symbol类型的值，而是会先检查给定的key是否已经存在，如果不存在才会新建一个值。
+ `Symbol.keyFor`: Symbol.keyFor方法返回一个已登记的Symbol类型值的key。
+ `内置的Symbol值`: 略。

# 11. Proxy和Reflect
+ `Proxy`: Proxy可以理解成，在目标对象之前架设一层“拦截”，外界对该对象的访问，都必须先通过这层拦截，因此提供了一种机制，可以对外界的访问进行过滤和改写。
```JavaScript
var proxy = new Proxy(target, handler);
```
对于可以设置、但没有设置拦截的操作，则直接落在目标对象上，按照原先的方式产生结果。

    - （1）`get(target, propKey, receiver)`: 拦截对象属性的读取，比如proxy.foo和proxy['foo']。最后一个参数receiver是一个对象，可选，参见下面Reflect.get的部分。
    - （2）`set(target, propKey, value, receiver)`: 拦截对象属性的设置，比如proxy.foo = v或proxy['foo'] = v，返回一个布尔值。
    - （3）`has(target, propKey)`: 拦截propKey in proxy的操作，以及对象的hasOwnProperty方法，返回一个布尔值。
    - （4）`deleteProperty(target, propKey)`: 拦截delete proxy[propKey]的操作，返回一个布尔值。
    - （5）`ownKeys(target)`: 拦截Object.getOwnPropertyNames(proxy)、Object.getOwnPropertySymbols(proxy)、Object.keys(proxy)，返回一个数组。该方法返回对象所有自身的属性，而Object.keys()仅返回对象可遍历的属性。

    - （6）`getOwnPropertyDescriptor(target, propKey)`: 拦截Object.getOwnPropertyDescriptor(proxy, propKey)，返回属性的描述对象。
    - （7）`defineProperty(target, propKey, propDesc)`: 拦截Object.defineProperty(proxy, propKey, propDesc）、Object.defineProperties(proxy, propDescs)，返回一个布尔值。
    - （8）`preventExtensions(target)`: 拦截Object.preventExtensions(proxy)，返回一个布尔值。
    - （9）`getPrototypeOf(target)`: 拦截Object.getPrototypeOf(proxy)，返回一个对象。
    - （10）`isExtensible(target)`: 拦截Object.isExtensible(proxy)，返回一个布尔值。
    - （11）`setPrototypeOf(target, proto)`: 拦截Object.setPrototypeOf(proxy, proto)，返回一个布尔值。如果目标对象是函数，那么还有两种额外操作可以拦截。
    - （12）`apply(target, object, args)`: 拦截Proxy实例作为函数调用的操作，比如proxy(...args)、proxy.call(object, ...args)、proxy.apply(...)。
    - （13）`construct(target, args)`: 拦截Proxy实例作为构造函数调用的操作，比如new proxy(...args)。

+ Proxy.revocable()
    - Proxy.revocable方法返回一个可取消的Proxy实例。

+ Reflect
    - Reflect对象与Proxy对象一样，也是ES6为了操作对象而提供的新API。Reflect对象的设计目的有这样几个。
        + （1） 将Object对象的一些明显属于语言内部的方法（比如Object.defineProperty），放到Reflect对象上。现阶段，某些方法同时在Object和Reflect对象上部署，未来的新方法将只部署在Reflect对象上。
        + （2） 修改某些Object方法的返回结果，让其变得更合理。比如，Object.defineProperty(obj, name, desc)在无法定义属性时，会抛出一个错误，而Reflect.defineProperty(obj, name, desc)则会返回false。
        + （3） 让Object操作都变成函数行为。某些Object操作是命令式，比如name in obj和delete obj[name]，而Reflect.has(obj, name)和Reflect.deleteProperty(obj, name)让它们变成了函数行为。
        + （4）Reflect对象的方法与Proxy对象的方法一一对应，只要是Proxy对象的方法，就能在Reflect对象上找到对应的方法。这就让Proxy对象可以方便地调用对应的Reflect方法，完成默认行为，作为修改行为的基础。也就是说，不管Proxy怎么修改默认行为，你总可以在Reflect上获取默认行为。

# 12. 二进制数组
它很像C语言的数组，允许开发者以数组下标的形式，直接操作内存，大大增强了JavaScript处理二进制数据的能力，使得开发者有可能通过JavaScript与操作系统的原生接口进行二进制通信。
+ `ArrayBuffer对象`: 代表内存之中的一段二进制数据，可以通过“视图”进行操作。“视图”部署了数组接口，这意味着，可以用数组的方法操作内存。
+ `TypedArray视图`: 共包括9种类型的视图，比如Uint8Array（无符号8位整数）数组视图, Int16Array（16位整数）数组视图, Float32Array（32位浮点数）
+ `复合视图`: 由于视图的构造函数可以指定起始位置和长度，所以在同一段内存之中，可以依次存放不同类型的数据，这叫做“复合视图”。
+ `DataView视图`:可以自定义复合格式的视图，比如第一个字节是Uint8（无符号8位整数）、第二、三个字节是Int16（16位整数）、第四个字节开始是Float32（32位浮点数）等等，此外还可以自定义字节序。
+ `二进制数组的应用`: 大量的Web API用到了ArrayBuffer对象和它的视图对象。

详略。
