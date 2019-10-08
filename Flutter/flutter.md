## 学习笔记

### 1. dart初始化

> 1. ```dart
>     //项目的基本写法
>     import 'package:flutter/material.dart';
>         void main(){
>             runApp(Center(
>                 child: Text(
>                 "我是一个文本内容",
>                 textDirection: TextDirection.ltr,
>             ),
>         ));
>     	}
>     
>     //可以将flutter 内容抽离成为一个组件
>     void main(){
>         runAPP(MyApp())
>     }
>     class MyApp extends StatelessWidget{
>     @override
>         Widget build(BuildContext context) {
>             return Center(
>             	child:Text(
>                 	"文本内容"
>                 )
>             )
>         }
>         
>         //项目的大致结构
>     void main(){
>         runAPP(MyApp())
>     }
>     class MyApp extends StatelessWidget{
>     @override
>         Widget build(BuildContext context) {
>             return MaterialApp(   // 一般作为顶层的widget  常用的属性有 
>                 				// ：hone title color theme(主题) routes(路由)
>             	title:"我是一个标题",
>                 home:Scaffold(   // Scaffold 是Material Design 布局结构的基本实现
>                 	appBar:AppBar(
>                     	title:Text('SANGONGCHI')
>                     )
>                 ),
>                 themes:()
>             )
>         }
>         
>     ```
>
> 2. Scaffold 有下面几个主要的属性：
>
>     - appBar - 显示在界面顶部的一个AppBar。
>     - body - 当前界面所显示的主要内容Widget。
>     - drawer - 抽屉菜单控件。
>     - .....