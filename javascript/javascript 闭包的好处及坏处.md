javascript 闭包的好处及坏处
原创 2015年01月23日 14:15:46 标签：闭包 /javascript /js /内存泄露 10464
#   闭包javascript 是最强大的特征之一，它允许函数访问局部作用域之外的函数。

创建闭包的常见方式：就是在一个函数里创建另一个函数
            
[javascript] view plain copy
function  fun(){  
                 return function{  
                    alert("hello");  
                          }  
                 }  

闭包的好处有：
1.缓存
2.面向对象中的对象
3.实现封装，防止变量跑到外层作用域中，发生命名冲突
4.匿名自执行函数，匿名自执行函数可以减小内存消耗

以上四条详见（http://blog.csdn.net/sunlylorn/article/details/6534610）
闭包的坏处：
1.内存消耗
 通常来说，函数的活动对象会随着执行期上下文一起销毁，但是，由于闭包引用另外一个函数的活动对象，因此这个活动对象无法被销毁，这意味着，闭包比一般的函数需要更多的内存消耗。尤其在IE浏览器中需要关注。由于IE使用非原生javascript对象实现DOM对象，因此闭包会导致内存泄露问题，例如：
 
[javascript] view plain copy
function A(){  
      var a=document.createElement("div")，//  
            msg="Hello";  
       a.onclick=function(){  
          alert(msg);  
          }  
   }  
 A();  


以上的闭包会在IE下导致内存泄露，假设A()执行时创建的作用域对象ScopeA，ScopeA引用了DOM对象a,DOM对象a
引用了function(aleert(msg))，函数function(alert(msg))引用了ScopeA，这是一个循环引用，在IE会导致内存泄露。

2.性能问题

使用闭包时，会涉及到跨作用域访问，每次访问都会导致性能损失。
因此在脚本中，最好小心使用闭包，它同时会涉及到内存和速度问题。不过我们可以通过把跨作用域变量存储在局部变量中，然后直接访问局部变量，来减轻对执行速度的影响。

（PS：以上参考《高性能JavaScript》）
