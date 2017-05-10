# Ajax跨域请求简单解决方法
ajax跨域访问是一个老问题了，解决方法很多，比较常用的是JSONP方法。  
JSONP方法是一种非官方方法，而且这种方法只支持GET方式，不如POST方式安全。  

即使使用jQuery的jsonp方法，type设为POST，也会自动变为GET。  

### 官方问题说明：
> “script”: Evaluates the response as JavaScript and returns it as plain text. Disables caching by appending a query string parameter, “_=[TIMESTAMP]“, to the URL unless the cache option is set to true.Note: This will turn POSTs into GETs for remote-domain requests.

---
### 设置Access-Control-Allow-Origin来实现跨域访问比较简单  
例如：客户端的域名是www.client.com,而请求的域名是www.server.com  
如果直接使用ajax访问，会有以下错误  
> XMLHttpRequest cannot load http://www.server.com/server.PHP. No 'Access-Control-Allow-Origin' header is present on the requested resource.Origin 'http://www.client.com' is therefore not allowed access.

### 在被请求的Response header中加入
```
// 指定允许其他域名访问  
header('Access-Control-Allow-Origin:*');  
// 响应类型  
header('Access-Control-Allow-Methods:POST');  
// 响应头设置  
header('Access-Control-Allow-Headers:x-requested-with,content-type');  
```
就可以实现ajax POST跨域访问了