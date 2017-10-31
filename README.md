# MyTooL-1-2
Node对象中获取子节点和兄弟节点时的空白节点问题 - 构造函数优化版
```js
/*
    自调函数的特点
    1. 自己调用自己 - 省略了函数的调用代码
    2. 定义的变量、函数、对象、数组等 - 全部都在函数作用域中
 */
(function(global){
    /*
        1. 之前定义的所有函数必须被定义在当前函数作用域中
        2. 这些函数必须可以在全局作用域中被正常使用
     */
    function MyTool(){
        this.firstChild = function(parentNode){
            // 1.正确的子节点；2.空白节点
            var child = parentNode.firstChild;
            // 判断当前是否为空白节点
            if (child.nodeType === 3){
                child = child.nextSibling;
            }
            return child;
        }
    }

    var mytool = new MyTool();
    var fn = MyTool.prototype;

    // 将当前的函数作用域中的对象，提升为全局作用域的
    global.MyTool = mytool;
    global.Fn = fn;
})(window);
```
