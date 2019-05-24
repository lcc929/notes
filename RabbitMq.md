#踩坑
- guest只能用于localhost登录，远程连接时需要创建一个新用户并授权，否则会报下面的错误。

- 账号密码填错java连接异常：
```
org.springframework.amqp.AmqpAuthenticationException: 
com.rabbitmq.client.AuthenticationFailureException: 
ACCESS_REFUSED - Login was refused using authentication mechanism PLAIN. 
For details see the broker logfile.
```
