# Readme
iOS基础常见面试题

## 题目：

### 1. strong,weak,retain,assign,copy nomatic 等的区别
* strong 对象被销毁,但是仍然会在内存中 weak 对象被销毁,也就不会占用内存了
* assign 简单数据赋值,不更改Reference Counting的值
* copy 建立一个索引技术为1的对象,然后释放旧对象
* retain 释放旧对象,将就对象的值赋予输入对象,然后在增加引用计数
* nomatic 非原子性访问，对属性赋值的时候不加锁，多线程并发访问会提高性能。如果不加此属性，则默认是两个访问方法都为原子型事务访问

### 2. map,flatMap,filter,reduce的区别
* map,flatMap 都是对现有数组进行操作,但是flatMap可以讲多个数组合并为同一个数组

    ```
    let array = [[1,2,3],[4,5,6]]
    let arr1 = array.map{$0 + 1}
    arr1 // [[2,3,4],[5,6,7]]
    let arr2 = array.flatMap{ $0 + 1}
    arr2 // [3,4,5,6,7,8]
    ```
*  flitter 过滤，可以对数组中的元素按照某种规则进行一次过滤
    
    ```
    let array = [1,2,3,4,5,6,7,8,9]
    let arr1 = array.flitter{ $0 > 5 }
    arr1 // [6,7,8,9]
    ```
* reduce 对数组元素进行计算

### 3. 深拷贝浅拷贝的区别,哪些属于深拷贝,哪些属于浅拷贝
* 深拷贝是对一个对象的拷贝，浅拷贝是对一个对象地址的拷贝。
* strong修饰的可以理解为浅拷贝，它只是对对象地址的引用，所以修改原对象，
* copy修饰的可以理解为深拷贝，它又另外复制了一份原对象，两者地址不同，所以修改原对象

### 4. viewController,view的生命周期是什么
* viewController
   viewDidload -> viewDidUnload -> viewWillAppear -> ViewWillLayoutSubViews -> ViewDidLayoutSubViews -> viewDidAppear -> ViewwWillDissappear -> ViewDidDisappear
   
### 5. KVC(Key-Value Coding),KVO(Key-Value Observing)是什么,底层的实现原理是什么
* KVC键值编码。它是一种不通过存取方法，而通过属性名称字符串间接访问属性的机制。
* KVO键值观察。它是观察者模式的一种衍生。基本思想是，对目标对象的某属性添加观察，当该属性发生变化时，会自动的通知观察者

### 6. 冒泡排序
```
var arr = [1,5,2,8,3]
for i in 0...arr.count - 1 {
    for j in 0...arr.count - 1 - i {
        if a[j] >a[ j + 1 ] {
            let temp = a[ j + 1 ]
            a[ j + 1 ] = a[ j ]
            a[ j ] = temp
        }
    }
}
```

### 7. delegate,block有什么区别
* delegae 运行成本低, block运行成本高,block出栈需要将使用的数据从栈内存中拷贝到堆内存,对象的话就是计数加1,使用完成或者block置nil才能消除,deleaget只是保存了个别指针对象,直接回调,没有额外消耗
* delegate 让多个方法分成一组,可以多次回调,使用起来更简单
* block的话需要考虑循环引用,delegate相对更加安全

### 8. Storyboard,Xib的区别
* xib更加轻量化 Storyboard更加注重各个界面之间的逻辑
* 在团队开发中使用Xib能够更好地避免冲突

### 9. iOS本地化存储的方法有几种,各有什么特点
* NSCodeing: 能将任何遵守了NSCodeing协议的对象存储到文件中 
* plist属性列表: 仅仅是Foundation框架自带的一些类的存储
* userdefault存储,仅支持简单数据存储
* sqlite 数据库存储: 大型数据,有分类顺序需要查询的数据存储. 

### 10. 造成内存泄漏的原因有什么
* 最常见的就是循环引用造成内存泄漏
* 

### 11. 造成程序Crash的可能性有哪些
### 12. include,import,@class三者区别
### 13. denfine,typefil的区别
### 14. 造成tableview滑动卡顿的原因
### 15. TCPIP几次握手
### 16. static 的作用



