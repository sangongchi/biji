## Dart语言（强类型语言）

### 1. 变量声明

> 1. var 声明，它可以接受任何类型的变量，但是Dart中的var 变量一旦赋值，类型会确定，且不能再改变其类型，
>
>  ```dart
>  var t;
>  t = "hi world";
>  // 下面代码在dart中会报错，因为变量t的类型已经确定为String，
>  // 类型一旦确定后则不能再更改其类型。
>  t = 1000;
>  ```
>
>  当用`var`声明一个变量后，Dart在编译时会根据第一次赋值数据的类型来推断其类型，编译结束后其类型就已经被确定，而JavaScript是纯粹的弱类型脚本语言，var只是变量的声明方式而已。
>
> 2. dynamic 和Object
>
>  `dynamic`与`var`一样都是关键词,声明的变量可以赋值任意对象。 而`dynamic`与`Object`相同之处在于,他们声明的变量可以在后期改变赋值类型。
>
> 3. final 和const  修饰符**(定义常量 赋值之后不可修改)**
>
>     - const 一开始就得赋值
>     - final  可以开始不赋值，但只能赋值一次，
>
>     ```dart
>     main(){
>         final a=new DateTime.now();
>         print(a);
>         
>         const a=new DateTime.now(); //会报错
>     }
>     ```
>
>     

### 2. Dart 入口方法介绍

> 1. dart 中所有要执行的方法都必需放在  main方法中
>
> 2. ```dart
>     main(){
>         //所有要执行的方法
>     }
>     
>     void main(){
>         
>     }
>     //添加了void 表示该方法没有返回值
>     ```
>
> 3.   



