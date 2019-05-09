#双重检查的两种写法

问题一：  
为什么说双重检查的两种写法，A的代码比B的代码效率要高?  

A:  
用局部变量来接收被volatile声明的全局变量
```
pulbic class LccTest {
    private volatile Map<String, String> testMap;
    
    void test(String a, String b) {
        Map<String, String> temporaryMap = testMap;
        if (temporaryMap == null) {
            synchronized (this) {
                temporaryMap = testMap;
                if (temporaryMap == null) {
                    temporaryMap = new HashMap<>();
                    testMap = temporaryMap;
                }
            }
        }
        temporaryMap.put(a, b);
    }
    
    //skipped
}
```

B:  
直接用volatile声明的变量来进行双重检查
```
pulbic class LccTest {
    private volatile Map<String, String> testMap;
    
    void test(String a, String b) {
        if (testMap == null) {
            synchronized (this) {
                if (testMap == null) {
                    testMap = new HashMap<>();
                }
            }
        }
        testMap.put(a, b);
    }
    
    //skipped
}
```


问题二：  
七个问题:
1. Q: helloWordsMap 变量为什么使用 volatile 限定词？  
A: 保证共享变量在线程间的可见性
2. Q: 为什么要 temporaryMap 变量？  
A: 减少volatile变量的拷贝开销。
3. Q: temporaryMap 变量为什么要两次设置为 helloWordsMap？  
A: 第一次是为了初始化temporaryMap，第二次是为了刷新局部变量。
4. Q: 为什么要检查两次 temporaryMap 的值不等于空？  
A: 保证防止重复初始化，如果有线程在synchronized前被阻塞，如果不检查非空，则会重复初始化。
5. Q: synchronized 为什么用在第一次检查之后？  
A: 不是每次都需要初始化，减少锁范围，减少开销
6. Q: 为什么使用 ConcurrentHashMap 而不是 HashMap？  
A: 全局变量应该使用线程安全的容器。
7. Q: 为什么使用 temporaryMap.put() 而不是 helloWordsMap.put()？  
A: 减少volatile变量的拷贝开销。
