## 问题
i. 为什么说双重检查的两种写法，A的代码比B的代码效率要高?  

ii. 七个问题：  
   1. helloWordsMap 变量为什么使用 volatile 限定词？
   2. 为什么要 temporaryMap 变量？
   3. temporaryMap 变量为什么要两次设置为 helloWordsMap？
   4. 为什么要检查两次 temporaryMap 的值不等于空？
   5. synchronized 为什么用在第一次检查之后？
   6. 为什么使用 ConcurrentHashMap 而不是 HashMap？
   7. 为什么使用 temporaryMap.put() 而不是 helloWordsMap.put()？  

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
