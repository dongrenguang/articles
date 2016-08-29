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

 Reflect对象与Proxy对象一样，也是ES6为了操作对象而提供的新API。Reflect对象的设计目的有这样几个。
    * （1） 将Object对象的一些明显属于语言内部的方法（比如Object.defineProperty），放到Reflect对象上。现阶段，某些方法同时在Object和Reflect对象上部署，未来的新方法将只部署在Reflect对象上。
    * （2） 修改某些Object方法的返回结果，让其变得更合理。比如，Object.defineProperty(obj, name, desc)在无法定义属性时，会抛出一个错误，而Reflect.defineProperty(obj, name, desc)则会返回false。
    * （3） 让Object操作都变成函数行为。某些Object操作是命令式，比如name in obj和delete obj[name]，而Reflect.has(obj, name)和Reflect.deleteProperty(obj, name)让它们变成了函数行为。
    * （4）Reflect对象的方法与Proxy对象的方法一一对应，只要是Proxy对象的方法，就能在Reflect对象上找到对应的方法。这就让Proxy对象可以方便地调用对应的Reflect方法，完成默认行为，作为修改行为的基础。也就是说，不管Proxy怎么修改默认行为，你总可以在Reflect上获取默认行为。

# 12. 二进制数组
它很像C语言的数组，允许开发者以数组下标的形式，直接操作内存，大大增强了JavaScript处理二进制数据的能力，使得开发者有可能通过JavaScript与操作系统的原生接口进行二进制通信。
+ `ArrayBuffer对象`: 代表内存之中的一段二进制数据，可以通过“视图”进行操作。“视图”部署了数组接口，这意味着，可以用数组的方法操作内存。
+ `TypedArray视图`: 共包括9种类型的视图，比如Uint8Array（无符号8位整数）数组视图, Int16Array（16位整数）数组视图, Float32Array（32位浮点数）
+ `复合视图`: 由于视图的构造函数可以指定起始位置和长度，所以在同一段内存之中，可以依次存放不同类型的数据，这叫做“复合视图”。
+ `DataView视图`:可以自定义复合格式的视图，比如第一个字节是Uint8（无符号8位整数）、第二、三个字节是Int16（16位整数）、第四个字节开始是Float32（32位浮点数）等等，此外还可以自定义字节序。
+ `二进制数组的应用`: 大量的Web API用到了ArrayBuffer对象和它的视图对象。

详略。

# 13. Set和Map数据结构
+ Set
    - Set函数可以接受一个数组（或类似数组的对象）作为参数，用来初始化。
    - Set结构的实例有以下属性。
        * Set.prototype.constructor：构造函数，默认就是Set函数。
        * Set.prototype.size：返回Set实例的成员总数。
    - 实例方法：
        * add(value)：添加某个值，返回Set结构本身。
        * delete(value)：删除某个值，返回一个布尔值，表示删除是否成功。
        * has(value)：返回一个布尔值，表示该值是否为Set的成员。
        * clear()：清除所有成员，没有返回值。
        * keys()：返回键名的遍历器
        * values()：返回键值的遍历器
        * entries()：返回键值对的遍历器
        * forEach()：使用回调函数遍历每个成员，第一第二个参数都是value值
    - Set的遍历顺序就是插入顺序。
    - Array.from方法可以将Set结构转为数组。
    - Set结构的实例默认可遍历，它的默认遍历器生成函数就是它的values方法。这意味着，可以省略values方法，直接用for...of循环遍历Set。
    - 扩展运算符（...）内部使用for...of循环，所以也可以用于Set结构。而for...of循环内部调用的是数据结构的Symbol.iterator方法。
+ WeakSet
    - WeakSet结构与Set类似，也是不重复的值的集合。但是，它与Set有两个区别。
        * 首先，WeakSet的成员只能是对象，而不能是其他类型的值。
        * 其次，WeakSet中的对象都是弱引用，即垃圾回收机制不考虑WeakSet对该对象的引用，也就是说，如果其他对象都不再引用该对象，那么垃圾回收机制会自动回收该对象所占用的内存，不考虑该对象还存在于WeakSet之中。这个特点意味着，无法引用WeakSet的成员，因此WeakSet是不可遍历的。
    - WeakSet结构有以下三个方法。
        * WeakSet.prototype.add(value)：向WeakSet实例添加一个新成员。
        * WeakSet.prototype.delete(value)：清除WeakSet实例的指定成员。
        * WeakSet.prototype.has(value)：返回一个布尔值，表示某个值是否在WeakSet实例之中。
    - WeakSet没有size属性，没有办法遍历它的成员。
    - WeakSet不能遍历，是因为成员都是弱引用，随时可能消失，遍历机制无法保证成员的存在，很可能刚刚遍历结束，成员就取不到了。WeakSet的一个用处，是储存DOM节点，而不用担心这些节点从文档移除时，会引发内存泄漏。
+ Map
    - 类似于对象，也是键值对的集合，但是“键”的范围不限于字符串，各种类型的值（包括对象）都可以当作键。
    - 作为构造函数，Map也可以接受一个数组作为参数。该数组的成员是一个个表示键值对的数组。
    - Map结构的实例有以下属性和操作方法:
        * （1）size属性
        * （2）set(key, value)
        * （3）get(key)
        * （4）has(key)
        * （5）delete(key)
        * （6）clear()
    - Map原生提供三个遍历器生成函数和一个遍历方法。    
        * keys()：返回键名的遍历器。
        * values()：返回键值的遍历器。
        * entries()：返回所有成员的遍历器。
        * forEach()：遍历Map的所有成员。
    - Map的遍历顺序就是插入顺序。
    - Map结构的默认遍历器接口（Symbol.iterator属性），就是entries方法。
+ WeakMap
    - WeakMap结构与Map结构基本类似，唯一的区别是它只接受对象作为键名（null除外），不接受其他类型的值作为键名，而且键名所指向的对象，不计入垃圾回收机制。
    - WeakMap的设计目的在于，键名是对象的弱引用（垃圾回收机制不将该引用考虑在内），所以其所对应的对象可能会被自动回收。当对象被回收后，WeakMap自动移除对应的键值对。典型应用是，一个对应DOM元素的WeakMap结构，当某个DOM元素被清除，其所对应的WeakMap记录就会自动被移除。基本上，WeakMap的专用场合就是，它的键所对应的对象，可能会在将来消失。WeakMap结构有助于防止内存泄漏。
    - WeakMap与Map在API上的区别主要是两个，一是没有遍历操作（即没有key()、values()和entries()方法），也没有size属性；二是无法清空，即不支持clear方法。这与WeakMap的键不被计入引用、被垃圾回收机制忽略有关。因此，WeakMap只有四个方法可用：get()、set()、has()、delete()。

# 14. Iterator和for...of循环
+ Iterator的作用有三个：一是为各种数据结构，提供一个统一的、简便的访问接口；二是使得数据结构的成员能够按某种次序排列；三是ES6创造了一种新的遍历命令for...of循环，Iterator接口主要供for...of消费。
+ 凡是部署了Symbol.iterator属性的数据结构，就称为部署了遍历器接口。调用这个接口，就会返回一个遍历器对象。
+ 当使用for...of循环遍历某种数据结构时，该循环会自动去寻找Iterator接口。
+ 在ES6中，有三类数据结构原生具备Iterator接口：数组、某些类似数组的对象、Set和Map结构。
+ 一个对象如果要有可被for...of循环调用的Iterator接口，就必须在Symbol.iterator的属性上部署遍历器生成方法（原型链上的对象具有该方法也可）。
+ 对于类似数组的对象（存在数值键名和length属性），部署Iterator接口，有一个简便方法，就是Symbol.iterator方法直接引用数组的Iterator接口。
```JavaScript
NodeList.prototype[Symbol.iterator] = Array.prototype[Symbol.iterator];
```
+ 调用Iterator接口的场合
    - for...of
    - 解构赋值
    - 扩展运算符
    - yield*
    - 其他场合。由于数组的遍历会调用遍历器接口，所以任何接受数组作为参数的场合，其实都调用了遍历器接口。下面是一些例子。
        * for...of
        * Array.from()
        * Map(), Set(), WeakMap(), WeakSet()（比如new Map([['a',1],['b',2]])）
        * Promise.all()
        * Promise.race()
+ 遍历器对象的return()，throw()

    遍历器对象除了具有next方法，还可以具有return方法和throw方法。如果你自己写遍历器对象生成函数，那么next方法是必须部署的，return方法和throw方法是否部署是可选的。

    return方法的使用场合是，如果for...of循环提前退出（通常是因为出错，或者有break语句或continue语句），就会调用return方法。如果一个对象在完成遍历前，需要清理或释放资源，就可以部署return方法。

    throw方法主要是配合Generator函数使用，一般的遍历器对象用不到这个方法。
+ for...of循环

    一个数据结构只要部署了Symbol.iterator属性，就被视为具有iterator接口，就可以用for...of循环遍历它的成员。也就是说，for...of循环内部调用的是数据结构的Symbol.iterator方法。

    for...of循环可以使用的范围包括数组、Set和Map结构、某些类似数组的对象（比如arguments对象、DOM NodeList对象）、后文的Generator对象，以及字符串。

    for...of循环调用遍历器接口，数组的遍历器接口只返回具有数字索引的属性。这一点跟for...in循环也不一样。
+ 计算生成的数据结构

    有些数据结构是在现有数据结构的基础上，计算生成的。比如，ES6的数组、Set、Map都部署了以下三个方法，调用后都返回遍历器对象。
    - entries() 返回一个遍历器对象，用来遍历[键名, 键值]组成的数组。对于数组，键名就是索引值；对于Set，键名与键值相同。Map结构的iterator接口，默认就是调用entries方法。
    - keys() 返回一个遍历器对象，用来遍历所有的键名。
    - values() 返回一个遍历器对象，用来遍历所有的键值。

# 15. Generator 函数
+ 执行Generator函数会返回一个遍历器对象，也就是说，Generator函数除了状态机，还是一个遍历器对象生成函数。返回的遍历器对象，可以依次遍历Generator函数内部的每一个状态。形式上，Generator函数是一个普通函数，但是有两个特征。一是，function关键字与函数名之间有一个星号；二是，函数体内部使用yield语句，定义不同的内部状态（yield语句在英语里的意思就是“产出”）。然后，Generator函数的调用方法与普通函数一样，也是在函数名后面加上一对圆括号。不同的是，调用Generator函数后，该函数并不执行，返回的也不是函数运行结果，而是一个指向内部状态的指针对象，也就是上一章介绍的遍历器对象（Iterator Object）。下一步，必须调用遍历器对象的next方法，使得指针移向下一个状态。也就是说，每次调用next方法，内部指针就从函数头部或上一次停下来的地方开始执行，直到遇到下一个yield语句（或return语句）为止。换言之，Generator函数是分段执行的，yield语句是暂停执行的标记，而next方法可以恢复执行。
+ yield语句如果用在一个表达式之中，必须放在圆括号里面。yield语句用作函数参数或赋值表达式的右边，可以不加括号。
```JavaScript
console.log('Hello' + (yield 123)); // OK
foo(yield 'a', yield 'b'); // OK
let input = yield; // OK
```
+ 任意一个对象的Symbol.iterator方法，等于该对象的遍历器生成函数，调用该函数会返回该对象的一个遍历器对象。由于Generator函数就是遍历器生成函数，因此可以把Generator赋值给对象的Symbol.iterator属性，从而使得该对象具有Iterator接口。
+ Generator函数执行后，返回一个遍历器对象。该对象本身也具有Symbol.iterator属性，执行后返回自身。
+ next方法可以带一个参数，该参数就会被当作上一个yield语句的返回值。
+ for...of: for...of循环可以自动遍历调用Generator函数时生成的Iterator对象，且此时不再需要调用next方法。一旦next方法的返回对象的done属性为true，for...of循环就会中止，且不包含该返回对象。
+ Generator函数返回的遍历器对象，都有一个throw方法，可以在函数体外抛出错误，然后在Generator函数体内捕获。
+ 不要混淆遍历器对象的throw方法和全局的throw命令。
+ 如果Generator函数内部没有部署try...catch代码块，那么throw方法抛出的错误，将被外部try...catch代码块捕获。如果Generator函数内部和外部，都没有部署try...catch代码块，那么程序将报错，直接中断执行。
+ throw方法被捕获以后，会附带执行下一条yield语句。也就是说，会附带执行一次next方法。
+ Generator函数体外抛出的错误，可以在函数体内捕获；反过来，Generator函数体内抛出的错误，也可以被函数体外的catch捕获。
+ 一旦Generator执行过程中抛出错误，且没有被内部捕获，就不会再执行下去了。如果此后还调用next方法，将返回一个value属性等于undefined、done属性等于true的对象，即JavaScript引擎认为这个Generator已经运行结束了。
+ Generator函数返回的遍历器对象，还有一个return方法，可以返回给定的值，并且终结遍历Generator函数。
+ 如果Generator函数内部有try...finally代码块，那么return方法会推迟到finally代码块执行完再执行。
+ yield*语句，用来在一个Generator函数里面执行另一个Generator函数。
+ 从语法角度看，如果yield命令后面跟的是一个遍历器对象，需要在yield命令后面加上星号，表明它返回的是一个遍历器对象。这被称为yield*语句。
+ 如果被代理的Generator函数有return语句，那么就可以向代理它的Generator函数返回数据。
+ Generator函数总是返回一个遍历器，ES6规定这个遍历器是Generator函数的实例，也继承了Generator函数的prototype对象上的方法。Generator函数也不能跟new命令一起用，会报错。

# 16. Promise对象
+ Promise对象有以下两个特点。
    - （1）对象的状态不受外界影响。Promise对象代表一个异步操作，有三种状态：Pending（进行中）、Resolved（已完成，又称Fulfilled）和Rejected（已失败）。只有异步操作的结果，可以决定当前是哪一种状态，任何其他操作都无法改变这个状态。这也是Promise这个名字的由来，它的英语意思就是“承诺”，表示其他手段无法改变。
    - （2）一旦状态改变，就不会再变，任何时候都可以得到这个结果。Promise对象的状态改变，只有两种可能：从Pending变为Resolved和从Pending变为Rejected。只要这两种情况发生，状态就凝固了，不会再变了，会一直保持这个结果。就算改变已经发生了，你再对Promise对象添加回调函数，也会立即得到这个结果。这与事件（Event）完全不同，事件的特点是，如果你错过了它，再去监听，是得不到结果的。
+ Promise也有一些缺点。
    - 首先，无法取消Promise，一旦新建它就会立即执行，无法中途取消。
    - 其次，如果不设置回调函数，Promise内部抛出的错误，不会反应到外部。
    - 第三，当处于Pending状态时，无法得知目前进展到哪一个阶段（刚刚开始还是即将完成）。
+ Promise新建后就会立即执行。
+ then方法指定的回调函数，将在当前脚本所有同步任务执行完才会执行。
+ resolve函数的参数除了正常的值以外，还可能是另一个Promise实例，表示异步操作的结果有可能是一个值，也有可能是另一个异步操作。
+ then方法返回的是一个新的Promise实例（注意，不是原来那个Promise实例）。因此可以采用链式写法，即then方法后面再调用另一个then方法。
+ 采用链式的then，可以指定一组按照次序调用的回调函数。这时，前一个回调函数，有可能返回的还是一个Promise对象（即有异步操作），这时后一个回调函数，就会等待该Promise对象的状态发生变化，才会被调用。
+ Promise对象的错误具有“冒泡”性质，会一直向后传递，直到被捕获为止。也就是说，错误总是会被下一个catch语句捕获。一般来说，不要在then方法里面定义Reject状态的回调函数（即then的第二个参数），总是使用catch方法。
+ catch方法返回的还是一个Promise对象，因此后面还可以接着调用then方法。
+ Promise.all()方法用于将多个Promise实例，包装成一个新的Promise实例。Promise.all方法接受一个数组作为参数，数组成员都应该是Promise对象的实例，如果不是，就会先调用下面讲到的Promise.resolve方法，将参数转为Promise实例，再进一步处理。（Promise.all方法的参数可以不是数组，但必须具有Iterator接口，且返回的每个成员都是Promise实例。）
```JavaScript
var p = Promise.all([p1, p2, p3]);
```
p的状态由p1、p2、p3决定，分成两种情况。
    - （1）只有p1、p2、p3的状态都变成fulfilled，p的状态才会变成fulfilled，此时p1、p2、p3的返回值组成一个数组，传递给p的回调函数。
    - （2）只要p1、p2、p3之中有一个被rejected，p的状态就变成rejected，此时第一个被reject的实例的返回值，会传递给p的回调函数。
+ Promise.race()用法类似于Promise.all()。率先改变的Promise实例的返回值，会传递给整体的回调函数。
+ Promise.resolve()：有时需要将现有对象转为Promise对象，Promise.resolve方法就起到这个作用。Promise.resolve方法的参数分成四种情况。
    - （1）参数是一个Promise实例。如果参数是Promise实例，那么Promise.resolve将不做任何修改、原封不动地返回这个实例。
    - （2）参数是一个thenable对象。thenable对象指的是具有then方法的对象。Promise.resolve方法会将这个对象转为Promise对象，然后就立即执行thenable对象的then方法。
    - （3）参数不是具有then方法的对象，或根本就不是对象。如果参数是一个原始值，或者是一个不具有then方法的对象，则Promise.resolve方法返回一个新的Promise对象，状态为Resolved。Promise.resolve方法的参数，会同时传给回调函数。
    - （4）不带有任何参数。Promise.resolve方法允许调用时不带参数，直接返回一个Resolved状态的Promise对象。所以，如果希望得到一个Promise对象，比较方便的方法就是直接调用Promise.resolve方法。需要注意的是，立即resolve的Promise对象，是在本轮“事件循环”（event loop）的结束时，而不是在下一轮“事件循环”的开始时。
+ Promise.reject(reason)方法也会返回一个新的Promise实例，该实例的状态为rejected。它的参数用法与Promise.resolve方法完全一致。

# 17. 异步操作和Async函数
+ Thunk函数与co模块省略。
+ Async函数内置执行器；返回值是Promise；await命令后面是一个Promise对象，如果不是，会被转成一个立即resolve的Promise对象。

# 18. Class
+ 类的所有方法都定义在类的prototype属性上面。
+ 类的内部所有定义的方法，都是不可枚举的（non-enumerable），这一点与ES5的行为不一致。
+ 类的构造函数，不使用new是没法调用的，会报错。这是它跟普通构造函数的一个主要区别，后者不用new也可以执行。
+ 与ES5一样，实例的属性除非显式定义在其本身（即定义在this对象上），否则都是定义在原型上（即定义在class上）。
+ 与ES5一样，类的所有实例共享一个原型对象。这意味着，使用实例的__proto__属性改写原型，必须相当谨慎，不推荐使用，因为这会改变Class的原始定义，影响到所有实例。
+ Class不存在变量提升（hoist），这一点与ES5完全不同。这种规定的原因与下文要提到的继承有关，必须保证子类在父类之后定义。
+ 私有方法：
    - 以下划线(_)开头标志方法名，
    - 将私有方法移出模块，因为模块内部的所有方法都是对外可见的。
    ```JavaScript
    class Widget {
        foo (baz) {
            bar.call(this, baz);
        }

        // ...
    }
    function bar(baz) {
        return this.snaf = baz;
    }
    ```
    - 还有一种方法是利用Symbol值的唯一性，将私有方法的名字命名为一个Symbol值。
+ 类和模块的内部，默认就是严格模式，所以不需要使用use strict指定运行模式。
+ 子类必须在constructor方法中调用super方法，否则新建实例时会报错。这是因为子类没有自己的this对象，而是继承父类的this对象，然后对其进行加工。如果不调用super方法，子类就得不到this对象。
+ ES5的继承，实质是先创造子类的实例对象this，然后再将父类的方法添加到this上面（Parent.apply(this)）。ES6的继承机制完全不同，实质是先创造父类的实例对象this（所以必须先调用super方法），然后再用子类的构造函数修改this。
+ 在子类的构造函数中，只有调用super之后，才可以使用this关键字。
+ 大多数浏览器的ES5实现之中，每一个对象都有\__proto\__属性，指向对应的构造函数的prototype属性。Class作为构造函数的语法糖，同时有prototype属性和\__proto\__属性，因此同时存在两条继承链。
    - （1）子类的\__proto\__属性，表示构造函数的继承，总是指向父类。
    - （2）子类prototype属性的\__proto\__属性，表示方法的继承，总是指向父类的prototype属性。

    这样的结果是因为，类的继承是按照下面的模式实现的(B继承自A)。
    ```JavaScript
        class A {
        }

        class B {
        }

        // B的实例继承A的实例
        Object.setPrototypeOf(B.prototype, A.prototype);

        // B继承A的静态属性
        Object.setPrototypeOf(B, A);
    ```
+ Extends 的继承目标

    extends关键字后面可以跟多种类型的值。
    ```JavaScript
    class B extends A {
    }
    ```
    上面代码的A，只要是一个有prototype属性的函数，就能被B继承。由于函数都有prototype属性（除了Function.prototype函数），因此A可以是任意函数。下面，讨论三种特殊情况。
    - 第一种特殊情况，子类继承Object类。
        ```JavaScript
        class A extends Object {
        }

        A.__proto__ === Object // true
        A.prototype.__proto__ === Object.prototype // true
        ```
        这种情况下，A其实就是构造函数Object的复制，A的实例就是Object的实例。
    - 第二种特殊情况，不存在任何继承。
        ```JavaScript
        class A {
        }

        A.__proto__ === Function.prototype // true
        A.prototype.__proto__ === Object.prototype // true
        ```
        这种情况下，A作为一个基类（即不存在任何继承），就是一个普通函数，所以直接继承Funciton.prototype。但是，A调用后返回一个空对象（即Object实例），所以A.prototype.\__proto\__指向构造函数（Object）的prototype属性。
    - 第三种特殊情况，子类继承null。
        ```JavaScript
        class A extends null {
        }

        A.__proto__ === Function.prototype // true
        A.prototype.__proto__ === undefined // true
        ```
        这种情况与第二种情况非常像。A也是一个普通函数，所以直接继承Funciton.prototype。但是，A调用后返回的对象不继承任何方法，所以它的\__proto\__指向Function.prototype
+ super这个关键字，有两种用法，含义不同。
    - （1）作为函数调用时（即super(...args)），super代表父类的构造函数。
    - （2）作为对象调用时（即super.prop或super.method()），super代表父类。注意，此时super即可以引用父类实例的属性和方法，也可以引用父类的静态方法。
+ ES6中可以继承原生构造函数（Boolean, Number, String, Object, Function, Date, Array, Error, RegExp），而ES5中不可以。注意，继承Object的子类，有一个[行为差异](http://stackoverflow.com/questions/36203614/super-does-not-pass-arguments-when-instantiating-a-class-extended-from-object)。
+ 类相当于实例的原型，所有在类中定义的方法，都会被实例继承。如果在一个方法前，加上static关键字，就表示该方法不会被实例继承，而是直接通过类来调用，这就称为“静态方法”。
+ 父类的静态方法，可以被子类继承。静态方法也是可以从super对象上调用的。
+ ES6明确规定，Class内部只有静态方法，没有静态属性。ES7中可以支持类的实例属性，和类的静态属性。
+ new.target属性：ES6为new命令引入了一个new.target属性，（在构造函数中）返回new命令作用于的那个构造函数。如果构造函数不是通过new命令调用的，new.target会返回undefined，因此这个属性可以用来确定构造函数是怎么调用的。
