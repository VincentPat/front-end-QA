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


###offsetParent的寻找规则是？
####答案：
布局中设置postion属性(relative、absolute、fixed)的父容器，从最近的父节点开始，一层层向上找，直到HTML的body。
