---
layout: post
title: This & Object
categories: 
    - YDKJS 趟坑记
tags: 
    - javascript
    - YDKJS
    - sticky
thumbnail: /img/background/rolling-waves.jpg
cover: /img/background/rolling-waves.jpg
prism: true
---
{% highlight javascript %}
// // Keng: undefined 可以进行数值类型操作 并返回 NaN
// // var a=1;
// // var b=undefined;
// // var c=b+0;
//
// // ch1 this
// // function foo1() {
// //     var a = 2;
// //     this.bar1(); // TypeError: Cannot read property 'a' of undefined
// //                 // undefined (use strict mode)
// // }
// // function bar1() {
// //     console.log( this.a );// undefined (none strict mode)
// // }
// // foo1();
// //
// // function foo2() {
// //     var a = 2;
// //     bar2();
// // }
// // function bar2() {
// //     console.log( this.a ); // undefined
// // }
// // foo2(); //undefined
//
// // new 新生成一个 instance
// // function foo3(something,flag)
// // {
// //     if(flag === true){
// //         this.a = something;
// //     }
// // }
// // var obj3 = {
// //     foo: foo3,
// // }
// // obj3.foo(3,true)
// //
// // var bar3 = new obj3.foo(4,false)
// // console.log('fapowiejf'+obj3.a); // 3
// // console.log('fapowi'+bar3.a); // undefined
// //
// // // 只有link prototype，没有内存拷贝
// // function foo4(something,flag)
// // {
// //     if(flag === true){
// //         this.a = something;
// //     }
// // }
// // var obj4 = {
// //     foo: foo4,
// //     a:3
// // }
// // obj4.foo(3,true)
// //
// // var bar4 = new obj4.foo(4,false)
// // console.log('fapowiejf'+obj4.a); // 4
// // console.log('fapowi'+bar4.a); // undefined
//
//
// // Keng: 函数体只在函数被调用时才执行，函数名在编译时就被分配（hoisting)
// // function test()
// // {
// //     function foo5(fn)
// //     {
// //         console.log('apoejfipaoj foo5' + fn.a); // undefined 2 2
// //     }
// //
// //     function bar5()
// //     {
// //         foo5(obj)
// //     }
// //     bar5() // 报错：65 TypeError: undefined babeljs翻译成 let->var
// //     let obj = {
// //         a: 2
// //     }
// //     bar5() // 不报错：function 在 run 的时候才执行函数体
// //     // http://javascript.info/tutorial/initialization
// // }
// // test()
//
// // Keng: Compiler: var 允许函数、变量重名；let 报错
// // function test()
// // {
// // }
// // test()
// // var test = 234 // 不报错
// // let test = 234 // 报错
//
// // Explicit Binding
// function foo6()
// {
//     console.log('ajopefijapjfi foo6: ' + this.a);
// }
//
// var obj6 = {
//     a: 2
// }
//
// foo6.call(obj6)
//
// // Hard Binding
// function foo7()
// {
//     console.log('ajopefijapjfi foo7: ' + this.a);
// }
//
// var obj7 = {
//     a: 2
// }
//
// function bar7()
// {
//     foo7.call(obj7)
// }
//
// bar7()
//
// // helper
// function foo8(something)
// {
//     console.log(something + this.a);
// }
//
// var obj8 = {
//     a: 2
// }
//
// // 先确定输入输出、再写函数体，应用逻辑学迭代
// function bind(obj, fn)
// {
//     function binded()
//     {
//         fn.apply(obj, arguments)
//     }
//     return binded
// }
//
// let b_foo8 = bind(obj8, foo8)
// b_foo8('jfpoaiejfopaji foo8: ')
// let bb_foo8 = foo8.bind(obj8)
// bb_foo8('jafopeifjapowefij inner foo8: ')
//
// // 理解 new binding; hard binding
// function foo9(something, b)
// {
//     this.a = something
// }
// var obj9 = {
//     a: 2
// }
//
// function bind(obj, fn)
// {
//     function binded()
//     {
//         fn.apply(obj, arguments)
//     }
//     return binded
// }
// let bb_foo9 = bind(obj9, foo9)
// let nb_foo9 = new bb_foo9(45)
//
// console.log(obj9.a) // 45
// console.log(nb_foo9.a) // undefined
//
// // Keng: new binding 优先级在 explicit binding 下不一定
// // new binding 不能overide closure 形式的 hard binding
// // new binding 的优先级高过(overide) bind()
// function foo(p1, p2)
// {
//     this.val = p1 + p2;
// }
// // using `null` here because we don't care about
// // the `this` hard-binding in this scenario, and
// // it will be overridden by the `new` call anyway!
// var bar = foo.bind(null, "p1");
// var baz = new bar("p2");
// baz.val; // p1p2
//
// var a
//
// console.log(a = 3);
//
var a = 2;
function foo()
{
    console.log(this.a);
}
(function()
{
    "use strict";
    foo(); // 2
})();
{% endhighlight %}
