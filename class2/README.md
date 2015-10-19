js 源码：系统对象也是基于原型的程序
例如：

    function Array(){
        this.length = 0;
    }
    Array.prototype.pop = function(){}
    Array.prototype.push = function(){}

不要对系统对象进行操作

    var arr = [1,2,3];
    Array.prototype.push = function(){}
    arr.push(4,5,6);//arr 就push不了了

尽量不去修改或者添减系统对象下面的方法和属性