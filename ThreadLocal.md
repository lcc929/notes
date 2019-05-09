set(T t)执行流程
1. 取得当前线程。
2. 取得当前线程中的ThreadLocalMap，判断当前线程中是否有设置map，如果有进入第3步，否则进入第4步。
3. 如果有map，直接对当前的ThreadLocal对象作为key进行hash，计算出一个下标，
根据此下标找到数组中对应下标的值，进行判断，如果为空进入第5步，如果不为空进入第6步。
4. 在线程中初始化一个ThreadLocalMap，ThreadLocalMap本身只维护一个真实存值数据结构Entry的数组。
通过对ThreadLocal对象进行hash得到一个下标，然后构建一个Entry，根据下标放入Entry数组中，到此set(T t)完成。
5. 构建一个Entry，根据hash得到的下标，放入ThreadLocalMap的数组对应的下标中，执行清理和扩容检查后，set(T t)完成。
6. 取得根据下标值获得的Entry，根据软引用的key拿到对应的ThreadLocal的对象，与当前ThreadLocal对象做比对，
如果相等说明是对同一个ThreadLocal进行setValue，直接用新的value覆盖旧的value。
如果不相等说明当前线程出现了多个ThreadLocal的hash冲突，解决hash冲突（这部分源码没有看）后构建Entry，完成set(T t)。