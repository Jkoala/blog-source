## Oauth2 四种授权模式

参考文档：https://github.com/lansinuote/Spring-Oauth2-Toturials

###  授权码模式

1. 请求得到授权码 ttp://127.0.0.1:3001/oauth/authorize?client_id=client1&response_type=token&scope=all&redirect_uri=http://www.baidu.com
2. 通过得到的授权码去获取token http://127.0.0.1:3001/oauth/token?client_id=admin&client_secret=123&grant_type=authorization_code&redirect_uri=http://www.baidu.com&code=YFHlnS
3. 

```json
{
                "client_id", "client1",
                "client_secret", "123123",
                "grant_type", "authorization_code",
                "code", "euCRiL",//这个code是从getCode()方法获取的
                "redirect_uri", "http://www.baidu.com"
        };
```



### 用户密码模式

http://127.0.0.1:3001/oauth/token?client_id=admin&client_secret=123&grant_type=password&username=admin&password=admin

```json
String[] params = new String[]{
                "client_id", "client1",
                "client_secret", "123123",
                "grant_type", "password",
                "username", "admin",
                "password", "admin"
        };
```

### 简单模式

```handlebars
http://127.0.0.1:3001/oauth/authorize?client_id=client1&response_type=token&scope=all&redirect_uri=http://www.baidu.com
```

## 客户端模式

http://127.0.0.1:3001/oauth/token?client_id=admin&client_secret=123&grant_type=client_credentials

```json
String[] params = new String[]{
"client_id", "client1",
"client_secret", "123123",
"grant_type", "client_credentials"
};
```

