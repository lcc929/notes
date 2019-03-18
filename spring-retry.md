# Spring-Retry 重试框架

基于异常实现的重试框架

### 接口设计：
1. `RetryOperations`：重试操作，定义了几种执行重试的方式
2. `RetryCallback`：重试回调
3. `RetryContext`：重试上下文
4. `RecoveryCallback`：回调恢复机制（重试达到上限时执行的回调，以保证业务恢复）
5. `RetryState`：重试状态，分为有状态重试和无状态重试
6. `RetryPolicy`：重试策略（重试操作执行的策略）

### 重试策略：
* `NeverRetryPolicy`：不重试策略
* `AlwaysRetryPolicy`：无限重试，直至成功策略
* `SimpleRetryPolicy`：按次数和异常类型进行匹配的策略
* `TimeoutRetryPolicy`：超时放弃策略
* `ExceptionClassifierRetryPolicy`：根据异常类型自定义策略的策略





### 声明式重试









### 注意点
1. 声明式调用是采用代理方式将重试模板由Spring AOP织入，如果被声明为`@Retryable`的方法是通过内部调用，proxy对象就不会生成，导致切面失效无法重试。
2. 重试如果不设置超时或次数上限，或其他原因造成大量重试，对可能引起平台降级限流，另一方面抛出异常时会记录堆栈开销比较重。

### 对现有代码的调整
- 使用创建template方式重试，在mall
- 使用声明式
