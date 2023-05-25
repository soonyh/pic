# 类型

- [1.1](#1.1) <a name="1.1"></a> **基本类型**: 直接存取基本类型。

  + `string`
  + `number`
  + `boolean`
  + `null`
  + `undefined`
  + `symbol`

  **正例**

  ```javascript
    const foo = 1;
    let bar = foo;

    bar = 9;

    console.log(foo, bar); // => 1, 9
    ```

- [1.2](#1.2) <a name="1.2"></a> **复杂类型**: 通过引用的方式存取复杂类型。

  + `object`
  + `array`
  + `function`

  **正例**

  ```javascript
    const foo = {
      a: 1,
      b: 2,
    };
    const bar = foo;

    bar.a = 9;

    console.log(foo.a, bar.a); // => 9, 9
    ```

# 引用

- [2.1](#2.1) <a name="2.1"></a> 对所有的引用使用 `const` ；不要使用 `var`。eslint：[`no-var`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/es6.js#L108)

  > 为什么？这能确保你无法对引用重新赋值，也不会导致出现 bug 或难以理解。

  **<font color=red>反例</font>**

  ```javascript
    var a = 1;
    var b = 2;
    ```

  **正例**

  ```javascript
    const a = 1;
    const b = 2;
    ```

- [2.2](#2.2) <a name="2.2"></a> 如果你一定需要可变动的引用，使用 `let` 代替 `var`。`const`声明的变量是不允许修改的。eslint：[`no-const-assign`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/es6.js/#L56)

  > 为什么？因为  `let` 是块级作用域，而 `var` 是函数作用域。

  **<font color=red>反例</font>**

  ```javascript
    var count = 1;
    if (true) {
      count += 1;
    }
    ```

  **正例**

  ```javascript
    let count = 1;
    if (true) {
      count += 1;
    }
    ```

  *[说明] use the let.*

- [2.3](#2.3) <a name="2.3"></a> `let`和`const`不允许一次声明多个变量/常量，用逗号隔开。

  **<font color=red>反例</font>**

  ```javascript
    const bar = 1, baz = 'test';
    let a, b;
    ```

  **正例**

  ```javascript
    const bar = 1;
    const baz = 'test';
    let a;
    let b;
    ```

- [2.4](#2.4) <a name="2.4"></a> 注意 `let` 和 `const` 都是块级作用域。

  **正例**

  ```javascript
    {
      let a = 1;
      const b = 1;
    }
    console.log(a); // ReferenceError
    console.log(b); // ReferenceError
    ```

  *[说明] const 和 let 只存在于它们被定义的区块内。*

# 对象

- [3.1](#3.1) <a name="3.1"></a> 使用字面语法创建对象。eslint: [`no-new-object`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/style.js#L385)

  **<font color=red>反例</font>**

  ```javascript
    const item = new Object();
    ```

  **正例**

  ```javascript
    const item = {};
    ```

- [3.2](#3.2) <a name="3.2"></a> 如果你的代码在浏览器环境下执行，别使用 [保留字](http://es5.github.io/#x7.6.1) 作为键值。这样的话在 IE8 不会运行。 [更多信息](https://github.com/airbnb/javascript/issues/61)。 但在 ES6 模块和服务器端中使用没有问题。

  **<font color=red>反例</font>**

  ```javascript
    const superman = {
      default: { clark: 'kent' },
      private: true,
    };
    ```

  **正例**

  ```javascript
    const superman = {
      defaults: { clark: 'kent' },
      hidden: true,
    };
    ```

- [3.3](#3.3) <a name="3.3"></a> 使用同义词替换需要使用的保留字。

  **<font color=red>反例</font>**

  ```javascript
    const superman = {
      class: 'alien',
    };

    const superman = {
      klass: 'alien',
    };
    ```

  **正例**

  ```javascript
    const superman = {
      type: 'alien',
    };
    ```

<a name="es6-computed-properties"></a>

- [3.4](#3.4) <a name="3.4"></a> 创建有动态属性名的对象时，使用可被计算的属性名称。

  > 为什么？因为这样可以让你在一个地方定义所有的对象属性。

  **<font color=red>反例</font>**

  ```javascript
    function getKey(k) {
      return `a key named ${k}`;
    }

    const obj = {
      id: 5,
      name: 'San Francisco',
    };
    obj[getKey('enabled')] = true;
    ```

  **正例**

  ```javascript

    function getKey(k) {
      return `a key named ${k}`;
    }

    const obj = {
      id: 5,
      name: 'San Francisco',
      [getKey('enabled')]: true,
    };

    ```

- [3.5](#3.5) <a name="3.5"></a> 使用对象属性值和方法的简写。eslint：[object-shorthand](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/es6.js#L112)

  > 为什么？因为这样更短更有描述性。

  **<font color=red>反例</font>**

  ```javascript
    const lukeSkywalker = 'Luke Skywalker';

    const obj = {
      lukeSkywalker: lukeSkywalker,
      addValue: function (value) {
        return atom.value + value;
      },
    };
    ```

  **正例**

  ```javascript
    const lukeSkywalker = 'Luke Skywalker';

    const obj = {
      lukeSkywalker,
      addValue(value) {
        return atom.value + value;
      },
    };
    ```

- [3.6](#3.6) <a name="3.6"></a> 如果对象的键是字符串，请使用长格式语法。

  **<font color=red>反例</font>**

  ```javascript
      const foo = {
        'bar-baz'() {},
      };
    ```

  **正例**

  ```javascript
      const foo = {
        'bar-baz': function () {},
      };
    ```

- [3.7](#3.7) <a name="3.7"></a> 在对象属性声明前把简写的属性分组。

  > 为什么？因为这样能清楚地看出哪些属性使用了简写。

  **<font color=red>反例</font>**

  ```javascript
    const anakinSkywalker = 'Anakin Skywalker';
    const lukeSkywalker = 'Luke Skywalker';

    const obj = {
      episodeOne: 1,
      twoJedisWalkIntoACantina: 2,
      lukeSkywalker,
      episodeThree: 3,
      mayTheFourth: 4,
      anakinSkywalker,
    };
    ```

  **正例**

  ```javascript
    const anakinSkywalker = 'Anakin Skywalker';
    const lukeSkywalker = 'Luke Skywalker';

    const obj = {
      lukeSkywalker,
      anakinSkywalker,
      episodeOne: 1,
      twoJedisWalkIntoACantina: 2,
      episodeThree: 3,
      mayTheFourth: 4,
    };
    ```

- [3.8](#3.8) <a name="3.8"></a> 不允许在使用对象字面量申明对象时使用相同的键名。 eslint：[`no-dupe-keys`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/errors.js#L53)

  **<font color=red>反例</font>**

  ```javascript
    const foo = {
      bar: 'baz',
      bar: 'qux',
    };
    ```

  **正例**

  ```javascript
    const foo = {
      bar: 'baz',
      quxx: 'qux',
    };
    ```

- [3.9](#3.9) <a name="3.9"></a> 禁止将全局对象（Math和JSON)作为函数调用。eslint：[`no-obj-calls`](http://gitlab.iwhalecloud.com/ngweb/eslint-config-ztesoft/blob/master/rules/errors.js#L70)

  **<font color=red>反例</font>**

  ```javascript
    const math = Math();
    const json = JSON();
    const reflect = Reflect();
    ```

  **正例**

  ```javascript
    function area(r) {
        return Math.PI * r * r;
    }
    const object = JSON.parse("{}");
    const value = Reflect.get({ x: 1, y: 2 }, "x");
    ```

- [3.10](#3.10) <a name="3.10"></a> 禁止在对象中使用不必要的计算属性。eslint：[`no-useless-computed-key`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/es6.js#L89)

  **<font color=red>反例</font>**

  ```javascript
    const a = { ['0']: 0 };
    const a = { ['0+1,234']: 0 };
    const a = { [0]: 0 };
    const a = { ['x']: 0 };
    const a = { ['x']() {} };
    ```

  **正例**

  ```javascript
    const c = { a: 0 };
    const c = { 0: 0 };
    const a = { x() {} };
    const c = { a: 0 };
    const c = { '0+1,234': 0 };
    ```

- [3.11](#3.11) <a name="3.11"></a> 只允许引号标注无效标识符的属性。eslint：[`no-useless-computed-key`](http://gitlab.iwhalecloud.com/ngweb/eslint-config-ztesoft/blob/master/rules/styles.js#L425)

  **<font color=red>反例</font>**

  ```javascript
    const bad = {
      'foo': 3,
      'bar': 4,
      'data-blah': 5,
    };
    ```

  **正例**

  ```javascript
    const good = {
      foo: 3,
      bar: 4,
      'data-blah': 5,
    };
    ```

# 数组

- [4.1](#4.1) <a name="4.1"></a> 使用字面值创建数组。禁止使用new创建包装实例，如 new String、new Number，这样会变成初始化一个对象，而不是对应的初始类型。eslint: [`no-new-wrappers`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/best-practices.js#L210)  [`no-array-constructor`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/style.js/#L316)

  **<font color=red>反例</font>**

  ```javascript
    const items = new Array();
    ```

  **正例**

  ```javascript
    const items = [];
    ```

- [4.2](#4.2) <a name="4.2"></a> 向数组添加元素时使用 Arrary#push 替代直接赋值。

  **<font color=red>反例</font>**

  ```javascript
    const someStack = [];

    someStack[someStack.length] = 'abracadabra';
    ```

  **正例**

  ```javascript
    const someStack = [];

    someStack.push('abracadabra');
    ```

<a name="es6-array-spreads"></a>

- [4.3](#4.3) <a name="4.3"></a> 使用数组展开方法`...`来拷贝数组。

  **<font color=red>反例</font>**

  ```javascript
    const len = items.length;
    const itemsCopy = [];
    let i;

    for (let i = 0; i < len; i += 1) {
      itemsCopy[i] = items[i];
    }
    ```

  **正例**

  ```javascript
    const itemsCopy = [...items];
    ```

- [4.4](#4.4) <a name="4.4"></a> 将一个类数组对象转换成一个数组， 使用展开方法`...`代替`Array.from`。

  **正例 good**

  ```javascript
    const foo = document.querySelectorAll('.foo');

    const nodes = Array.from(foo);
    ```

  **正例 best**

  ```javascript
    const foo = document.querySelectorAll('.foo');

    const nodes = [...foo];
    ```

- [4.5](#4.5) <a name="4.5"></a> 在数组回调方法中使用 return 语句。 如果函数体由一个返回无副作用的表达式的单个语句组成，那么可以省略返回值, 具体查看[8.3](#8.3)

  **<font color=red>反例</font>**

  ```javascript
    [[0, 1], [2, 3], [4, 5]].reduce((acc, item, index) => {
      const flatten = acc.concat(item);
      acc[index] = flatten;
    });

    inbox.filter( msg => {
      const { subject, author } = msg;
      if (subject === 'Mockingbird') {
        return author === 'Harper Lee';
      } else {
        return false;
      }
    });
    ```

  *[说明] 没有返回值，意味着在第一次迭代后 `acc` 没有被定义。*

  **正例**

  ```javascript
    inbox.filter( msg => {
      const { subject, author } = msg;
      if (subject === 'Mockingbird') {
        return author === 'Harper Lee';
      }

      return false;
    });

    [1, 2, 3].map(x => x + 1);
    ```

# 解构

- [5.1](#5.1) <a name="5.1"></a> 在访问和使用对象的多个属性的时候使用对象的解构。eslint: [`prefer-destructuring`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/es6.js#L134)

  > 为什么？解构可以避免为这些属性创建临时引用。

  **<font color=red>反例</font>**

  ```javascript
    function getFullName(user) {
      const firstName = user.firstName;
      const lastName = user.lastName;

      return `${firstName} ${lastName}`;
    }
    ```

  **正例 good**

  ```javascript
    function getFullName(obj) {
      const { firstName, lastName } = obj;
      return `${firstName} ${lastName}`;
    }
    ```

  **正例 best**

  ```javascript
    function getFullName({ firstName, lastName }) {
      return `${firstName} ${lastName}`;
    }
    ```

- [5.2](#5.2) <a name="5.2"></a> 对数组使用解构赋值。 eslint: [`prefer-destructuring`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/es6.js#L134)

  **<font color=red>反例</font>**

  ```javascript
    const arr = [1, 2, 3, 4];

    const first = arr[0];
    const second = arr[1];
    ```

  **正例**

  ```javascript
    const arr = [1, 2, 3, 4];

    const [first, second] = arr; // first = 1  second = 2
    const [, first, second] = arr;
    ```

- [5.3](#5.3) <a name="5.3"></a> 对于多个返回值使用对象解构，而不是数组解构。

  > 为什么？你可以随时添加新的属性或者改变属性的顺序，而不用修改调用方。

  **<font color=red>反例</font>**

  ```javascript
    function processInput(input) {
      // then a miracle occurs
      return [left, right, top, bottom];
    }

    const [left, __, top] = processInput(input);
    ```

  *[说明] 调用时需要考虑回调数据的顺序。*

  **正例**

  ```javascript
    function processInput(input) {
      // then a miracle occurs
      return { left, right, top, bottom };
    }

    const { left, right } = processInput(input);
    ```

  *[说明] 调用时只选择需要的数据。*

# 字符串

- [6.1](#6.1) <a name="6.1"></a> 静态字符串一律使用单引号 `''` 。（如果不是引号嵌套，不要使用双引号）eslint: [`quotes`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/style.js#L529)

  **<font color=red>反例</font>**

  ```javascript
    const name = "Capt. Janeway";

    const name = `Capt. Janeway`;
    ```

  *[说明] 模板文字应该包含插值或换行。*

  **正例**

  ```javascript
    const name = 'Capt. Janeway';
    ```

- [6.2](#6.2) <a name="6.2"></a> 使行超过100个字符的字符串不应使用字符串连接跨多行写入。

  > 注：过度使用字串连接符号可能会对性能造成影响。[jsPerf](http://jsperf.com/ya-string-concat) 和 [讨论](https://github.com/airbnb/javascript/issues/40).

  **<font color=red>反例</font>**

  ```javascript
    const errorMessage = 'This is a super long error that was thrown because \
    of Batman. When you stop to think about how Batman had anything to do \
    with this, you would get nowhere \
    fast.';
    ```

  **正例**

  ```javascript
    const errorMessage = 'This is a super long error that was thrown because ' +
      'of Batman. When you stop to think about how Batman had anything to do ' +
      'with this, you would get nowhere fast.';
    const errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';
    ```

<a name="es6-template-literals"></a>

- [6.3](#6.3) <a name="6.3"></a> 建议使用模板。eslint: [prefer-template](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/es6.js#L171)

  > 为什么？字符串模板为您提供了一种可读的、简洁的语法，具有正确的换行和字符串插值特性。

  **<font color=red>反例</font>**

  ```javascript
    function sayHi(name) {
      return 'How are you, ' + name + '?';
    }

    function sayHi(name) {
      return ['How are you, ', name, '?'].join();
    }
    ```

  **正例**

  ```javascript
    function sayHi(name) {
      return `How are you, ${name}?`;
    }
    ```

- [6.4](#6.4) <a name="6.4"></a> 模板字符串中的嵌入表达式两端不要存在空格。eslint: [prefer-template](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/es6.js#L201)

  **<font color=red>反例</font>**

  ```javascript
    `hello, ${ name}!`;
    `hello, ${name }!`;
    `hello, ${ name }!`;
    ```

  **正例**

  ```javascript
    `hello, ${name}!`;
    `hello, ${
        name
    }!`;
    ```

- [6.5](#6.5) <a name="6.5"></a> 不要在转义字符串中不必要的字符: [no-useless-escape](http://gitlab.iwhalecloud.com/ngweb/eslint-config-ztesoft/blob/master/rules/best-practices.js#L277)

  > 为什么？反斜杠损害了可读性，因此只有在必要的时候才会出现。

  **<font color=red>反例</font>**

  ```javascript
    const foo = '\'this\' \i\s \"quoted\"';
    ```

  **正例**

  ```javascript
    const foo = '\'this\' is "quoted"';
    const foo = `my name is '${name}'`;
    ```

# 函数

- [7.1](#7.1) <a name="7.1"></a> 使用函数声明代替函数表达式。

  > 为什么？因为函数声明是可命名的，所以他们在调用栈中更容易被识别。此外，函数声明会把整个函数提升（hoisted），而函数表达式只会把函数的引用变量名提升。这条规则使得[箭头函数](#arrow-functions)可以取代函数表达式。

  **<font color=red>反例</font>**

  ```javascript
    const foo = function () {
    };
    ```

  **正例 good**

  ```javascript
    const short = function test() {
      // ...
    };
    const foo = () => {};
    ```

  **正例 best**

  ```javascript
    function foo() {
    }
    ```

- [7.2](#7.2) <a name="7.2"></a> 函数表达式:

  **正例**

  ```javascript
    (() => {
      console.log('Welcome to the Internet. Please follow me.');
    })();
    ```

  *[说明] 立即调用的函数表达式 (IIFE)。*

- [7.3](#7.3) <a name="7.3"></a> 永远不要在一个非函数代码块（`if`、`while` 等）中声明一个函数，把那个函数赋给一个变量。浏览器允许你这么做，但它们的解析表现不一致。eslint: [`no-inner-declarations`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/errors.js#L97)

- [7.4](#7.4) <a name="7.4"></a> **注意:** ECMA-262 把 `block` 定义为一组语句。函数声明不是语句。[阅读 ECMA-262 关于这个问题的说明](http://www.ecma-international.org/publications/files/ECMA-ST/Ecma-262.pdf#page=97)。

  **<font color=red>反例</font>**

  ```javascript
    if (currentUser) {
      function test() {
        console.log('Nope.');
      }
    }
    ```

  **正例**

  ```javascript
    let test;
    if (currentUser) {
      test = () => {
        console.log('Yup.');
      };
    }
    ```

- [7.5](#7.5) <a name="7.5"></a> 永远不要把参数命名为 `arguments`。这将取代原来函数作用域内的 `arguments` 对象。eslint: [`no-shadow-restricted-names`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/variables.js#L30)

  > 为什么？`arguments`对象是所有(非箭头)函数中都可用的局部变量，不可当做参数。

  **<font color=red>反例</font>**

  ```javascript
    function nope(name, options, arguments) {
      // ...stuff...
    }
    ```

  **正例**

  ```javascript
    function yup(name, options, args) {
      // ...stuff...
    }
    ```

<a name="es6-rest"></a>

- [7.6](#7.6) <a name="7.6"></a> 不要使用 `arguments`。可以选择 rest 语法 `...` 替代。eslint: [`prefer-rest-params`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/es6.js#L161)

  > 为什么？使用 `...` 能明确你要传入的参数。另外 rest 参数是一个真正的数组，而 `arguments` 是一个类数组。

  **<font color=red>反例</font>**

  ```javascript
    function concatenateAll() {
      const args = Array.prototype.slice.call(arguments);
      return args.join('');
    }
    ```

  **正例**

  ```javascript
    function concatenateAll(...args) {
      return args.join('');
    }
    ```

<a name="es6-default-parameters"></a>

- [7.7](#7.7) <a name="7.7"></a> 使用默认的参数语法，而不是改变函数参数。eslint: [`no-param-reassign`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/best-practices.js#L223)

  **<font color=red>反例</font>**

  ```javascript
    function handleThings(opts) {
      // 不！我们不应该改变函数参数。
      // 更加糟糕: 如果参数 opts 是 false 的话，它就会被设定为一个对象。
      // 但这样的写法会造成一些 Bugs。
      //（译注：例如当 opts 被赋值为空字符串，opts 仍然会被下一行代码设定为一个空对象。）
      opts = opts || {};
      // ...
    }

    function handleThings(opts) {
      if (opts === void 0) {
        opts = {};
      }
      // ...
    }
    ```

  **正例**

  ```javascript
    function handleThings(opts = {}) {
      // ...
    }
    ```

- [7.8](#7.8) <a name="7.8"></a> 直接给函数参数赋值时需要避免副作用。

  > 为什么？因为这样的写法很容易混淆。

  **<font color=red>反例</font>**

  ```javascript
    var b = 1;

    function count(a = b++) {
      console.log(a);
    }
    count();  // 1
    count();  // 2
    count(3); // 3
    count();  // 3
    ```

- [7.9](#7.9) <a name="7.9"></a> 在函数中有分支时，保证所有的return 语句必须指定返回值。 eslint: [`consistent-return`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/best-practices.js#L27)  [`no-useless-return`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/best-practices.js#L282)

  **<font color=red>反例</font>**

  ```javascript
    function doSomething(condition) {
      if (condition) {
        return true;
      }
      return;
    }

    function doSomething(condition) {
      if (condition) {
        return true;
      }
    }
    ```

  **正例**

  ```javascript
    function doSomething(condition) {
      if (condition) {
        return true;
      }
      return false;
    }

    function Foo() {
      if (!(this instanceof Foo)) {
        return new Foo();
      }

      this.a = 0;
    }
    ```

- [7.10](#7.10) <a name="7.10"></a> 数组方法的回调函数中要有 return 语句。以下方法的回调函数必须最终有`return`语句。 eslint: [`array-callback-return`](http://gitlab.ztesoft.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/best-practices.js#L7)

  - `Array.from`
  - `Array.prototype.every`
  - `Array.prototype.filter`
  - `Array.prototype.find`
  - `Array.prototype.findIndex`
  - `Array.prototype.map`
  - `Array.prototype.reduce`
  - `Array.prototype.reduceRight`
  - `Array.prototype.some`
  - `Array.prototype.sort`

  **<font color=red>反例</font>**

  ```javascript
    const indexMap = myArray.reduce(function(memo, item, index) {
      memo[item] = index;
    }, {});

    const foo = Array.from(nodes, function(node) {
      if (node.tagName === "DIV") {
        return true;
      }
    });

    const bar = foo.filter(function(x) {
      if (x) {
        return true;
      }
      return;
    });
    ```

  **正例**

  ```javascript
    const indexMap = myArray.reduce((memo, item, index) => {
      memo[item] = index;
      return memo;
    }, {});

    const foo = Array.from(nodes, node => {
      if (node.tagName === 'DIV') {
        return true;
      }
      return false;
    });

    const bar = foo.map(node => node.getAttribute('id'));
    ```

- [7.11](#7.11) <a name="7.11"></a> 调用无参构造函数时必须带括号。eslint：[`new-parens`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/style.js/#L295)

  **<font color=red>反例</font>**

  ```javascript
    const person = new Person;
    const person = new (Person);
    ```

  **正例**

  ```javascript
    const person = new Person();
    const person = new (Person)();
    ```

- [7.12](#7.12) <a name="7.12"></a> 函数签名中的间距。eslint：[`space-before-function-paren`](http://gitlab.iwhalecloud.com/ngweb/eslint-config-ztesoft/blob/master/rules/styles.js/#L471)  [`space-before-blocks`](http://gitlab.iwhalecloud.com/ngweb/eslint-config-ztesoft/blob/master/rules/styles.js/#L466)

  > 为什么？因为一致性很好，在删除或添加名称时不需要添加或删除空格。

  **<font color=red>反例</font>**

  ```javascript
    const f = function(){};
    const g = function (){};
    const h = function() {};
    ```

  **正例**

  ```javascript
    const x = function () {};
    const y = function a() {};
    ```

- [7.13](#7.13) <a name="7.13"></a> 不要变异参数和再分配参数。eslint：[`no-param-reassign`](http://gitlab.iwhalecloud.com/ngweb/eslint-config-ztesoft/blob/master/rules/best-practices.js/#L187)

  > 为什么？将传入的对象作为参数进行操作可能会在原始调用程序中造成不必要的变量副作用。重新分配参数会导致意外的行为。

  **<font color=red>反例</font>**

  ```javascript
    function f1(obj) {
      obj.key = 1;
    }

    function f1(a) {
      a = 1;
      // ...
    }

    function f2(a) {
      if (!a) { a = 1; }
      // ...
    }
    ```

  **正例**

  ```javascript
    function f3(a) {
      const b = a || 1;
      // ...
    }

    function f4(a = 1) {
      // ...
    }
    ```

- [7.14](#7.14) <a name="7.14"></a> `Generator` 函数是 ES6 提供的一种异步编程解决方案.

  > 为什么需要`Generator`？为了解决javascript异步回调层层嵌套的问题，`Generator` 函数提供了异步编程解决方案。他有以下几个特征：

  - `function`关键字后面会带一个`*`号;函数体内部会使用`yield`表达式
  - `Generator`函数是分段执行的，`yield`表达式是暂停执行的标记，而`next`方法可以恢复执行

  **正例**

  ```javascript
    function* helloWorldGenerator() {
      yield 'hello';
      yield 'world';
      return 'ending';
    }
    const hw = helloWorldGenerator();

    hw.next();
    // { value: 'hello', done: false }

    hw.next();
    // { value: 'world', done: false }

    hw.next();
    // { value: 'ending', done: true }

    hw.next();
    // { value: undefined, done: true }
    ```

- [7.15](#7.15) <a name="7.15"></a> `Generator` 函数内一定要有`yield`。eslint：[`require-yield`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/es6.js/#L176)

  **<font color=red>反例</font>**

  ```javascript
    function* foo() {
      return 10;
    }
    ```

  **正例**

  ```javascript
    function* foo() {
      yield 5;
      return 10;
    }
    ```

# 箭头函数

- [8.1](#8.1) <a name="8.1"></a> 当你必须使用函数表达式（或传递一个匿名函数）时，使用箭头函数符号。

  > 为什么？因为箭头函数创造了新的一个 `this` 执行环境（注：参考 [Arrow functions - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions) 和 [ES6 arrow functions, syntax and lexical scoping](http://toddmotto.com/es6-arrow-functions-syntaxes-and-lexical-scoping/)），通常情况下都能满足你的需求，而且这样的写法更为简洁。

  **<font color=red>反例</font>**

  ```javascript
    [1, 2, 3].map(function (x) {
      const y = x + 1;
      return x * y;
    });
    ```

  **正例 good**

  ```javascript
    [1, 2, 3].map(x => {
      const y = x + 1;
      return x * y;
    });
    ```

  **正例 best**

  ```javascript
    [1, 2, 3].map(x => x * (x + 1));
    ```

- [8.2](#8.2) <a name="8.2"></a> 要求使用箭头函数作为回调。eslint：[`prefer-arrow-callback`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/es6.js/#L120)

  > 为什么？箭头函数自动绑定到其周围作用域/上下文，可以替代显式绑定函数表达式

  **正例**

  ```javascript
    [1, 2, 3].reduce((total, n) => {
      return total + n;
    }, 0);
    ```

- [8.3](#8.3) <a name="8.3"></a> 如果一个函数适合用一行写出并且只有一个参数，那就把花括号、圆括号和 `return` 都省略掉。如果不是，那就不要省略。eslint：[`arrow-parens`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/es6.js/#L23)。eslint：[`arrow-body-style`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/es6.js/#L17)

  > 为什么？语法糖。多个函数被链接在一起时，提高可读性。

  > 什么时候不？当你打算回传一个对象的时候。

  **正例**

  ```javascript
    [1, 2, 3].map(x => x * x);

    [1, 2, 3].reduce((total, n) => total + n, 0);

    [1, 2, 3].map(x => (
      {
        x: x + 1,
      }
    ));
    ```

# 构造函数

- [9.1](#9.1) <a name="9.1"></a> 总是使用 `class`。避免直接操作 `prototype` 。

  > 为什么? 因为 `class` 语法更为简洁更易读。ES6的类class只是一个语法糖，完全可以看作构造函数的另一种写法。新的class写法只是让对象原型的写法更加清晰、更像面向对象编程的语法而已。

  **<font color=red>反例</font>**

  ```javascript
    function Queue(contents = []) {
      this._queue = [...contents];
    }
    Queue.prototype.pop = function() {
      const value = this._queue[0];
      this._queue.splice(0, 1);
      return value;
    }
    ```

  **正例**

  ```javascript
    class Queue {
      constructor(contents = []) {
        this._queue = [...contents];
      }

      pop() {
        const value = this._queue[0];
        this._queue.splice(0, 1);
        return value;
      }
    }
    ```

- [9.2](#9.2) <a name="9.2"></a> 使用 `extends` 继承。

  > 为什么？因为 `extends` 是一个内建的原型继承方法并且可以在不破坏 instanceof 的情况下继承原型功能。这比ES5的通过修改原型链实现继承，要清晰和方便很多

  **<font color=red>反例</font>**

  ```javascript
    const inherits = require('inherits');
    function PeekableQueue(contents) {
      Queue.apply(this, contents);
    }
    inherits(PeekableQueue, Queue);
    PeekableQueue.prototype.peek = function() {
      return this._queue[0];
    }
    ```

  **正例**

  ```javascript
    class PeekableQueue extends Queue {
      peek() {
        return this._queue[0];
      }
    }
    ```

- [9.3](#9.3) <a name="9.3"></a> 方法可以返回 `this` 来供其内部方法调用。

  **<font color=red>反例</font>**

  ```javascript
    Jedi.prototype.jump = function() {
      this.jumping = true;
      return true;
    };

    Jedi.prototype.setHeight = function(height) {
      this.height = height;
    };

    const luke = new Jedi();
    luke.jump(); // => true
    luke.setHeight(20); // => undefined
    ```

  **正例**

  ```javascript
    class Jedi {
      jump() {
        this.jumping = true;
        return this;
      }

      setHeight(height) {
        this.height = height;
        return this;
      }
    }

    const luke = new Jedi();

    luke.jump()
      .setHeight(20);
    ```

- [9.4](#9.4) <a name="9.4"></a> 可以写一个自定义的 `toString()` 方法，但要确保它能正常运行并且不会引起副作用。

  **正例**

  ```javascript
    class Jedi {
      constructor(options = {}) {
        this.name = options.name || 'no name';
      }

      getName() {
        return this.name;
      }

      toString() {
        return `Jedi - ${this.getName()}`;
      }
    }
    ```

- [9.5](#9.5) <a name="9.5"></a> 构造函数中禁止在`super()`调用之前使用`this`或`super`。eslint：[`no-this-before-super`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/es6.js/#L84)

  **<font color=red>反例</font>**

  ```javascript
    class A extends B {
      constructor() {
        this.foo();
        super();
      }
    }

    class A extends B {
      constructor() {
        super.foo();
        super();
      }
    }
    ```

  **正例**

  ```javascript
    class A {
      constructor() {
        this.a = 0;
      }
    }

    class A extends B {
      constructor() {
        super();
        this.a = 0;
      }
    }
    ```

- [9.6](#9.6) <a name="9.6"></a> 如果没有指定类，则类具有默认的构造器。 一个空的构造器或是一个代表父类的函数是没有必要的。eslint：[`no-useless-constructor`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/es6.js/#L94)

  > 为什么？es6为没有指定构造函数的类提供了默认构造函数。因此，没有必要提供一个空的构造函数或只是简单的调用父类这样的构造函数

  **<font color=red>反例</font>**

  ```javascript
    class Jedi {
      constructor() {}

      getName() {
        return this.name;
      }
    }

    class Rey extends Jedi {
      constructor(...args) {
        super(...args);
      }
    }
    ```

  **正例**

  ```javascript
    class Rey extends Jedi {
      constructor(...args) {
        super(...args);
        this.name = 'Rey';
      }
    }
    ```

- [9.7](#9.7) <a name="9.7"></a> 构造函数类成员中不允许出现重复名称。eslint：[`no-dupe-class-members`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/es6.js/#L60)

  **<font color=red>反例</font>**

  ```javascript
    class Foo {
      bar() {}
      bar() {}
    }

    class Foo {
      bar() {}
      get bar() {}
    }

    class Foo {
      static bar() {}
      static bar() {}
    }
    ```

  **正例**

  ```javascript
    class Foo {
      bar() {}
      qux() {}
    }

    class Foo {
      get bar() {}
      set bar(value) {}
    }

    class Foo {
      static bar() {}
      bar() {}
    }
    ```

# 模块

- [10.1](#10.1) <a name="10.1"></a> 总是使用模组 (`import`/`export`) 而不是其他非标准模块系统。

  > 为什么？模块就是未来，让我们开始迈向未来吧。

  **<font color=red>反例</font>**

  ```javascript
    const WhaleCloudStyleGuide = require('./WhaleCloudStyleGuide');
    module.exports = WhaleCloudStyleGuide.es6;
    ```

  **正例 good**

  ```javascript
    import WhaleCloudStyleGuide from './WhaleCloudStyleGuide';
    export default WhaleCloudStyleGuide.es6;
    ```

  **正例 best**

  ```javascript
    import { es6 } from './WhaleCloudStyleGuide';
    export default es6;
    ```

- [10.2](#10.2) <a name="10.2"></a> 不要使用通配符导入。

  > 为什么？这样能确保你只有一个默认 export。

  **<font color=red>反例</font>**

  ```javascript
    import * as WhaleCloudStyleGuide from './WhaleCloudStyleGuide';
    ```

  *[说明] 不报错。*

  **正例**

  ```javascript
    import WhaleCloudStyleGuide from './WhaleCloudStyleGuide';
    ```

- [10.3](#10.3) <a name="10.3"></a>不要从 import 中直接 export。

  > 为什么？虽然一行代码简洁明了，但让 import 和 export 各司其职让事情能保持一致。

  **<font color=red>反例</font>**

  ```javascript
    export { es6 as default } from './WhaleCloudStyleGuide';
    ```

  **正例**

  ```javascript
    import { es6 } from './WhaleCloudStyleGuide';
    export default es6;
    ```

- [10.4](#10.4) <a name="10.4"></a>确保`import`和`export`命名匹配。eslint：[`import/named`](http://gitlab.ztesoft.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/imports.js/#L35)

  **<font color=red>反例</font>**

  ```javascript
    // ./foo.js
    export const foo = "I'm so foo";

    // ./baz.js
    import { notFoo } from './foo'
    ```

  **正例**

  ```javascript
    // ./foo.js
    export const foo = "I'm so foo";

    // ./bar.js
    import { foo } from './foo'
    ```

- [10.5](#10.5) <a name="10.5"></a>模块导入顺序优先级注意。并且`import`优先级一定高于`require`。模块导入按照以下顺序：eslint：[`import/order`](http://gitlab.ztesoft.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/imports.js/#L144)

  - node模块(fs等)
  - 外部模块(lodash等)
  - 全局模块
  - 父目录模块
  - 当前目录模块

  **<font color=red>反例</font>**

  ```javascript
    import _ from 'lodash';
    import path from 'path'; // `path` import should occur before import of `lodash`

    // -----

    const _ = require('lodash');
    const path = require('path'); // `path` import should occur before import of `lodash`

    // -----

    const path = require('path');
    import foo from './foo'; // `import` statements must be before `require` statement
    ```

  **正例**

  ```javascript
    import { es6 } from './WhaleCloudStyleGuide';
    export default es6;

    import path from 'path';
    import _ from 'lodash';

    // -----

    const path = require('path');
    const _ = require('lodash');

    // -----

    // Allowed as ̀`babel-register` is not assigned.
    require('babel-register');
    const path = require('path');

    // -----

    // Allowed as `import` must be before `require`
    import foo from './foo';
    const path = require('path');
    ```

- [10.6](#10.6) <a name="10.6"></a>如果一个模块仅有一个导出，请加上`export default`。同样的，一个模块内只能出现一个默认导出`export default`。eslint：[`import/prefer-default-export`](http://gitlab.ztesoft.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/imports.js/#L155) [`import/export`](http://gitlab.ztesoft.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/imports.js/#L55)

  **<font color=red>反例</font>**

  ```javascript
    export const foo = 'foo';
    ```

  **正例**

  ```javascript
    // example1
    export const foo = 'foo';
    const bar = 'bar';
    export default 'bar';

    // example2
    export const foo = 'foo';
    export const bar = 'bar';

    // example3
    const foo = 'foo';
    const bar = 'bar';
    export default { foo, bar }

    // example4
    const foo = 'foo';
    export { foo as default }
    ```

- [10.7](#10.7) <a name="10.7"></a>禁止使用`default`作为导入变量名，因为会与`export default`冲突发生错误。eslint：[`no-named-default`](http://gitlab.ztesoft.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/imports.js/#L206)

  **<font color=red>反例</font>**

  ```javascript
    // foo.js
    export default 'foo';
    export const bar = 'baz';

    import { default as foo } from './foo.js';
    import { default as foo, bar } from './foo.js';
    ```

  **正例**

  ```javascript
    // foo.js
    export default 'foo';
    export const bar = 'baz';

    import foo from './foo.js';
    import foo, { bar } from './foo.js';
    ```

- [10.8](#10.8) <a name="10.8"></a>禁止使用绝对路径导入。eslint：[`import/no-absolute-path`](http://gitlab.ztesoft.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/imports.js/#L170)

  **<font color=red>反例</font>**

  ```javascript
    import f from '/foo';
    import f from '/some/path';

    const f = require('/foo');
    const f = require('/some/path');
    ```

  **正例**

  ```javascript
    import _ from 'lodash';
    import foo from 'foo';
    import foo from './foo';

    const _ = require('lodash');
    const foo = require('foo');
    const foo = require('./foo');
    ```

- [10.9](#10.9) <a name="10.9"></a>禁止使用`AMD` `require/define`。eslint：[`import/no-amd`](http://gitlab.ztesoft.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/imports.js/#L100)

  > 为什么？因为ES6已经具备模块化，不需要再使用`AMD`规范了。

  **<font color=red>反例</font>**

  ```javascript
    define(["a", "b"], function (a, b) { /* ... */ });

    require(["b", "c"], function (b, c) { /* ... */ });
    ```

- [10.10](#10.10) <a name="10.10"></a>禁止在 `import` 和 `export` 和解构赋值时将引用重命名为相同的名字。eslint：[`no-useless-rename`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/es6.js/#L99)

  **<font color=red>反例</font>**

  ```javascript
    import { foo as foo } from "bar";

    export { foo as foo };
    export { foo as foo } from "bar";

    let { foo: foo } = bar;
    let { 'foo': foo } = bar;
    function foo({ bar: bar }) {}
    ({ foo: foo }) => {}
    ```

  **正例**

  ```javascript
    import * as foo from "foo";
    import { foo } from "bar";
    import { foo as bar } from "baz";

    export { foo };
    export { foo as bar };
    export { foo as bar } from "foo";

    let { foo } = bar;
    let { foo: bar } = baz;
    let { [foo]: foo } = bar;

    function foo({ bar }) {}
    function foo({ bar: baz }) {}

    ({ foo }) => {}
    ({ foo: bar }) => {}
    ```

# 迭代器和生成器

- [11.1](#11.1) <a name="11.1"></a> 不要使用 iterators。使用高阶函数例如 `map()` 和 `reduce()` 替代 `for-of`。

  > 为什么？这加强了我们不变的规则。处理纯函数的回调值更易读，这比它带来的副作用更重要。
  > 使用`map()`/`every()`/`filter()`/`find()`/`findIndex()`/`reduce()`/`some()`/`...`遍历数组， 和使用`Object.keys()`/`Object.values()`/`Object.entries()`迭代你的对象生成数组。

  **<font color=red>反例</font>**

  ```javascript
    const numbers = [1, 2, 3, 4, 5];

    let sum = 0;
    for (let num of numbers) {
      sum += num;
    }

    sum === 15;
    ```

  **正例**

  ```javascript
    const numbers = [1, 2, 3, 4, 5];

    let sum = 0;
    numbers.forEach((num) => sum += num);
    sum === 15;

    // best (use the functional force)
    const sum = numbers.reduce((total, num) => total + num, 0);
    sum === 15;
    ```

# 属性

- [12.1](#12.1) <a name="12.1"></a> 使用 `.` 来访问对象的属性。eslint：[`dot-notation`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/best-practices.js/#L39)

  **<font color=red>反例</font>**

  ```javascript
    const luke = {
      jedi: true,
      age: 28,
    };

    const isJedi = luke['jedi'];
    ```

  **正例**

  ```javascript
    const luke = {
      jedi: true,
      age: 28,
    };

    const isJedi = luke.jedi;
    ```

- [12.2](#12.2) <a name="12.2"></a> 当通过变量访问属性时使用中括号 `[]`。

  **正例**

  ```javascript
    const luke = {
      jedi: true,
      age: 28,
    };

    function getProp(prop) {
      return luke[prop];
    }

    const isJedi = getProp('jedi');
    ```

- [12.3](#12.3) <a name="12.3"></a> 规定声明对象的属性时只能一行声明所有的属性或者每行声明一个属性。 eslint: [`object-property-newline`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/style.js#L477)

  **<font color=red>反例</font>**

  ```javascript
    const obj1 = { foo: 'foo', bar: 'bar',
      baz: 'baz',
    };
    ```

  **正例**

  ```javascript
    const obj1 = { foo: 'foo', bar: 'bar', baz: 'baz' };
    const obj2 = {
      foo: 'foo',
      bar: 'bar',
      baz: 'baz',
    };
    ```

- [12.4](#12.4) <a name="12.4"></a> 禁止使用`__proto__`属性，`__proto__`属性已从ECMAScript 3.1开始弃用，不应在代码中使用，改用`getPrototypeOf`方法。 eslint: [`no-proto`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/best-practices.js#L243)

  **<font color=red>反例</font>**

  ```javascript
    const a = obj.__proto__;
    const a = obj['__proto__'];
    ```

  **正例**

  ```javascript
    const a = Object.getPrototypeOf(obj);
    ```

# 变量

- [13.1](#13.1) <a name="13.1"></a> 变量的名称采用小驼峰法则，首字母小写，后续单词的首字母大写。变量的属性名不需要遵循该规则。 eslint: [`camelcase`](http://gitlab.iwhalecloud.com/ngweb/eslint-config-ztesoft/blob/master/rules/styles.js#L19)

  **<font color=red>反例</font>**

  ```javascript
    const Is_Editable = false;
    ```

  **正例**

  ```javascript
    const isEditable = false;
    const obj = {
      my_pref: 1,
      'my-pref': 2,
    };
    ```

- [13.2](#13.2) <a name="13.2"></a> 一直使用 `const` 来声明变量，如果不这样做就会产生全局变量。我们需要避免全局命名空间的污染。eslint：[`no-undef`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/variables.js/#L34)

  **<font color=red>反例</font>**

  ```javascript
    superPower = new SuperPower();
    ```

  **正例**

  ```javascript
    const superPower = new SuperPower();
    ```

- [13.3](#13.3) <a name="13.3"></a> 使用 `const` 声明常量或者不会再被分配的变量。eslint：[`prefer-const`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/es6.js/#L127)  `one-var`

  > 为什么？这样更容易添加新的变量声明，而且你不必担心是使用 ; 还是使用 , 或引入标点符号的差别。 你可以通过 debugger 逐步查看每个声明，而不是立即跳过所有声明。

  **<font color=red>反例</font>**

  ```javascript
    const items = getItems(),
        goSportsTeam = true,
        dragonball = 'z';

    // (compare to above, and try to spot the mistake)
    const items = getItems(),
        goSportsTeam = true;
        dragonball = 'z';
    ```

  **正例**

  ```javascript
    const items = getItems();
    const goSportsTeam = true;
    const dragonball = 'z';
    ```

- [13.4](#13.4) <a name="13.4"></a> 将所有的 `const` 和 `let` 分组

  > 为什么？这在后边如果需要根据前边的赋值变量指定一个变量时很有用。

  **<font color=red>反例</font>**

  ```javascript
    let i, len, dragonball,
        items = getItems(),
        goSportsTeam = true;

    let i;
    const items = getItems();
    let dragonball;
    const goSportsTeam = true;
    let len;
    ```

  **正例**

  ```javascript
    const goSportsTeam = true;
    const items = getItems();
    let dragonball;
    let i;
    let length;
    ```

- [13.5](#13.5) <a name="13.5"></a> 在你需要的地方给变量赋值，但请把它们放在一个合理的位置。

  > 为什么？`let` 和 `const` 是块级作用域而不是函数作用域。

  **<font color=red>反例</font>**

  ```javascript
    function(hasName) {
      const name = getName();

      if (!hasName) {
        return false;
      }

      this.setFirstName(name);

      return true;
    }
    ```

  *[说明] unnecessary function call。*

  **正例**

  ```javascript
    function() {
      test();
      console.log('doing stuff..');

      //..other stuff..

      const name = getName();

      if (name === 'test') {
        return false;
      }

      return name;
    }

    function(hasName) {
      if (!hasName) {
        return false;
      }

      const name = getName();
      this.setFirstName(name);

      return true;
    }
    ```

- [13.6](#13.6) <a name="13.6"></a> 禁止重新声明变量。eslint：[`no-redeclare`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/best-practices.js/#L247)

  **<font color=red>反例</font>**

  ```javascript
    let a = 3;
    let a = 10;
    ```

  **正例**

  ```javascript
    let a = 3;
    a = 10;
    ```

- [13.7](#13.7) <a name="13.7"></a> 避免使用不必要的递增和递减 (++, --)。eslint：[`no-plusplus`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/variables.js/#L17)

  > 为什么？在`eslint`文档中，一元递增和递减语句以自动分号插入为主题，并且在应用程序中可能会导致默认值的递增或递减。你可以使用`num += 1`这样的语句来改变您的值，而不是使用`num++`或`num ++`。不允许不必要的增量和减量语句也会使您无法预先递增/预递减值，这也会导致程序中的意外行为

  **<font color=red>反例</font>**

  ```javascript
    const array = [1, 2, 3];
    let num = 1;
    num++;
    --num;

    let sum = 0;
    let truthyCount = 0;
    for (let i = 0; i < array.length; i++) {
      let value = array[i];
      sum += value;
      if (value) {
        truthyCount++;
      }
    }
    ```

  **正例**

  ```javascript
    const array = [1, 2, 3];
    let num = 1;
    num += 1;
    num -= 1;

    const sum = array.reduce((a, b) => a + b, 0);
    const truthyCount = array.filter(Boolean).length;
    ```

- [13.8](#13.8) <a name="13.8"></a> 禁止声明的变量与外层作用域的变量同名。eslint：[`no-shadow`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/variables.js/#L26)

  **<font color=red>反例</font>**

  ```javascript
    const a = 3;
    function b() {
        const a = 10;
    }
    ```

  **正例**

  ```javascript
    const a = 3;
    function b() {
        const c = 10;
    }
    ```

- [13.9](#13.9) <a name="13.9"></a> 禁止使用没有定义的变量。禁止在变量定义之前使用它们。 eslint: [`no-undef`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/variables.js#L34) eslint: [`no-use-before-define`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/variables.js.js#L51)

  **<font color=red>反例</font>**

  ```javascript
    const a = 5;
    b = 10;
    f();
    function f() {}
    ```

  **正例**

  ```javascript
    let a = 5;
    a = 10;
    function f() {}
    f();
    ```

- [13.10](#13.10) <a name="13.10"></a> 不允许初始化变量值为 `undefined`。 eslint: [`no-undef-init`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/variables.js#L38)

  **<font color=red>反例</font>**

  ```javascript
    let bar = undefined;
    ```

  **正例**

  ```javascript
    let bar;
    const baz = undefined;
    ```

  *[说明] const声明的常量必须要首先赋值。*

- [13.11](#13.11) <a name="13.11"></a> 不允许定义了的变量但是在后面的代码中没有被使用到。 eslint: [`no-unused-vars`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/variables.js#L47)

  **<font color=red>反例</font>**

  ```javascript
    function foo(d) {
      const y = 10;
      const z = 0;
      console.log(z);
    }
    ```

  **正例**

  ```javascript
    function foo(d) {
      console.log(d);
    }
    ```

- [13.12](#13.12) <a name="13.12"></a> 禁止使用链式赋值的表达式。 eslint: [`no-multi-assign`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/style.js#L367)

  **<font color=red>反例</font>**

  ```javascript
    const a = b = c = 5;
    const foo = bar = 'baz';
    ```

  **正例**

  ```javascript
    const a = 5;
    const b = 5;
    const c = 5;
    const foo = 'baz';
    const bar = 'baz';
    ```

- [13.13](#13.13) <a name="13.13"></a> 把变量的使用限制在其定义的作用域范围内。 eslint: [`block-scoped-var`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/best-practices.js#L12)

  **<font color=red>反例</font>**

  ```javascript
    function doIf() {
      if (true) {
          var build = true;
      }

      console.log(build);
    }

    function doIfElse() {
        if (true) {
            var build = true;
        } else {
            var build = false;
        }
    }

    function doTryCatch() {
        try {
            var build = 1;
        } catch (e) {
            var f = build;
        }
    }
    ```

  **正例**

  ```javascript
    function doIf() {
    let build;

    if (true) {
        build = true;
    }

    console.log(build);
    }

    function doIfElse() {
        let build;

        if (true) {
            build = true;
        } else {
            build = false;
        }
    }

    function doTryCatch() {
        let build;
        let f;

        try {
            build = 1;
        } catch (e) {
            f = build;
        }
    }
    ```

- [13.14](#13.14) <a name="13.14"></a> 禁止修改类声明的变量。 eslint: [`no-class-assign`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/es6.js#L44)

  **<font color=red>反例</font>**

  ```javascript
    let A = class A {
      b() {
        A = 0;
      }
    }
    ```

  **正例**

  ```javascript
    class A {
      b(A) {
        A = 0; // A is a parameter.
      }
    }
    ```

# 提升

- [14.1](#14.1) <a name="14.1"></a> `var` 声明会被提升至该作用域的顶部，但它们赋值不会提升。`let` 和 `const` 被赋予了一种称为「[暂时性死区（Temporal Dead Zones, TDZ）](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let#Temporal_dead_zone_and_errors_with_let)」的概念。这对于了解为什么 [type of 不再安全](http://es-discourse.com/t/why-typeof-is-no-longer-safe/15)相当重要。

  **<font color=red>反例</font>**

  ```javascript
    // 我们知道这样运行不了
    // （假设 notDefined 不是全局变量）
    function example() {
      console.log(notDefined); // => throws a ReferenceError
    }

    // 由于变量提升的原因，
    // 在引用变量后再声明变量是可以运行的。
    // 注：变量的赋值 `true` 不会被提升。
    function example() {
      console.log(declaredButNotAssigned); // => undefined
      var declaredButNotAssigned = true;
    }

    // 使用 const 和 let
    function example() {
      console.log(declaredButNotAssigned); // => throws a ReferenceError
      console.log(typeof declaredButNotAssigned); // => throws a ReferenceError
      const declaredButNotAssigned = true;
    }
    ```

  **正例**

  ```javascript
    // 编译器会把函数声明提升到作用域的顶层，
    // 这意味着我们的例子可以改写成这样：
    function example() {
      let declaredButNotAssigned;
      console.log(declaredButNotAssigned); // => undefined
      declaredButNotAssigned = true;
    }
    ```

- [14.2](#14.2) <a name="14.2"></a> 匿名函数表达式的变量名会被提升，但函数内容并不会。

  **<font color=red>反例</font>**

  ```javascript
    function example() {
      console.log(anonymous); // => undefined

      anonymous(); // => TypeError anonymous is not a function

      var anonymous = function() {
        console.log('anonymous function expression');
      };
    }
    ```

- [14.3](#14.3) <a name="14.3"></a> 命名的函数表达式的变量名会被提升，但函数名和函数内容并不会。

  **<font color=red>反例</font>**

  ```javascript
    function example() {
      console.log(named); // => undefined

      named(); // => TypeError named is not a function

      superPower(); // => ReferenceError superPower is not defined

      const named = function superPower() {
        console.log('Flying');
      };
    }

    // the same is true when the function name
    // is the same as the variable name.
    function example() {
      console.log(named); // => undefined

      named(); // => TypeError named is not a function

      const named = function named() {
        console.log('named');
      }
    }
    ```

- [14.4](#14.4) <a name="14.4"></a> 函数声明的名称和函数体都会被提升。

  **<font color=red>反例</font>**

  ```javascript
    function example() {
      superPower(); // => Flying

      function superPower() {
        console.log('Flying');
      }
    }
    ```

# 比较运算符和等号

- [15.1](#15.1) <a name="15.1"></a> 优先使用 `===` 和 `!==` 而不是 `==` 和 `!=`.eslint：[`eqeqeq`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/best-practices.js/#L48)

- [15.2](#15.2) <a name="15.2"></a> 条件表达式例如 `if` 语句通过抽象方法 `ToBoolean` 强制计算它们的表达式并且总是遵守下面的规则：

  + **对象** 被计算为 **true**
  + **Undefined** 被计算为 **false**
  + **Null** 被计算为 **false**
  + **布尔值** 被计算为 **布尔的值**
  + **数字** 如果是 **+0、-0、或 NaN** 被计算为 **false**, 否则为 **true**
  + **字符串** 如果是空字符串 `''` 被计算为 **false**，否则为 **true**

  **正例**

  ```javascript
    if ([0]) {
      // true
      // An array is an object, objects evaluate to true
    }
    ```

- [15.3](#15.3) <a name="15.3"></a> 对于布尔值使用简写，但是对于字符串和数字进行显式比较。

  **<font color=red>反例</font>**

  ```javascript
    if (isValid === true) {
      // ...
    }

    if (name) {
      // ...
    }

    if (collection.length) {
      // ...
    }
    ```

  **正例**

  ```javascript
    if (isValid) {
      // ...
    }

    if (name !== '') {
      // ...
    }

    if (collection.length > 0) {
      // ...
    }
    ```

- [15.4](#15.4) <a name="15.4"></a> 对于绝大多数的使用情况下，结果typeof操作是下列字符串常量之一："undefined"，"object"，"boolean"，"number"，"string"，"function"和"symbol"。将typeof运算符的结果与其他字符串文字进行比较通常是代码编写出现错误。 eslint: [`valid-typeof`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/errors.js#L177)

  **<font color=red>反例</font>**

  ```javascript
    typeof foo === undefined;
    typeof bar == Object;
    typeof baz === 'strnig';
    typeof qux === 'some invalid type';
    typeof baz === anotherVariable;
    typeof foo == 5;
    ```

  **正例**

  ```javascript
    typeof foo === 'undefined';
    typeof bar == 'object';
    typeof baz === 'string';
    typeof bar === typeof qux;
    ```

- [15.5](#15.5) <a name="15.5"></a> 禁止出现与本身作比较的语句。 eslint: [`no-self-compare`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/best-practices.js#L313)

  **<font color=red>反例</font>**

  ```javascript
    let x = 10;
    if (x === x) {
        x = 20;
    }
    ```

  **正例**

  ```javascript
    let x = 10;
    const y = 10;
    if (x === y) {
        x = 20;
    }
    ```

- [15.6](#15.6) <a name="15.6"></a> 禁止条件表达式中出现赋值操作符。eslint: [`no-cond-assign`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/errors.js#L29)

  **<font color=red>反例</font>**

  ```javascript
    let x;
    if (x = 0) {
        const b = 1;
    }

    // Practical example that is similar to an error
    function setHeight(someNode) {
        "use strict";
        do {
            someNode.height = "100px";
        } while (someNode = someNode.parentNode);
    }
    ```

  **正例**

  ```javascript
    const x;
    if (x === 0) {
        const b = 1;
    }
    ```

- [15.7](#15.7) <a name="15.7"></a> 禁止对关系运算符的左操作数使用否定运算符。 eslint: [`no-unsafe-negation`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/errors.js#L151)

  **<font color=red>反例</font>**

  ```javascript
    if (!key in object) {
        // operator precedence makes it equivalent to (!key) in object
        // and type conversion makes it equivalent to (key ? "false" : "true") in object
    }
    if (!obj instanceof Ctor) {
        // operator precedence makes it equivalent to (!obj) instanceof Ctor
        // and it equivalent to always false since boolean values are not objects.
    }
    ```

  **正例**

  ```javascript
    if (!(key in object)) {
        // key is not in object
    }
    if (!(obj instanceof Ctor)) {
        // obj is not an instance of Ctor
    }
    if(('' + !key) in object) {
        // make operator precedence and type conversion explicit
        // in a rare situation when that is the intended meaning
    }
    ```

- [15.8](#15.8) <a name="15.8"></a> 建议使用扩展运算符而非`.apply()`。 eslint: [`prefer-spread`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/es6.js#L166)

  **<font color=red>反例</font>**

  ```javascript
    foo.apply(undefined, args);
    foo.apply(null, args);
    obj.foo.apply(obj, args);
    ```

  **正例**

  ```javascript
    foo(...args);
    obj.foo(...args);
    ```

- [15.9](#15.9) <a name="15.9"></a> 三目表达式不应该嵌套，通常是单行表达式。 eslint: [`no-nested-ternary`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/es6.js#L166)

  **<font color=red>反例</font>**

  ```javascript
    const foo = maybe1 > maybe2
      ? "bar"
      : value1 > value2 ? "baz" : null;
    ```

  **正例 good**

  ```javascript
    const maybeNull = value1 > value2 ? 'baz' : null;
    const foo = maybe1 > maybe2
      ? 'bar'
      : maybeNull;
    ```

  *[说明] 分离为两个三目表达式。*

  **正例 best**

  ```javascript
    const maybeNull = value1 > value2 ? 'baz' : null;
    const foo = maybe1 > maybe2 ? 'bar' : maybeNull;
    ```

# 代码块

- [16.1](#16.1) <a name="16.1"></a> 使用大括号包裹所有的多行代码块。eslint：[`curly`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/best-practices.js/#L31)

  **<font color=red>反例</font>**

  ```javascript
    if (test)
      return false;

    function example() { return false; }
    ```

  **正例**

  ```javascript
    if (test) return false;

    if (test) {
      return false;
    }

    function example() {
      return false;
    }
    ```

- [16.2](#16.2) <a name="16.2"></a> 如果通过 `if` 和 `else` 使用多行代码块，把 `else` 放在 `if` 代码块关闭括号的同一行。eslint：[`brace-style`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/style.js/#L24)

  **<font color=red>反例</font>**

  ```javascript
    if (test) {
      thing1();
      thing2();
    }
    else {
      thing3();
    }
    ```

  **正例**

  ```javascript
    if (test) {
      thing1();
      thing2();
    } else {
      thing3();
    }
    ```

# 注释

- [17.1](#17.1) <a name="17.1"></a> 使用 `/** ... */` 作为多行注释。包含描述、指定所有参数和返回值的类型和值。并且多行注释与上一个代码块之间要空一行。

  **<font color=red>反例</font>**

  ```javascript
    // make() returns a new element
    // based on the passed in tag name
    //
    // @param {String} tag
    // @return {Element} element
    function make(tag) {

      // ...stuff...

      return element;
    }
    ```

  **正例**

  ```javascript
    /**
     * make() returns a new element
     * based on the passed in tag name
     *
     * @param {String} tag
     * @return {Element} element
     */
    function make(tag) {

      // ...stuff...

      return element;
    }
    ```

- [17.2](#17.2) <a name="17.2"></a> 使用 `//` 作为单行注释。在评论对象上面另起一行使用单行注释。在注释前插入空行。eslint: [`lines-around-comment`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/style.js#L211)

  **<font color=red>反例</font>**

  ```javascript
    const active = true;  // is current tab

    function getType() {
      console.log('fetching type...');
      // set the default type to 'no type'
      const type = this._type || 'no type';

      return type;
    }
    ```

  *[说明] 注释错误。*

  **正例**

  ```javascript
    // is current tab
    const active = true;

    function getType() {
      console.log('fetching type...');

      // set the default type to 'no type'
      const type = this._type || 'no type';

      return type;
    }
    ```

  *[说明] 注释正确。*

- [17.3](#17.3) <a name="17.3"></a> 给注释增加 `FIXME` 或 `TODO` 的前缀可以帮助其他开发者快速了解这是一个需要复查的问题，或是给需要实现的功能提供一个解决方式。这将有别于常见的注释，因为它们是可操作的。使用 `FIXME -- need to figure this out` 或者 `TODO -- need to implement`。eslint: [`no-warning-comments`](http://gitlab.iwhalecloud.com/ngweb/eslint-config-ztesoft/blob/master/rules/best-practices.js#L292)

- [17.4](#17.4) <a name="17.4"></a> 使用 `// FIXME`: 标注问题。

  **正例**

  ```javascript
    class Calculator {
      constructor() {
        // FIXME: shouldn't use a global here
        total = 0;
      }
    }
    ```

- [17.5](#17.5) <a name="17.5"></a> 使用 `// TODO`: 标注问题的解决方式。

  **正例**

  ```javascript
    class Calculator {
      constructor() {
        // TODO: total should be configurable by an options param
        this.total = 0;
      }
    }
    ```

# 空白

- [18.1](#18.1) <a name="18.1"></a> 使用 2 个空格作为缩进。

  **<font color=red>反例</font>**

  ```javascript
    function() {
    ∙∙∙∙const name;
    }

    function() {
    ∙const name;
    }
    ```

  **正例**

  ```javascript
    function() {
    ∙∙const name;
    }
    ```

- [18.2](#18.2) <a name="18.2"></a> 在逗号后面需要有一个空格，提高列表项的可读性。eslint: [`comma-spacing`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/style.js#L59)

  **<font color=red>反例</font>**

  ```javascript
    const arr = [1 , 2];
    const obj = { foo: 'bar' ,baz: 'qur' };
    foo(a ,b);
    new Foo(a ,b);
    function foo(a ,b){}
    ```

  **正例**

  ```javascript
    const arr = [1, 2];
    const obj = { foo: 'bar', baz: 'qur' };
    foo(a, b);
    new Foo(a, b);
    function foo(a, b){}
    ```

- [18.3](#18.3) <a name="18.3"></a> 在花括号前放一个空格。eslint：[`space-before-blocks`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/style.js/#L559)

  **<font color=red>反例</font>**

  ```javascript
    function test(){
      console.log('test');
    }

    dog.set('attr',{
      age: '1 year',
      breed: 'Bernese Mountain Dog',
    });
    ```

  **正例**

  ```javascript
    function test() {
      console.log('test');
    }

    dog.set('attr', {
      age: '1 year',
      breed: 'Bernese Mountain Dog',
    });
    ```

- [18.4](#18.4) <a name="18.4"></a>单行对象代码块中，块中代码行前后需要加空格。数组不需要。 eslint: [`object-curly-spacing`](http://gitlab.iwhalecloud.com/ngweb/eslint-config-ztesoft/blob/master/rules/styles.js#L463)

  **<font color=red>反例</font>**

  ```javascript
    const obj = {foo: 'bar'};
    const test = {foo: 'bar' };
    const item = { baz: {foo: 'qux'}};
    ```

  **正例**

  ```javascript
    const obj = {};
    const test = { foo: 'bar' };
    const item = { foo: { bar: 'baz' }, qux: 'quxx' };
    ```

- [18.5](#18.5) <a name="18.5"></a> 在函数表达式、匿名函数和箭头函数的左括号之前放一个空格。而函数声明的`function`的左括号之前不需要空格。eslint：[`space-before-function-paren`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/style.js/#L563)

  **<font color=red>反例</font>**

  ```javascript
    function foo () {
      // ...
    }
    const bar = function() {
      // ...
    };
    class Foo {
      constructor () {
        // ...
      }
    }
    const foo = {
      bar () {
        // ...
      }
    };
    const foo = async(a) => await a
    ```

  **正例**

  ```javascript
    function foo() {
      // ...
    }
    const bar = function () {
      // ...
    };
    class Foo {
      constructor() {
        // ...
      }
    }
    const foo = {
      bar() {
        // ...
      }
    };
    const foo = async (a) => await a
    ```

- [18.6](#18.6) <a name="18.7"></a> 箭头函数箭头前后都必须要有空格。eslint：[`arrow-spacing`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/es6.js/#L30)

  **<font color=red>反例</font>**

  ```javascript
    ()=> {};
    () =>{};
    (a)=> {};
    (a) =>{};
    a =>a;
    a=> a;
    ()=> {'\n'};
    () =>{'\n'};
    ```

  **正例**

  ```javascript
    () => {};
    (a) => {};
    a => a;
    () => {'\n'};
    ```

- [18.7](#18.7) <a name="18.8"></a> 在控制语句（`if`、`while` 等）的小括号前放一个空格。在函数调用及声明中，不在函数的参数列表前加空格。eslint：[`keyword-spacing`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/style.js/#L179)

  - 一些关键字`yield`,`typeof`等后面需要一个空格

  **<font color=red>反例</font>**

  ```javascript
    if(isJedi) {
      fight ();
    }

    function fight () {
      console.log ('Swooosh!');
    }
    ```

  **正例**

  ```javascript
    if (isJedi) {
      fight();
    }

    function fight() {
      console.log('Swooosh!');
    }
    ```

- [18.8](#18.8) <a name="18.9"></a> 在对象的属性中，要求键名与冒号之间没有空格，冒号与值之间有一个空格。 eslint：[`key-spacing`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/style.js#L175)

  **<font color=red>反例</font>**

  ```javascript
    const obj = { 'foo':42 };
    ```

  **正例**

  ```javascript
    const obj = { 'foo': 42 };
    ```

- [18.9](#18.9) <a name="18.10"></a> 使用空格把运算符隔开。eslint：[`space-infix-ops`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/style.js/#L576)

  **<font color=red>反例</font>**

  ```javascript
    const x=y+5;
    ```

  **正例**

  ```javascript
    const x = y + 5;
    ```

- [18.10](#18.10) <a name="18.11"></a> 一元字母操作符前后需要加空格，如：new，delete，typeof，void，yield。一元运算符如-，+，--，++，!，!!前后不用加空格。 eslint：[`space-unary-ops`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/style.js#L580)

  **<font color=red>反例</font>**

  ```javascript
    typeof!foo;
    void{foo:0};
    new[foo][0];
    delete(foo.bar);
    ++ foo;
    foo --;
    - foo;
    + '3';
    ```

  **正例**

  ```javascript
    delete foo.bar;
    new Foo;
    void 0;
    ++foo;
    foo--;
    -foo;
    +'3';
    ```

- [18.11](#18.11) <a name="18.12"></a> 代码注释符号后面要加一个空格。 eslint: [`spaced-comment`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/style.js#L590)

  **<font color=red>反例</font>**

  ```javascript
    //This is a comment with no whitespace at the beginning

    /*This is a comment with no whitespace at the beginning */
    ```

  **正例**

  ```javascript
    // This is a comment with a whitespace at the beginning

    /* This is a comment with a whitespace at the beginning */
    ```

- [18.12](#18.12) <a name="18.13"></a> 禁止剩余和扩展运算符及其表达式之间有空格。 eslint: [`rest-spread-spacing`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/es6.js#L181)

  **<font color=red>反例</font>**

  ```javascript
    fn(... args)
    [... arr, 4, 5, 6]
    let [a, b, ... arr] = [1, 2, 3, 4, 5];
    function fn(... args) { console.log(args); }
    let { x, y, ... z } = { x: 1, y: 2, a: 3, b: 4 };
    let n = { x, y, ... z };
    ```

  **正例**

  ```javascript
    fn(...args)
    [...arr, 4, 5, 6]
    let [a, b, ...arr] = [1, 2, 3, 4, 5];
    function fn(...args) { console.log(args); }
    let { x, y, ...z } = { x: 1, y: 2, a: 3, b: 4 };
    let n = { x, y, ...z };
    ```

- [18.13](#18.13) <a name="18.14"></a> 避免在正则表达式中使用多个空格。 eslint：[`no-regex-spaces`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/errors.js#L124)

  **<font color=red>反例</font>**

  ```javascript
    const re = /foo   bar/;
    const re = new RegExp('foo   bar');
    ```

  **正例**

  ```javascript
    const re = /foo {3}bar/;
    const re = new RegExp('foo {3}bar');
    ```

- [18.14](#18.14) <a name="18.15"></a> 避免在逻辑表达式、条件表达式、声明语句、数组元素、对象属性、序列、函数参数中使用多个空格，除了连续使用多个空格用于缩进以外，其他情况下连续使用多个空格通常是错误的。 eslint：[`no-multi-spaces`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/best-practices.js#L192)

  **<font color=red>反例</font>**

  ```javascript
    const a =  1;
    if(foo   === 'bar') {}
    a <<  b;
    const arr = [1,  2];
    a ?  b: c;
    ```

  **正例**

  ```javascript
    const a = 1;
    if(foo === 'bar') {}
    a << b
    const arr = [1, 2];
    a ? b : c
    ```

- [18.15](#18.15) <a name="18.16"></a> 禁止在数组的左右方括号之间有空格。 eslint：[`array-bracket-spacing`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/style.js#L15)

  **<font color=red>反例</font>**

  ```javascript
    const arr = [ 'foo', 'bar' ];
    const arr = ['foo', 'bar' ];
    const arr = [ ['foo'], 'bar'];
    const arr = [[ 'foo' ], 'bar'];
    const arr = [ 'foo',
      'bar',
    ];
    ```

  **正例**

  ```javascript
    const arr = [];
    const arr = ['foo', 'bar', 'baz'];
    const arr = [['foo'], 'bar', 'baz'];
    const arr = [
      'foo',
      'bar',
      'baz',
    ];
    const arr = ['foo',
      'bar',
    ];
    ```

- [18.16](#18.16) <a name="18.17"></a> 分号前面不应该有空格，分号后面有空格。 eslint: [`semi-spacing`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/style.js#L542)

  **<font color=red>反例</font>**

  ```javascript
    const foo ;
    throw new Error("error") ;
    while (a) { break ; }
    for (i = 0 ; i < 10 ; i += 1) {}
    for (i = 0;i < 10;i += 1) {}
    ```

  **正例**

  ```javascript
    const foo;
    throw new Error("error");
    while (a) { break; }
    for (i = 0; i < 10; i += 1) {}
    ```

- [18.17](#18.17) <a name="18.18"></a> 计算属性的[]内不允许使用空格。 eslint: [`computed-property-spacing`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/style.js#L81)

  **<font color=red>反例</font>**

  ```javascript
    obj[foo ];
    obj[ 'foo'];
    obj[foo[ bar ]];
    ```

  **正例**

  ```javascript
    obj[foo];
    obj['foo'];
    obj[foo[bar]];
    ```

- [18.18](#18.18) <a name="18.19"></a> 禁止行末尾有空格。  eslint: [`no-trailing-spaces`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/style.js#L429)

  **<font color=red>反例</font>**

  ```javascript
    const foo = 0;∙∙∙∙
    const baz = 5;∙
    ```

  **正例**

  ```javascript
    const foo = 0;
    const baz = 5;
    ```

<!-- **注意:** 允许在空行中留空格，不会检验报错 -->
- [18.19](#18.19) <a name="18.20"></a> 禁止左右圆括号()与它内部的元素之间有空格。 eslint: [`space-in-parens`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/style.js#L572)

  **<font color=red>反例</font>**

  ```javascript
    foo( 'bar');
    foo('bar' );
    foo( 'bar' );
    const foo = ( 1 + 2 ) * 3;
    ( function () { return 'bar'; }() );
    ```

  **正例**

  ```javascript
    foo();
    foo('bar');
    const foo = (1 + 2) * 3;
    (function () { return 'bar'; }());
    ```

- [18.20](#18.20) <a name="18.21"></a> 禁止在函数标识符和其调用之间有空格。 eslint: [`func-call-spacing`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/style.js#L93)

  **<font color=red>反例</font>**

  ```javascript
    fn ();
    fn
    ();
    ```

  **正例**

  ```javascript
    fn();
    ```

- [18.21](#18.21) <a name="18.22"></a> 如果对象的属性位于同一行，不允许在点周围或开始括号之前的空格。当对象和属性位于不同的行时，则允许使用空格，因为通常将新行添加到较长的属性链。 eslint: [`no-whitespace-before-property`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/style.js#L452)

  **<font color=red>反例</font>**

  ```javascript
    foo [bar];
    foo. bar;
    foo .bar;
    foo. bar. baz;
    ```

  **正例**

  ```javascript
    foo.bar;
    foo[bar];
    foo.bar.baz;
    foo
    .bar()
    .baz();
    ```

- [18.22](#18.22) <a name="18.23"></a> 禁止使用tab键。eslint: [`no-tabs`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/style.js#L421)

- [18.23](#18.23) <a name="18.24"></a> 在使用长方法链时进行缩进。使用前面的点 `.` 强调这是方法调用而不是新语句。.号调用对象属性时，应保持.号与属性在同一行。eslint：[`dot-location`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/best-practices.js#L43)

  - 单行链式调用， 应保持.号与属性在同一行
  - 最多只允许4个在同一行；多行链式调用，应保持.号与属性在同一行

  **<font color=red>反例</font>**

  ```javascript
    const foo = object.
            property;

    $('#items').find('.selected').highlight().end().find('.open').updateCount();

    $('#items').
        find('.selected').
        highlight().
        end().
        find('.open').
        updateCount();

    const leds = stage.selectAll('.led').data(data).enter().append('svg:svg').class('led', true)
        .attr('width', (radius + margin) * 2).append('svg:g')
        .attr('transform', 'translate(' + (radius + margin) + ',' + (radius + margin) + ')')
        .call(tron.led);
    ```

  **正例**

  ```javascript
    const foo = object
            .property;
    const bar = object.property;

    $('#items')
        .find('.selected')
        .highlight()
        .end()
        .find('.open')
        .updateCount();

    const leds = stage.selectAll('.led')
        .data(data)
        .enter().append('svg:svg')
        .classed('led', true)
        .attr('width', (radius + margin) * 2)
        .append('svg:g')
        .attr('transform', 'translate(' + (radius + margin) + ',' + (radius + margin) + ')')
        .call(tron.led);
    ```

- [18.24](#18.24) <a name="18.25"></a> 类成员之间需要有空行。eslint：[`lines-between-class-members`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/style.js/#L206)

  **<font color=red>反例</font>**

  ```javascript
    class MyClass {
      foo() {
        //...
      }
      bar() {
        //...
      }
    }
    ```

  **正例**

  ```javascript
    class MyClass {
      foo() {
        //...
      }

      bar() {
        //...
      }
    }
    ```

- [18.25](#18.25) <a name="18.26"></a> 在块末和新语句前插入空行。eslint：[`space-before-blocks`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/style.js/#L559)

  **<font color=red>反例</font>**

  ```javascript
    if (foo) {
      return bar;
    }
    return baz;

    const obj = {
      foo() {
      },
      bar() {
      },
    };
    return obj;
    ```

  **正例**

  ```javascript
    if (foo) {
      return bar;
    }

    return baz;

    const obj = {
      foo() {
      },

      bar() {
      },
    };

    return obj;
    ```

- [18.26](#18.26) <a name="18.27"></a> 代码中最多连续使用两行空行。  eslint: [`no-multiple-empty-lines`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/style.js#L372)

  **<font color=red>反例</font>**

  ```javascript
    const foo = 5;
    ∙∙∙∙
    ∙∙∙∙
    ∙∙∙∙
    const bar = 3;
    ```

  **正例**

  ```javascript
    const foo = 5;
    ∙∙∙∙
    const bar = 3;
    ```

- [18.27](#18.27) <a name="18.28"></a> 在文件末尾插入一个空行。eslint：[`eol-last`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/style.js#L89)

  **<font color=red>反例</font>**

  ```javascript
    (function(global) {
      // ...stuff...
    })(this);

    (function(global) {
      // ...stuff...
    })(this);↵
    ↵
    ```

  **正例**

  ```javascript
    (function(global) {
      // ...stuff...
    })(this);↵
    ```

- [18.28](#18.28) <a name="18.29"></a> 在最后一组`import`和`require`后要插入一个空行。eslint：[`import/newline-after-import`](http://gitlab.ztesoft.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/imports.js#L150)

  **<font color=red>反例</font>**

  ```javascript
    import * as foo from 'foo';
    const FOO = 'BAR';
    import * as foo from 'foo';
    const FOO = 'BAR';

    import { bar }  from 'bar-lib';
    const FOO = require('./foo');
    const BAZ = 1;
    const BAR = require('./bar');
    ```

  **正例**

  ```javascript
    import defaultExport from './foo';

    const FOO = 'BAR';
    import defaultExport from './foo';
    import { bar }  from 'bar-lib';

    const FOO = 'BAR';
    const FOO = require('./foo');
    const BAR = require('./bar');

    const BAZ = 1;
    ```

# 逗号

- [19.1](#19.1) <a name="19.1"></a> 行首逗号：**不需要**。eslint：[`comma-style`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/style.js/#L63)

  **<font color=red>反例</font>**

  ```javascript
    const story = [
        once
      , upon
      , aTime
    ];

    const hero = {
        firstName: 'Ada'
      , lastName: 'Lovelace'
      , birthYear: 1815
      , superPower: 'computers'
    };
    ```

  **正例**

  ```javascript
    const story = [
      once,
      upon,
      aTime,
    ];

    const hero = {
      firstName: 'Ada',
      lastName: 'Lovelace',
      birthYear: 1815,
      superPower: 'computers',
    };
    ```

- [19.2](#19.2) <a name="19.2"></a> 增加结尾的逗号: **需要**。eslint：[`comma-dangle`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/style.js/#L49)

  > 为什么? 这会让 git diffs 更干净。另外，像 babel 这样的转译器会移除结尾多余的逗号，也就是说你不必担心老旧浏览器的尾逗号问题

  **<font color=red>反例</font>**

  ```javascript
    //  git diff without trailing comma
    const hero = {
         firstName: 'Florence',
         lastName: 'Nightingale'
         lastName: 'Nightingale',
         inventorOf: ['coxcomb graph', 'modern nursing']
    }

    const hero = {
      firstName: 'Dana',
      lastName: 'Scully'
    };

    const heroes = [
      'Batman',
      'Superman'
    ];
    ```

  **正例**

  ```javascript
    const hero = {
         firstName: 'Florence',
         lastName: 'Nightingale',
         inventorOf: ['coxcomb chart', 'modern nursing'],
    }

    const hero = {
      firstName: 'Dana',
      lastName: 'Scully',
    };

    const heroes = [
      'Batman',
      'Superman',
    ];
    ```

- [19.3](#19.3) <a name="19.3"></a> 避免使用逗号操作符,在for语句的初始化或更新部分或如果表达式序列明确地包含在括号中时可以使用逗号运算符。 eslint: [`no-sequences`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/best-practices.js#L317)

  **<font color=red>反例</font>**

  ```javascript
    var testA = 5;
    var testB = 0;
    testA = testB += 5, testA + testB;
    while (testA = next(), testA && testA.length) {}
    ```

  **正例**

  ```javascript
    foo = (doSomething(), val);
    (0, eval)("doSomething();");
    do {} while ((doSomething(), !!test));
    for (i = 0, j = 10; i < j; i++, j--) {}
    ```

- [19.4](#19.4) <a name="19.4"></a> 禁止使用多个逗号来声明一个空数组。 eslint: [`no-sparse-arrays`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/errors.js#L128)

  **<font color=red>反例</font>**

  ```javascript
    const items = [,];
    const colors = ['red',, 'blue'];
    ```

  **正例**

  ```javascript
    const items = [];
    const colors = ['red', 'blue'];
    ```

# 分号

- [20.1](#20.1) <a name="20.1"></a> **使用分号** 不允许省略。eslint: [`semi`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/style.js#L538) eslint: [`no-unexpected-multiline`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/errors.js#L137)

  **<font color=red>反例</font>**

  ```javascript
    (function() {
      const name = 'Skywalker'
      return name
    })()
    ```

  **正例**

  ```javascript
    (() => {
      const name = 'Skywalker';
      return name;
    })();

    // 防止函数在两个 IIFE 合并时被当成一个参数
    ;(() => {
      const name = 'Skywalker';
      return name;
    })();
    ```

- [20.2](#20.2) <a name="20.2"></a> 分号一定出现在句末。 eslint: [`semi-style`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/style.js#L546)

  **<font color=red>反例</font>**

  ```javascript
    foo()
    ;[1, 2, 3].forEach(bar)

    for (
        let i = 0
        ; i < 10
        ; i += 1
    ) {
        foo()
    }
    ```

  **正例**

  ```javascript
    foo();
    [1, 2, 3].forEach(bar);

    for (
        let i = 0;
        i < 10;
        i += 1
    ) {
        foo();
    }
    ```

- [20.3](#20.3) <a name="20.3"></a> 不允许使用多余的分号。 eslint: [`no-extra-semi`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/errors.js#L89)

  **<font color=red>反例</font>**

  ```javascript
    const x = 5;;
    function foo() {
        // code
    };
    ```

  **正例**

  ```javascript
    const x = 5;
    const foo = function () {
        // code
    };
    function bar () {
        // code
    }
    ```

  [Read more](http://stackoverflow.com/a/7365214/1712802).

# 类型转换

- [21.1](#21.1) <a name="21.1"></a> 在语句开始时执行类型转换。

- [21.2](#21.2) <a name="21.2"></a> 字符串：

  **<font color=red>反例</font>**

  ```javascript
    //  => this.reviewScore = 9;

    const totalScore = new String(this.reviewScore); // typeof totalScore is "object" not "string"

    const totalScore = this.reviewScore + ''; // invokes this.reviewScore.valueOf()

    const totalScore = this.reviewScore.toString(); // isn’t guaranteed to return a string
    ```

  **正例**

  ```javascript
    //  => this.reviewScore = 9;

    const totalScore = String(this.reviewScore);
    ```

- [21.3](#21.3) <a name="21.3"></a> 对数字使用 `parseInt` 转换，并带上类型转换的基数。eslint: [`radix`](http://gitlab.iwhalecloud.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/best-practices.js#L391)

  **<font color=red>反例</font>**

  ```javascript
    const inputValue = '4';

    const val = new Number(inputValue);

    const val = +inputValue;

    const val = inputValue >> 0;

    const val = parseInt(inputValue);
    ```

  **正例**

  ```javascript
    const inputValue = '4';

    const val = Number(inputValue);

    const val = parseInt(inputValue, 10);
    ```

- [21.5](#21.5) <a name="21.5"></a> 禁止使用位操作运算符. eslint: `no-bitwise`(https://eslint.org/docs/rules/no-bitwise)

  > 当你使用位运算的时候要小心。 数字总是被以 64-bit 值 的形式表示，但是位运算总是返回一个 32-bit 的整数。 对于大于 32 位的整数值，位运算可能会导致意外行为。 最大的 32 位整数是： 2,147,483,647。

  **<font color=red>反例</font>**

  ```javascript
    var test = y | z;
    var test = y & z;
    x |= y;
    x &= y;
    var test = y ^ z;
    var test = ~ z;
    var test = y << z;
    var test = y >> z;
    ```

  **正例**

  ```javascript
    var test = y || z;
    var test = y && z;
    var test = y > z;
    var test = y < z;
    test += y;
    ```

- [21.6](#21.6) <a name="21.6"></a> 布尔:

  **<font color=red>反例</font>**

  ```javascript
    const age = 0;

    const hasAge = new Boolean(age);
    ```

  **正例**

  ```javascript
    const age = 0;

    const hasAge = Boolean(age);

    const hasAge = !!age;
    ```

# 命名规则

- [22.1](#22.1) <a name="22.1"></a> 避免单字母命名。命名应具备描述性。

  **<font color=red>反例</font>**

  ```javascript
    // 不报错但不推荐使用
    function q() {
      // ...stuff...
    }
    ```

  **正例**

  ```javascript
    function query() {
      // ..stuff..
    }
    ```

- [22.2](#22.2) <a name="22.2"></a> 使用小驼峰式命名对象、函数和实例。eslint: [`camelcase`](http://gitlab.ztesoft.com/fish-x/eslint-config-whalecloud/blob/issue%231/rules/style.js#L28)

  **<font color=red>反例</font>**

  ```javascript
    const OBJEcttsssss = {};
    const this_is_my_object = {};
    function c() {}
    ```

  **正例**

  ```javascript
    const thisIsMyObject = {};
    function thisIsMyFunction() {}
    ```

- [22.3](#22.3) <a name="22.3"></a> 使用帕斯卡式命名构造函数或类。

  **<font color=red>反例</font>**

  ```javascript
    function user(options) {
      this.name = options.name;
    }

    const bad = new user({
      name: 'nope',
    });
    ```

  **正例**

  ```javascript
    class User {
      constructor(options) {
        this.name = options.name;
      }
    }

    const good = new User({
      name: 'yup',
    });
    ```

- [22.4](#22.4) <a name="22.4"></a> 别保存 `this` 的引用。使用箭头函数或 Function#bind。

  **<font color=red>反例</font>**

  ```javascript
    function foo() {
      const self = this;
      return function() {
        console.log(self);
      };
    }

    function foo() {
      const that = this;
      return function() {
        console.log(that);
      };
    }
    ```

  **正例**

  ```javascript
    function foo() {
      return () => {
        console.log(this);
      };
    }
    ```

- [22.5](#22.5) <a name="22.5"></a> 如果你的文件只输出一个类，那你的文件名必须和类名完全保持一致。

  **<font color=red>反例</font>**

  ```javascript
    // file contents
    class CheckBox {
      // ...
    }
    export default CheckBox;

    import CheckBox from './checkBox';

    import CheckBox from './check_box';
    ```

  **正例**

  ```javascript
    // file contents
    class CheckBox {
      // ...
    }
    export default CheckBox;

    import CheckBox from './CheckBox';
    ```

- [22.6](#22.6) <a name="22.6"></a> 当你导出默认的函数时使用驼峰式命名。你的文件名必须和函数名完全保持一致。

  **正例**

  ```javascript
    function makeStyleGuide() {
    }

    export default makeStyleGuide;
    ```

- [22.7](#22.7) <a name="22.7"></a> 当你导出单例、函数库、空对象时使用帕斯卡式命名。

  **正例**

  ```javascript
    class Singleton {
      constructor() {
        if (Singleton.instance) {
          return Singleton.instance
        }
        Singleton.instance = this
        return this
      }

      someMethod() {
        console.log('I am a method of the Singleton class')
      }
    }
    export default Singleton;
    ```

# 存取器

- [23.1](#23.1) <a name="23.1"></a> 对于属性的存取函数不是必须的。

- [23.2](#23.2) <a name="23.2"></a> 如果你需要存取函数时使用 `getVal()` 和 `setVal('hello')`。

  > 不要使用 JavaScript 的 getters/setters 方法，因为它们会导致意外的副作用，并且更加难以测试、维护和推敲。

  **<font color=red>反例</font>**

  ```javascript
    dragon.age();

    dragon.age(25);
    ```

  **正例**

  ```javascript
    dragon.getAge();

    dragon.setAge(25);
    ```

- [23.3](#23.3) <a name="23.3"></a> 如果属性是布尔值，使用 `isVal()` 或 `hasVal()`。

  **<font color=red>反例</font>**

  ```javascript
    if (!dragon.age()) {
      return false;
    }
    ```

  **正例**

  ```javascript
    if (!dragon.hasAge()) {
      return false;
    }
    ```

- [23.4](#23.4) <a name="23.4"></a> 创建 `get()` 和 `set()` 函数是可以的，但要保持一致。

  **正例**

  ```javascript
    class Jedi {
      constructor(options = {}) {
        const lightsaber = options.lightsaber || 'blue';
        this.set('lightsaber', lightsaber);
      }

      set(key, val) {
        this[key] = val;
      }

      get(key) {
        return this[key];
      }
    }
    ```

# 云雀检测工具和方法

`FishX` 封装的一套自己的 `eslint` 代码检测规则，这些规则都是按照以上的编程规范来制定的。

## 如何使用

- 全局使用

  全局安装 `@fishx/cli`：

  ```bash
    $ npm install -g @fishx/cli@4.3.11-beta.32 --force
    ```

- 命令行

  在工程的根目录下执行如下命令行可以进行校验（注：命令行运行所在的根目录需要存在.eslintignore文件）

  - es6

  检测所有js,jsx文件（注：云雀前端代码分析即是执行本命令，输出xml检测结果）

  ```bash
    $ fishx lint --eslint --type=es6 --format=xml --ext='.js,.jsx' "**/*.?(js|jsx)"
    ```

  检测单个js文件

  ```bash
    $ fishx lint --eslint --type=es6 --format=xml --ext='.js,.jsx' "src/pages/todo/index.js"
    ```

  - typescript

  检测所有ts,tsx文件（注：云雀前端代码分析即是执行本命令，输出xml检测结果）

  ```bash
    $ fishx lint --eslint --type=typescript --format=xml --ext='.ts,.tsx' "**/*.?(ts|tsx)"
    ```

  检测单个ts文件

  ```bash
    $ fishx lint --eslint --type=typescript --format=xml --ext='.ts,.tsx' "src/pages/todo/index.ts"
    ```

  > 需要注意的是，如果在运行时出现node内存溢出的报错，可以在检测命令前加上 `NODE_OPTIONS=--max_old_space_size=9000` 参数, windows 平台可以使用 `cross-env` 兼容，比如: `cross-env NODE_OPTIONS=--max_old_space_size=9000`。

## 如何创建自己的研发云CI/CD检测流程

1. 进入研发云（https://dev.iwhalecloud.com）并登陆，点击有上角菜单——>开发中心——>持续构建，如下图：

   ![image](uploads/4084/5136f87a-4765-4e3e-9c54-827d1f6f2fa0/cicd1.png)

2. 进入持续构建页面后点击新建构建，进入新建页面如下图，配置自己的代码归属，在语言模板处选择JS，最后选择要构建的的镜像。根据项目要求一步步创建

   ![image](uploads/25208/871ee1bf-f569-4bf7-8cd2-6dbe81ead9b6/image.png)

3. 在"代码分析"页面打开“是否需要代码分析选项”，之后一直点击next到最后一步点击create

   ![image](uploads/25208/0619fdd0-5e1d-4eca-82f8-dba833570e4a/image.png)

4. 在流程代码分析节点中，需要根据项目前端代码类型 选择一下JS语言类型 目前有 `ES5`、`ES6`、`TYPESCRIPT`、`ES6+TYPESCRIPT`
   ![image](uploads/25208/0f83d8f3-fd4f-4bee-9ce6-e1f443cd52da/image.png)

5. 点击“高级配置”可以选择es6编译所使用的node版本号
   ![image](uploads/25208/2cb3f39e-5c3c-4953-bb1a-9b1ffc4c4ad7/image.png)

6. 创建 静态检查例外配置例外文件：

   - 进入 项目 的根目录下的 `CI_Config` 目录下创建  `.eslintignore` 文件。
     ![image](uploads/25208/54ae7718-2261-4c80-b99d-323a0c863b81/image.png)
7. 找到创建的流程点击构建，等待流程构建完毕，在下方找到对应的检测结果，点击即可查看，如下图：
   ![image](uploads/25208/b7dbbf42-0c63-418b-8704-28dc433bd3a8/image.png)

# 主流前端框架的eslint、prettier、editorconfig的配置指导

## CRA框架

CRA全称create-react-app，是React官方脚手架
通过 `npx create-react-app my-app` 命令创建 CRA模板

### 添加公司eslint规则

1. 安装所需要的依赖

```sh
yarn add @whalecloud/eslint-config -D
```

2. 去掉package.json 里面的eslintConfig字段

```diff
- "eslintConfig": {
-    "extends": "react-app"
-  }
```

3. 项目根目录增加.editorconfig .prettierrc .eslintrc.js 文件
   .eslintrc.js 配置文件（模板默认为js）

```javascript
module.exports = {
  extends: '@whalecloud/eslint-config',
};

```

如果创建是CRA Typescript模板则使用如下 .eslintrc.js 配置文件

```javascript
module.exports = {
  extends: '@whalecloud/eslint-config/configurations/typescript',
};

```

.prettierrc配置文件:

```json
{
  "singleQuote": true,
  "trailingComma": "all",
  "printWidth": 150,
  "overrides": [
    {
      "files": ".prettierrc",
      "options": { "parser": "json" }
    }
  ]
}

```

.editorconfig配置文件:

```javascript
# http://editorconfig.org
root = true

[*]
indent_style = space
indent_size = 2
end_of_line = lf
charset = utf-8
trim_trailing_whitespace = true
insert_final_newline = true

[*.md]
trim_trailing_whitespace = false

[Makefile]
indent_style = tab
```

4. 配置[.eslintignore]
   在项目根目录新建CI_Config目录，在CI_Config目录中创建.eslintignore配置文件
   .eslintignore配置文件

```js
# 例外场景3：外部引入的开源软件。允许目录和文件级例外，需要给出开源代码对应的访问地址。
# node_modules目录里是第三方npm地址，开源地址：https://xxx
/node_modules
# 例外场景4：工具自动生成的代码。允许目录和文件级例外，需要给出代码生成工具的名称。
# 压缩后的js文件
/build
# 例外场景3：外部引入的开源软件。允许目录和文件级例外，需要给出开源代码对应的访问地址。
# public目录里是引入的第三方js，开源地址：https://xxx
**/public
```

注：各个项目根据自己项目实际情况，进行eslintignore的配置。
ZCM构建的时候会找CI_Config下的.eslintignore配置文件，建议根目录也放一份相同内容的的.eslintignore配置文件，用于本地检测

5. package.json里面增加 eslint命令

```json
  "scripts": {
    ...
+   "eslint": "eslint --ext=.js,.jsx ./"
  },
```

运行`npm run eslint`进行本地单独检测。检查结果与ci代码检查结果一致

注：如果要去掉 npm start 或者 npm build 自动eslint，可以在根目录新建 .env文件 内容如下：

```properties
DISABLE_ESLINT_PLUGIN=true

```

6. 参考示例流程号
   66401|es6-cra-app    项目：demo

## FishX框架

`FishX` 是针对公司未来转向 `React` 技术栈，基于 `React` 提供的一系列前端框架平台的名称
通过 `yarn create fishx appName` 命令创建 fishx模板
FishX框架生成的模板 用户不需要做更改（已经内置配置文件）， 本地运行run lint即可 本地和线上一致
1. 参考示例流程号
   66440|es6-fishx-app    项目：demo

## umi框架

umi中文可发音为**乌米**，是可扩展的企业级前端应用框架
通过 `yarn create @umijs/umi-app` 命令创建 umi模板

### 添加公司eslint规则

1. 安装所需要的依赖

```sh
yarn add @whalecloud/eslint-config -D
```

2. 项目根目录修改.editorconfig .prettierrc .eslintrc.js 文件
   .eslintrc.js 配置文件（模板默认为ts）

```javascript
module.exports = {
  extends: '@whalecloud/eslint-config/configurations/typescript',
};

```

如果创建是umi js模板则使用如下 .eslintrc.js 配置文件

```javascript
module.exports = {
  extends: '@whalecloud/eslint-config',
};

```

.prettierrc配置文件:

```json
{
  "singleQuote": true,
  "trailingComma": "all",
  "printWidth": 150,
  "overrides": [
    {
      "files": ".prettierrc",
      "options": { "parser": "json" }
    }
  ]
}

```

.editorconfig配置文件:

```javascript
# http://editorconfig.org
root = true

[*]
indent_style = space
indent_size = 2
end_of_line = lf
charset = utf-8
trim_trailing_whitespace = true
insert_final_newline = true

[*.md]
trim_trailing_whitespace = false

[Makefile]
indent_style = tab
```

4. 配置[.eslintignore]
   在项目根目录新建CI_Config目录，在CI_Config目录中创建.eslintignore配置文件
   .eslintignore配置文件

```js
# 例外场景3：外部引入的开源软件。允许目录和文件级例外，需要给出开源代码对应的访问地址。
# node_modules目录里是第三方npm地址，开源地址：https://xxx
/node_modules
# 例外场景4：工具自动生成的代码。允许目录和文件级例外，需要给出代码生成工具的名称。
# 压缩后的js文件
/build
# 例外场景3：外部引入的开源软件。允许目录和文件级例外，需要给出开源代码对应的访问地址。
# public目录里是引入的第三方js，开源地址：https://xxx
**/public
```

注：各个项目根据自己项目实际情况，进行eslintignore的配置。
ZCM构建的时候会找CI_Config下的.eslintignore配置文件，建议根目录也放一份相同内容的的.eslintignore配置文件，用于本地检测

5. package.json里面增加 eslint命令

```json
  "scripts": {
    ...
+   "eslint": "eslint --ext=.js,.jsx ./"
  },
```

运行`npm run eslint`进行本地单独检测。检查结果与ci代码检查结果一致

6. 参考示例流程号
   66433|es6-umi-app    项目：demo

## alitajs框架

alitajs框架是基于 Umi 的大前端开发框架
通过 `pnpx create-alita` 命令创建 alitajs模板

### 添加公司eslint规则

1. 安装所需要的依赖

```sh
yarn add @whalecloud/eslint-config -D
```

2. 项目根目录新增修改.editorconfig .prettierrc .eslintrc.js 文件
   .eslintrc.js 配置文件

```javascript
module.exports = {
  extends: '@whalecloud/eslint-config/configurations/typescript',
};
```

将.prettierrc.js重命名为.prettierrc.json        
.prettierrc.json配置文件:

```json
{
  "singleQuote": true,
  "trailingComma": "all",
  "printWidth": 150,
  "overrides": [
    {
      "files": ".prettierrc",
      "options": { "parser": "json" }
    }
  ]
}

```

.editorconfig配置文件:

```javascript
# http://editorconfig.org
root = true

[*]
indent_style = space
indent_size = 2
end_of_line = lf
charset = utf-8
trim_trailing_whitespace = true
insert_final_newline = true

[*.md]
trim_trailing_whitespace = false

[Makefile]
indent_style = tab
```

4. 配置[.eslintignore]
   在项目根目录新建CI_Config目录，在CI_Config目录中创建.eslintignore配置文件
   .eslintignore配置文件

```js
# 例外场景3：外部引入的开源软件。允许目录和文件级例外，需要给出开源代码对应的访问地址。
# node_modules目录里是第三方npm地址，开源地址：https://xxx
/node_modules
# 例外场景4：工具自动生成的代码。允许目录和文件级例外，需要给出代码生成工具的名称。
# 压缩后的js文件
/build
# 例外场景5：外部引入的开源软件。允许目录和文件级例外，需要给出开源代码对应的访问地址。
# public目录里是引入的第三方js，开源地址：https://xxx
**/public
#例外场景6：测试代码。允许目录和文件级例外，路径或文件名中必须有test字样。
**/__tests__
```

注：各个项目根据自己项目实际情况，进行eslintignore的配置。
ZCM构建的时候会找CI_Config下的.eslintignore配置文件，建议根目录也放一份相同内容的的.eslintignore配置文件，用于本地检测

5. package.json里面增加 eslint命令

```json
  "scripts": {
    ...
+   "eslint": "eslint --ext=.js,.jsx ./"
  },
```

运行`npm run eslint`进行本地单独检测。检查结果与ci代码检查结果一致

6. 参考示例流程号
   66435|es6-alita-app    项目：demo

## vue框架

vue是渐进式JavaScript框架
易学易用，性能出色，适用场景丰富的 Web 前端框架
通过 `npm init vue@latest` 命令创建 vue模板

### 添加公司eslint规则

1. 安装所需要的依赖

```sh
yarn add @whalecloud/eslint-config -D
```

2. 项目根目录修改.editorconfig .prettierrc .eslintrc.cjs 文件
   .eslintrc.cjs 配置文件（模板选择Add TypeScript）

```javascript
module.exports = {
  extends: '@whalecloud/eslint-config/configurations/typescript',
};

```

.eslintrc.cjs 配置文件（模板没有选择Add TypeScript）

```javascript
module.exports = {
  extends: '@whalecloud/eslint-config',
};

```

将.prettierrc.js重命名为.prettierrc.json  .prettierrc.json配置文件:

```json
{
  "singleQuote": true,
  "trailingComma": "all",
  "printWidth": 150,
  "overrides": [
    {
      "files": ".prettierrc",
      "options": { "parser": "json" }
    }
  ]
}

```

.editorconfig配置文件:

```javascript
# http://editorconfig.org
root = true

[*]
indent_style = space
indent_size = 2
end_of_line = lf
charset = utf-8
trim_trailing_whitespace = true
insert_final_newline = true

[*.md]
trim_trailing_whitespace = false

[Makefile]
indent_style = tab
```

4. 配置[.eslintignore]
   在项目根目录新建CI_Config目录，在CI_Config目录中创建.eslintignore配置文件
   .eslintignore配置文件

```js
# 例外场景3：外部引入的开源软件。允许目录和文件级例外，需要给出开源代码对应的访问地址。
# node_modules目录里是第三方npm地址，开源地址：https://xxx
/node_modules
# 例外场景4：工具自动生成的代码。允许目录和文件级例外，需要给出代码生成工具的名称。
# 压缩后的js文件
/build
# 例外场景5：外部引入的开源软件。允许目录和文件级例外，需要给出开源代码对应的访问地址。
# public目录里是引入的第三方js，开源地址：https://xxx
**/public
#例外场景6：测试代码。允许目录和文件级例外，路径或文件名中必须有test字样。
**/__tests__
```

注：各个项目根据自己项目实际情况，进行eslintignore的配置。
ZCM构建的时候会找CI_Config下的.eslintignore配置文件，建议根目录也放一份相同内容的的.eslintignore配置文件，用于本地检测

5. package.json里面增加 eslint命令

```json
  "scripts": {
    ...
+   "eslint": "eslint --ext=.js,.jsx ./"
  },
```

运行`npm run eslint`进行本地单独检测。检查结果与ci代码检查结果一致

6. 参考示例流程号
   66437|es6-vue-app    项目：demo

## 五个框架配置示例文件下载

| 组件 |  配置文件地址 |
| :--- | :--- |
| CRA |  [http://gitlab.iwhalecloud.com/CoP/JS_Specification/-/tree/master/rules/cra](http://gitlab.iwhalecloud.com/CoP/JS_Specification/-/tree/master/rules/cra) |
| Fishx |  [http://gitlab.iwhalecloud.com/CoP/JS_Specification/-/tree/master/rules/fishx](http://gitlab.iwhalecloud.com/CoP/JS_Specification/-/tree/master/rules/fishx) |
| umi |  [http://gitlab.iwhalecloud.com/CoP/JS_Specification/-/tree/master/rules/umi](http://gitlab.iwhalecloud.com/CoP/JS_Specification/-/tree/master/rules/umi) |
| alita |  [http://gitlab.iwhalecloud.com/CoP/JS_Specification/-/tree/master/rules/alita](http://gitlab.iwhalecloud.com/CoP/JS_Specification/-/tree/master/rules/alita) |
| vue |  [http://gitlab.iwhalecloud.com/CoP/JS_Specification/-/tree/master/rules/vue](http://gitlab.iwhalecloud.com/CoP/JS_Specification/-/tree/master/rules/vue) |

# 开发工具插件安装配置

## vscode插件安装配置

### ESLint 插件安装配置

1. 插件安装
   打开VSCode，在插件扩展商店搜索 `eslint`，点击安装，并重新加载；
   ![image](uploads/26110/06dca2c7-a580-4e23-9968-1b29bf96c3f9/image.png)

2. 插件配置
   确保 VSCode 输出面板中 ESlint  ESLint server是处于工作状态的，并且找到npm ESlint  
   ![image](uploads/26110/3fe55125-5f44-40f4-9ab6-6e744da06c84/image.png)

VSCode 的 ESLint 插件优先使用安装在当前项目中的 npm ESLint，如果当前项目中没有提供，它会使用全局安装的 npm ESLint。
然后看是否存在 ESLint 配置文件`.eslintrc`，如果没有的话就不会去校验；如果存在VSCode 会根据你当前项目下的 `.eslintrc` 文件的规则来验证代码

### Prettier - Code formatter 插件 安装配置

1. 插件安装
   打开VSCode，在插件扩展商店搜索 `Prettier`，点击安装，并重新加载；
   ![image](uploads/26110/51018b4e-33df-4d96-88bc-91c8d0e0fffd/image.png)

2. 插件配置
   通过 VSCode -> 首选项 -> 设置（settings.json），可配置 VSCode 编辑器的默认格式化工具，也可根据语言设置其对应的默认格式化工具。

```json
{
  "editor.defaultFormatter": "esbenp.prettier-vscode", // 设置编辑器的默认格式化工具为 prettier
  "[javascript]": { // 根据语言设置其对应的默认格式化工具
      "editor.defaultFormatter": "esbenp.prettier-vscode", // 设置 javascript 的默认格式化工具为 prettier
      "editor.formatOnSave": true, // 保存的时候自动格式化
  },
}
```

在项目根目录添加自定义配置文件.prettierrc
确保VSCode 输出面板中 Prettier  处于工作状态的。
![image](uploads/26110/85198f99-ce31-4e9e-9ed8-16ec67da2a28/image.png)

VSCode 的 prettier 插件将使用当前项目本地依赖中的npm prettier，如果当前项目中没有提供，将使用 prettier-vscode 插件捆绑的 prettier。
然后看是否存在 prettier 配置文件`.prettierrc`，如果存在VSCode 会根据你当前项目下的 `.prettierrc` 文件的规则来格式化代码

### EditorConfig 插件 安装配置

1. 插件安装
   打开VSCode，在插件扩展商店搜索 `EditorConfig`，点击安装，并重新加载；
   ![image](uploads/26110/ba8c58bc-3258-4960-bd3f-1d8721643c41/image.png)

2. 插件配置
   在项目根目录添加自定义配置文件 .editorconfig
   确保VSCode 输出面板中 EditorConfig  处于工作状态的。
   ![image](uploads/26110/60397744-a286-4b76-bab7-14296fc247f3/image.png)

配置完之后，VSCode 会根据你当前项目下的 `.editorconfig` 文件进行文本编辑器设置

## IntelliJ Idea插件安装配置

### ESLint 插件安装配置

1. 插件安装
   IntelliJ Idea自带ESLint插件

2. 插件配置
   通过 File -> Settings -> Languages & Frameworks -> JavaScript -> Code Quality Tools -> ESLint，可配置 ESlint插件
   ![image](uploads/26110/0b4a248d-e47a-4fca-9386-c4d7ea0a42e4/image.png)

配置完之后，选择需要检测js的文件或文件夹，右键菜单选择 Analyze -> Inspect Code

### Prettier 插件安装配置

1. 插件安装
   打开File-Settings在Plugins中安装Prettier插件并且重启
   ![image](uploads/26110/6be1da45-28df-404d-a96f-835d94187e14/image.png)

2. 插件配置
   通过 File -> Settings -> Languages & Frameworks -> JavaScript -> Prettier，可配置 Prettier插件
   ![image](uploads/26110/970b6aab-1e0b-484d-b93c-cb7b092e132c/image.png)

配置完之后，在需要格式化的文件中用Shift+Ctrl+A
![image](uploads/26110/8bfb0cfb-61a4-4f33-b948-6393d96d1ff9/image.png)
如图所示也可以直接用ctrl+alt+Shift+P快捷键来美化当前文件

### EditorConfig 插件安装配置

1. 插件安装
   IntelliJ Idea自带EditorConfig插件

2. 插件配置
   通过 File -> Settings -> Editor -> Code Style，可配置开启 EditorConfig
   ![image](uploads/26110/fab2abff-1fe3-4e26-94e1-3442ce50d056/image.png)

配置完之后，IntelliJ Idea 会根据你当前项目下的 `.editorconfig` 文件进行文本编辑器设置

# FAQ

**Q：我的项目 前端告警数量很多，有没有什么工具可以把ESLint检查出的代码给自动修复的呢？**
A: ESLint有个fix命令能修复ESLint检查出的错误。但ESLint fix命令会改变业务逻辑的，举一个例子 如它会把 == 都换成 ===，之前zmp项目就遇到导致业务逻辑出了问题。
规范组做了个`[浩鲸js规范空白格式化工具](https://docs.iwhalecloud.com/bidjefd/share?d=gcb#didqysAxfY)` 对空格、空行、双引号之类不影响业务逻辑的进行格式化。（注：目前只对空格、空行、双引号之类不影响业务逻辑的错误进行修复，因为格式化自动修复涉及到业务代码的修改，要谨慎）

**Q：eslint效验的规则有相关的文档说明么？我们这边ZCM代码分析的XML错误日志，想参考文档改下代码**
A: 举个例子  
`<error line="508" column="11" severity="error" message="'originSwaggerData' is never reassigned. Use 'const' instead. (prefer-const)" source="eslint.rules.prefer-const"/>`
1. 打开 [http://eslint.cn/](http://eslint.cn/)  或者[eslint英文官网](https://eslint.org/)
2. 在顶部输入框中 输入XML中`source`字段的 prefer-const
3. 即显示出详细的规则说明，正反例，以及如何修复
