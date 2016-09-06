# front-end-interview
前端面试题

###IE和Chrome、FireFox、Safari等在子节点数量上的区别？
例如：
```html
<ul>
    <li>A</li>
    <li>B</li>
    <li>C</li>
</ul>
```
IE中ul的子节点是几个？其他浏览器呢？<br>
另：什么情况下才会一致？
####答案：
IE中3个，其他7个，因为在其他浏览器中，换行之后有空白节点。
```html
<ul>空白节点
    <li>A</li>空白节点
    <li>B</li>空白节点
    <li>C</li>空白节点
</ul>
```
如果都写在同一行的话就一致了。
```html
<ul><li>A</li><li>B</li><li>C</li</ul>
```

---

###想要删除id为test的节点下第一个子元素，代码如下，有何弊端？
```javascript
var test = document.getElementById("test");
test.removeChild(test.childNodes[0]);
```
####答案：
只执行removeChild，是从DOM树中删除节点，但节点还存在于内存中。实际上removeChild方法如果删除成功，本身就会返回被删除节点本身，证明节点数据还存在于内存中。因此应该把节点变量设置成null：
```javascript
var test = document.getElementById("test");
var x = test.removeChild(test.childNodes[0]);
x = null;
```

---

###offsetParent的寻找规则是？
####答案：
布局中设置postion属性(relative、absolute、fixed)的父容器，从最近的父节点开始，一层层向上找，直到HTML的body。

---

###隐式转换中“+”和“-”的区别
####答案：
“+”隐式转换代表字符串拼接，“-”将字符串等转换成数字类型再作运算。

---

###下面各表达式，哪些返回false？
```javascript
1 === 1;
"2" === 2;
null === null;
undefined === undefined;
NaN === NaN;
new Object === new Object;
```
####答案：
表达式2、5、6返回false

---

###下面的num输出什么？为什么？什么是包装对象？
```javascript
var a = "string";
a.num = 3;
console.log(a.num);
```
####答案：
输出undefined，因为a的包装对象在赋值之后就销毁了，因此访问不到。
包装对象是js原始类型，像对象一样访问自身属性时，会自动转化生成的对象。例如我们访问str.length，实际过程如下：
```javascript
var a = "string";
console.log(a.length); // 分解成: 1.a=new String("string"); 2.输出a.length; 3.a = "string";然后创建的String对象被销毁。
```

---

###下面表达式的值分别是什么？
```javascript
typeof 100
typeof undefined
typeof [1, 2]
typeof NaN
typeof null
```
####答案:
"number"、"undefined"、"object"、"number"、"object"

---

###预览本地图片方法？
####答案：
有两种方法：1.使用FileReader;2.使用window.URL.createObjectURL

---

###下面的表达式中，a的值是？
```javascript
var a = (1,2,3);
```
####答案：
a的值是3，逗号运算符会取最后一个表达式的值。

---

###如何使一个对象的属性不可被删除？
####答案：
```javascript
var obj = {};
Object.defineProperty(obj, "x", {
    configurable: false,
    value: 1
});
obj.x; // 1
delete obj.x; // false
obj.x; // 1
```

---

###下面的a、b分别输出什么？
```javascript
function foo() {
    var a = b = 1;
}
foo();
console.log(typeof a);
console.log(typeof b);
```
####答案：
a输出undefined, b输出number。原因是b其实是全局变量，执行顺序为：1.b = 1; 2.var a = b，而函数内定义var a，因此在函数体外无法访问a，因此undefined。

---

###下面两种调用函数方法，哪一种会抛出异常？
```javascript
fd();
function fd() {
    return true;
}

fe();
var fe = function() {
    return true;
}
```
####答案：
第二种会抛出TypeError。第一种为函数声明，会被优先处理，或者叫函数前置，因此调用没有问题；第二种为函数表达式，执行表达式前函数未被定义，因此抛出异常。

---

###为什么with语句不推荐使用？
####答案:
使JS引擎优化变得困难，在执行之前不能确定作用域；可读性差，维护困难；严格模式下被禁用。

---

###列举一下严格模式下的区别？
####答案：
- 不能使用with
- 不允许未声明的变量被赋值
- arguments变为参数的静态副本，例如修改arguments[0] = 100;第一个参数不会变成100
- delete参数、函数名会报错
- delete不可配置的属性报错
- 对象字面量重复属性名报错
- 禁止八进制字面量，如010
- eval，arguments变为关键字，不能作为变量、函数名
- eval独立作用域，并在eval返回时丢弃
- 一般函数调用时（非对象的方法调用，也不是用apply/call/bind等修改this），则this指向null，而非全局对象window
- 使用apply/call时，如传入null或undefined时，this将指向null或undefined，而非全局对象window
- 试图修改不可写属性（writable=false），在不可扩展的对象上添加属性时抛出TypeError，而不是忽略
- arguments.caller，arguments.callee被禁用

---

###下面表达式输出为？
```javascript
!function(a) {
    arguments[0] = 100;
    console.log(a);
}(1);
```
####答案：
输出1，修改arguments不会导致原参数的改变。

---

###如何判断下面代码中obj.z是继承过来的属性？
```javascript
function foo(){};
foo.prototype.z = 3;
var obj = new foo();
obj.z; // 3
```
####答案：
'z' in obj;返回true，证明obj自身或原型链上有z这个属性；obj.hasOwnProperty('z');返回false，证明obj自身没有z这个属性。因此得出obj.z是继承过来的属性。

---

###列举对象的属性标签？各标签的意义又是什么？
####答案：
对象的属性标签有：writable（可写）,enumerable（可枚举）,configurable（可配置）。


---

###如何禁止对象增加属性？
####答案：
```javascript
var obj = {x:1};
Object.preventExtensions(obj);
Object.isExtensible(obj); // false
```

---

###如何禁止对象进行配置？
####答案：
```javascript
var obj = {x:1};
Object.seal(obj);
Object.isSealed(obj); // true
```

---

###如何禁止对象进行任何修改？
####答案：
```javascript
var obj = {x:1};
Object.freeze(obj);
Object.isFrozen(obj); // true
```

---

###说明以下ES5支持的各个数组方法的含义及传入参数代表什么：forEach,map,filter,every,some,reduce,reduceRight
####答案：
- forEach 遍历数组，参数：1.值;2.索引;3.数组本身
- map 遍历数组，参数：1.值
- filter 过滤数组，返回true的加入到返回的新数组中，参数：1.值;2.索引
- every 每一个元素都符合条件，则返回true，参数：1.值
- some 存在符合条件的元素，则返回true，参数：1.值
- reduce 元素两两进行遍历，并执行计算，最终返回计算结果，参数：1.第一个元素（或之前计算的结果）;2.第二个元素
- reduceRight 元素从右到左两两进行，并执行计算，最终返回计算结果，参数：1.第一个元素（或之前计算的结果）;2.第二个元素

---

###函数方法apply和call的区别？
####答案：
apply方法的参数以数组形式传入，call方法的参数则逐个传入

---

