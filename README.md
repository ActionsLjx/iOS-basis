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
* 在xib中控件与.m /.h文件的引用关系未取消 但是控件已经移除的时候.
* 代理在一般情况下，需要使用weak修饰。如果你这个VC需要外部传某个delegate进来，通过delegate+protocol的方式传参数给其他对象，那么这个delegate一定不要强引用，尽量使用weak修饰，否则你的VC会持续持有这个delegate，直到代理自身被释放。
* ViewController中Block
* ViewController中存在NSTimer
* more ... 

### 11. 造成程序Crash的可能性有哪些
1. 短时间内内存暴涨
2. 内存泄漏 
3. setObjectForKey key不能为nil，object不能为nil 
4. setValueForKey key不能为nil，value可以为nil 
5. dic [key] = value; 键不能为无，值可以为无
6. 数组超出范围
7. 日期格式化不正确
8. 索引超出范围
9. kvo  志愿没有移除监听，或者国际志愿者组织注册多次监听,移除移除的关键和注册的关键不一致，或者移除多次,确保注册一次要移除一次，不要重复注册，不要重复移除

### 12. include,import,@class三者区别
* include是C中用来引用文件的关键字
* import是OC中用来代替include的关键字,使用import可以保证同一个文件只被引用一次,避免了include的重复引用问题
* @class只是告诉编译器,存在这样一个类,而并不会告诉编译器这个类里面有什么东西

### 13. define,typedef、enum、const的区别
* define 文本替换
* typedef 给类型起别名（给已知的类型起别名）。常用于简化复杂类型，变量类型意义化等。
* (注意)typedef是类型替换，直接参与编译，而define只是简单的文本替换。
* 枚举（Enum）是C语言中的一种基本数据类型,是一个"被命名的整型常量"的集合,他不参与内存的占用和释放,在开发中使用枚举目的是为了增加程序的可读性
* const 基本数据类型,一般用来定义基本数据常量

### 14. 移位运算符
左移运算符	<<	0011 -> 0110
右移运算符	>>	0110 -> 0011
或运算符	︳	1000 | 0001 =1001
与运算符	&	1001 & 1000 = 1000

### 15. 造成tableview滑动卡顿的原因(多数情况)
* 没有使用重用
* cell多次重新布局
* 没有提前计算cell高度
* 加载过多网络图片

### 16. TCPIP几次握手
三次握手
### 17. static 的作用
静态变量和静态方法
可以通过类名.变量名直接引用，而不需要new出一个类来.
静态变量和非静态变量的区别是：静态变量被所有的对象所共享，在内存中只有一个副本，它当且仅当在类初次加载时会被初始化。而非静态变量是对象所拥有的，在创建对象的时候被初始化，存在多个副本，各个对象拥有的副本互不影响。
### 18. a++ 与 ++a 的区别

```
int a=0
printf("%d",a++); //输出0,执行完后a=1
int a=0
printf("%d",++a);//输出1，执行完后a=1
```
### 19. 如何外部访问类的私有属性
通过KVC.runtime机制

### 20. 写一个单例

```
//OC
static Singleton * _instance = nil;
+(instancetype) sharedInstance{
          static dispatch_once_t onceToken;
          dispatch_once(&onceToken, ^{
          _instance= [[self alloc] init];
         });
        return _instance;
}

```
### 21. 斐波那契数列(1、1、2、3、5、8、13、21...) 计算第500位  

```
swift 
var f1 = 1
var f2 = 1
var c = 1 
for i in 3...500 {
    c = f2 
    f2 = f1 + f2
    f1 = f2
}
print(f2)
```

### 22. 为什么微信要自己写浏览器内核而不用WKWebview.

### 23. swift 与 oc 有什么区别
* oc 是面向对象编程
* swift是面向协议编程
* (rxswift是响应式编程)




