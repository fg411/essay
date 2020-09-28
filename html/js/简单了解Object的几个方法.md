
 - Object.defineProperty()
 - Object.keys()
 - Object.getOwnPropertyNames()
 - Object.isFrozen()
 - Object.freeze()

---------

### Object.defineProperty()

　　`Object.defineProperty()` 方法会直接在一个对象上定义一个新属性，或者修改一个对象的现有属性，并返回此对象

　　**语法**：
>Object.defineProperty(obj, prop, descriptor)

　　**参数**：

　　`obj` — 要定义属性的对象

　　`prop` — 要定义或修改的属性的名称或 `Symbol`

　　`descriptor` — 要定义或修改的属性描述符

　　**返回值**：

　　被传递给函数的对象

　　对象里目前存在的属性描述符有两种主要形式：`数据描述符`和`存取描述符`。

　　数据描述符是一个具有值的属性，该值可以是可写的，也可以是不可写的；存取描述符是由 `getter` 函数和 `setter` 函数所描述的属性。一个描述符只能是这两者其中之一；不能同时是两者


| |configurable|enumerable|value|writable|get|set|
|---|---|---|---|---|---|---|
|数据描述符|可以|可以|可以|可以|不可以|不可以|
|存取描述符|可以|可以|不可以|不可以|可以|可以|

 - `configurable`
 
　　当且仅当该属性的 `configurable` 键值为 `true` 时，该属性的描述符才能够被改变，同时该属性也能从对应的对象上被删除。默认为 `false`。
 - `enumerable`
 
 　　当且仅当该属性的 `enumerable` 键值为 `true` 时，该属性才会出现在对象的枚举属性中。默认为 `false`。
 - `value`
 
　　该属性对应的值。可以是任何有效的 JavaScript 值（数值，对象，函数等）。默认为 `undefined`
 - `writable`

　　当且仅当该属性的 `writable` 键值为 `true` 时，属性的值，也就是上面的 `value`，才能被赋值运算符改变。默认为 false
 - `get`
 
　　属性的 getter 函数，如果没有 `getter`，则为 `undefined`。当访问该属性时，会调用此函数。执行时不传入任何参数，但是会传入 this 对象（由于继承关系，这里的this并不一定是定义该属性的对象）。该函数的返回值会被用作属性的值。默认为 `undefined`
 - `set`

　　属性的 setter 函数，如果没有 `setter`，则为 `undefined`。当属性值被修改时，会调用此函数。该方法接受一个参数（也就是被赋予的新值），会传入赋值时的 this 对象。默认为 `undefined`

　　如果一个描述符不具有 value、writable、get 和 set 中的任意一个键，那么它将被认为是一个数据描述符。如果一个描述符同时拥有 value 或 writable 和 get 或 set 键，则会产生一个异常

```javascript
var o = {};
Object.defineProperty(o, "a", {
  value : 37,
  writable : true,
  enumerable : true,
  configurable : true
});

var obj = {};
var b;
Object.defineProperty(obj, 'b', {
    enumerable : true,
    configurable : true,
    get: () => {
        return b
    },
    set: newVal => b = newVal
})
```

------

### Object.keys()

　　`Object.keys()` 方法会返回一个由一个给定对象的自身 <u>可枚举属性</u> 组成的数组，数组中属性名的排列顺序和正常循环遍历该对象时返回的顺序一致

　　**语法**：

>Object.keys(obj)

　　**参数**：

　　要返回其枚举自身属性的对象

　　**返回值**：

　　一个表示给定对象的所有可枚举属性的字符串数组

------

### Object.getOwnPropertyNames()

　　`Object.getOwnPropertyNames()` 方法返回一个由指定对象的所有自身属性的属性名（包括不可枚举属性但不包括Symbol值作为名称的属性）组成的数组

　　**语法**：

>Object.getOwnPropertyNames(obj)

　　**参数**：

　　`obj` — 一个对象，其自身的可枚举和不可枚举属性的名称被返回

　　**返回值**：

　　在给定对象上找到的自身属性对应的字符串数组, 数组中枚举属性的顺序与通过 `for...in` 循环（或 `Object.keys`）迭代该对象属性时一致

　　只获取不可枚举的属性

```
var obj = {
    a: 11,
    b: 23
}

Object.defineProperty(obj, 'c', {
    value: 45
})
var target = obj;
var enum_and_nonenum = Object.getOwnPropertyNames(target);
var enum_only = Object.keys(target);
var nonenum_only = enum_and_nonenum.filter(function(key){
    var indexInEnum = enum_only.indexOf(key)
    if(indexInEnum == -1) {
        return true
    } else {
        return false
    }
})

console.log(nonenum_only);
```

------

### Object.freeze()

　　`Object.freeze()` 方法可以冻结一个对象

　　**语法**：

>Object.freeze(obj)

　　**参数**：

　　`obj` — 要被冻结的对象

　　**返回值**：

　　被冻结的对象

被冻结对象自身的所有属性都不可能以任何方式被修改。任何修改尝试都会失败。数据属性的值不可更改，访问器属性（有getter和setter）也同样（但由于是函数调用，给人的错觉是还是可以修改这个属性）。如果一个属性的值是个对象，则这个对象中的属性是可以修改的，除非它也是个冻结对象。数组作为一种对象，被冻结，其元素不能被修改。没有数组元素可以被添加或移除

------

### Object.isFrozen()

　　`Object.isFrozen()`方法判断一个对象是否被冻结

　　**语法**：
>Object.isFrozen(obj)

　　**参数**：

　　`obj` —— 被检测的对象

　　**返回值**：

　　表示给定对象是否被冻结的Boolean

　　如果使用`Object.defineProperty`将对象变成不可扩展，需将`writable`,`configurable`都设置成false。使用`Object.freeze`是冻结一个对象最方便的方法

---------

### Object.preventExtensions()

　　Object.preventExtensions()方法让一个对象变的不可扩展，也就是永远不能再添加新的属性

　　**语法**：

>Object.preventExtensions(obj)

　　**参数**：

　　`obj` — 将要变得不可扩展的对象

　　**返回值**：

　　已经不可扩展的对象

　　<u>`Object.preventExtensions()`仅阻止添加自身的属性。但其对象类型的原型依然可以添加新的属性</u>

---------

### Object.isExtensible()

　　`Object.isExtensible()` 方法判断一个对象是否是可扩展的（是否可以在它上面添加新的属性）

　　**语法**：

>Object.isExtensible(obj)

　　**参数**：

　　`obj` — 需要检测的对象

　　**返回值**：

　　表示给定对象是否可扩展的一个Boolean


　　默认情况下，对象是可扩展的：即可以为他们添加新的属性。以及它们的 __proto__ 属性可以被更改。`Object.preventExtensions`，`Object.seal` 或 `Object.freeze` 方法都可以标记一个对象为不可扩展（non-extensible）

---------

### Object.seal()

　　`Object.seal()` 方法判断一个对象是否是可扩展的（是否可以在它上面添加新的属性）

　　**语法**：

>Object.seal(obj)

　　**参数**：

　　`obj` — 将要被密封的对象

　　**返回值**：

　　被密封的对象

　　通常，一个对象是可扩展的（可以添加新的属性）。密封一个对象会让这个对象变的不能添加新属性，且所有已有属性会变的不可配置。属性不可配置的效果就是属性变的不可删除，以及一个数据属性不能被重新定义成为访问器属性，或者反之。但属性的值仍然可以修改。尝试删除一个密封对象的属性或者将某个密封对象的属性从数据属性转换成访问器属性，结果会静默失败或抛出TypeError

---------

### Object.isSealed()

　　`Object.isSealed()` 方法判断一个对象是否被密封

　　**语法**：

>Object.isSealed(obj)

　　**参数**：

　　`obj` — 要被检查的对象

　　**返回值**：

　　表示给定对象是否被密封的一个Boolean

## 资料

 - [Object.defineProperty()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty)
 - [Object.defineProperty()](https://segmentfault.com/a/1190000019446677)
 - [Object.freeze()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/freeze)
 - [Object.isFrozen()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/isFrozen)
 - [Object.preventExtensions()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/preventExtensions)
 - [Object.seal()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/seal)
