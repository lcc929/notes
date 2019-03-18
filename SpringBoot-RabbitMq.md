消息默认为持久化模式代码：
```
RabbitTemplate.convertAndSend() 方法的底层调用中，调用了
RabbitTemplate.convertMessageIfNecessary() ，其中有new MessageProperties();
在MessageProperties类中可以看到:
MessageDeliveryMode DEFAULT_DELIVERY_MODE = MessageDeliveryMode.PERSISTENT；
并且下面有：
private volatile MessageDeliveryMode deliveryMode = DEFAULT_DELIVERY_MODE;
在不改变deliveryMode的情况下默认为MessageDeliveryMode.PERSISTENT，因此可以看出消息是默认持久化的。
```