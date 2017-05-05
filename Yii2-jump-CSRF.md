# mdmsoft插件跳过SCRF验证
在项目过程中，有时候需要用YII2的框架提供一些公共的接口，但是YII2的backend里面的controller都有路由验证，这个时候，只有跳过路由验证才能正常访问接口。

### 第一步：
vendor/mdmsoft/yii2-admin/components/Configs.php
```
/**
* @var boolean If true then AccessControl only check if route are registered.
*/
public $onlyRegisteredRoute = true;
```

### 第二步：
这样修改以后，MDM将只校验被添加到权限系统的URL，而没有添加的URL就不会进行校验了  
在后台管理的权限管理中，将不需要验证的URL从注册表中删掉。

### 第三部：
控制器里面关闭SCRF验证
```
//关闭POST请求的CSRF验证
public $enableCsrfValidation = false;
```

##### 分析
这个参数配置是如何发挥作用的，yii2-admin/components/Helper.php中的代码如下：
```
public static function checkRoute($route, $params = [], $user = null)
{
    $config = Configs::instance();
    $r = static::normalizeRoute($route);
    if ($config->onlyRegisteredRoute && !isset(static::getRegisteredRoutes()[$r])) {
        return true;
}

```