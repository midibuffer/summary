输入一个例子

	[false, true, undefined, null, NaN, 0, 1, {}, {}, 'a', 'a', NaN].uniq()

需要输出

	[false, true, undefined, null, NaN, 0, 1, {}, {}, 'a']

分析

	题目要求给Array添加方法，所以我们需要用到prototype，数组去重本身算法不是很难，但是在Javascript中很多人会忽视NaN的存在，因为JS中NaN != NaN

在不考虑NaN的情况下我是使用indexOf判断是不是-1 或者是inCludes是不是false,再添加到数组中去。 

#ES5的实现如下：

    Array.prototype.uniq = function () {
    　　var arr = [];
    　　var flag = true;
    　　this.forEach(function(item) {
    　　　　// 排除 NaN (重要！！！)
    　　　　if (item != item) {
    　　　　　　flag && arr.indexOf(item) === -1 ? arr.push(item) : '';
    　　　　　　flag = false;
    　　　　} else {
    　　　　　　arr.indexOf(item) === -1 ? arr.push(item) : ''
    　　　　}
    　　});
    　　return arr;
    }
上边的if语句就是为了判断是不是NaN,给NaN一个标识，只要进来一次NaN就把他置为false，之后的话NaN再进入判断就不会再添加进去。这是真的精妙~
之后调用uniq方法，如
[false, true, undefined, null, NaN, 0, 1, {}, {}, 'a', 'a', NaN].uniq()
这里的话自己测试一下吧！
 
#ES6的实现如下：
ES6新增了Set对象，也就是我们所说的“集合”，它类似于数组，但是成员的值都是唯一的，没有重复的值。所以可以方便去重。
Set本身是一个构造函数，用来生成Set数据结构。
    Array.prototype.uniq = function() {
    　　return Array.from(new Set(this));
    }
代码中Array.from把Set结构换成数组，最最重要的是代码只需要一行就能实现
如果要写的优雅一点的话，可以使用ES6的扩展运算符
    Array.prototype.uniq = function() {
    　　return [...new Set(this)];
    }
 
 
本文转载出处 https://microzz.com/2017/04/01/array-uniq/ 
