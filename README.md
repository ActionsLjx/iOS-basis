# Readme
iOS基础常见面试题

## 题目：

###1. strong,weak,retain,assign,copy nomatic 等的区别
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

###3. 深拷贝浅拷贝的区别,哪些属于深拷贝,哪些属于浅拷贝
###4. viewController,view的生命周期是什么
###5. KVC,KVO的底层的实现原理是什么
###6. 冒泡排序
###7. delegate,block有什么区别
###8. Storyboard,Xib的区别
###9. iOS本地化存储的方法有几种,有什么区别
###10. 造成内存泄漏的原因有什么
###11. 造成程序Crash的可能性有哪些
###12. include,import,@class三者区别
###13. denfine,typefil的区别
###14. 造成tableview滑动卡顿的原因
###15. TCPIP几次握手
###16. static 的作用



