---
title: "Block原理"
date: 2019-05-07T12:35:29+08:00
draft: false
---  

# Block原理


1. block 里的ptr是怎么区分函数类型的？   
	函数指针自己能区分？怎么区分？ 

2. block里的值都是值传递，\__block才能是引用传递？   
	auto:  
	* 值传递， 普通局部变量  
	* 因为局部变量内存随时可能被回收，无法访问  
	
	static: 指针传递， 那\__block是啥原理？  
	全局变量: 不捕获，用的时候直接去取

3. NSBlock <-- NSObject   
   * globalBlock（少用，也少问） **stackBlock  mallocBlock** 
   * 只要没有访问 auto(局部)变量，都是 globalBlock，如果访问了，就是 stackBlock.  
     1. 那 mallocBlock 是啥时候访问的？
   * **[stackBlock copy] --> mallocBlock** （copy方法做了什么？对引用计数有什么影响？）  
   	    [globalBlock copy] --> globalBlock (不重要)  
   	    [mallocBlock copy] --> mallocBlock (不重要)

4. [Block copy] 何时由 ARC 自动调用？  
   * **block 作为返回值**  
   * **将block赋值给__strong指针时**  
   * cocoa api 中 usingBlock 方法（eg. NSArray遍历）
   * GCD Api 方法   dispatch\_once dispatch\_after
