# JWT(Json Web Token)
### OMS3.0中的校验机制：
1. token生成：  
登陆成功，生成一个token返回，之后请求都会携带该token
2. token校验：  
目前而言，不会对token进行校验，生成后也不保存token，每次只对携带的token进行解析，只要存在token就能登陆成功。