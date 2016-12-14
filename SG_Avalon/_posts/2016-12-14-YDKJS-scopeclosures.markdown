---
layout: post
title: Scope & Closures 
categories: 
    - YDKJS 趟坑记
tags: 
    - javascript
    - YDKJS
thumbnail: /img/space.jpg
cover: /img/space.jpg
prism: true
---

{% highlight js %}

// ------------ fe scope ---------------
var foo = function bar()
    {
        console.log('aepofi');
    }
    // bar();

// ------------ hoisting ignore
// function override ---------------
function foo()
{
    console.log(1);
}
foo(); // 3
var foo = function()
{
    console.log(2);
};
foo(); // 3

function foo()
{
    console.log(3);
}

// ---------- Closure -----------
function foo1()
{
    var a = 3;

    function bar()
    {
        var a = 3;
        console.log(a)
    }
    return bar
}
var a = foo1()

function foo2()
{
    var a = 3;

    function bar()
    {
        var b = 3;
        console.log(a)
    }
    console.log(3);
    return a
}
var a = foo2()

function foo3()
{
    let aa = 3;

    function fooo()
    {
        var b = 3;

        function bar()
        {
            var b = 3;
            console.log(aa)
        }
        return bar
    }
    let a = fooo()
    var b = 4;
    console.log(b);
}
foo3();

// Keng:
var aa = 4

function foo4()
{
    var b = 3;

    function bar()
    {
        var b = 3;
        console.log(aa)
    }
    return bar
}
var a = foo4()
var b = 3

// Immediate Enclosing Scope
function foo5()
{
    var a = 2;
    var bb = 3

    function baz()
    {
        console.log(a); // 2
    }
    bar1(baz);
}

function bar1(fn)
{
    fn(); // look ma, I saw closure!
    var b = 4;
}
foo5();

function foo6()
{
    var a = 2;

    function bar()
    {
        console.log(a); // 2
    }
    bar();
    var b = 4;
    console.log(b)
}
foo6();

function foo7()
{
    var aaa = 2;

    function baaz()
    {
        console.log(aaa); // 2
        aaa = 10;
    }

    function bar(fn)
    {
        fn(); // look ma, I saw closure!
        var b = 4;
    }
    bar(baaz);
    console.log(aaa)
    baaz()
    console.log(aaa)
    var bb = 4;
}
foo7()

function foo8()
{
    var aaa = 2;

    function baaz()
    {
        console.log(aaa); // 2
        aaa = 10;
    }

    function bar()
    {
        baaz(); // look ma, I saw closure!
        var b = 4;
    }
    bar();
    console.log(aaa) // aaa=10 not 2, closure is foo8
    baaz()
    console.log(aaa) // aaa=10
    var bb = 4;
}
foo8()

// Keng: Scope doesn't exist
var aaa10 = 2;
var func10 = (function IIFE()
{
    var b = 4
    var bbb = (function pafeij()
    {
        console.log(aaa10)
    })
    console.log(aaa10)
})
func10();

// --------- setTimeout 在for 循环结束后才执行 ---------
// function waitSeconds(iMilliSeconds) {
//     var counter= 0
//         , start = new Date().getTime()
//         , end = 0;
//     while (counter < iMilliSeconds) {
//         end = new Date().getTime();
//         counter = end - start;
//     }
// }
// for (let i=1; i<=5; i++) {
//      setTimeout( function timer(){
//          console.log( i ); }, 1000 );
//      waitSeconds(1001)
//      console.log('pajeopifaj'+i)
// }
//
// console.log('ajofpewijfopaej')

// --------- 上面循环的 equivalent ---------
// var i = 1
// i++
// setTimeout( function timer(){
//     console.log( i ); }, 1000 );
// i++
// setTimeout( function timer(){
//     console.log( i ); }, 1000 );
// i++
// setTimeout( function timer(){
//     console.log( i ); }, 1000 );
// i++
// setTimeout( function timer(){
//     console.log( i ); }, 1000 );
// i++
// setTimeout( function timer(){
//     console.log( i ); }, 1000 );
//
// console.log('japoweijfopaijwe')

// --------- iife implementation ---------
// for (var i=1; i<=5; i++) {
//     (function iifee(j){
//         setTimeout( function timer(){
//             console.log( j ); }, 1000 );
//         console.log('pajeopifaj'+i)
//     })(i)
// }
// console.log('jpfaoiejfopiaj')
var count = 10
var obj = {
    count:0,
    cool: function(){
        var self = this
        setTimeout(function(){
            self.count++},100)
    }
}
obj.cool()
console.log('jojio'+obj.count)

{% endhighlight %}

