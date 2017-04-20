# mdmsoft�������SCRF��֤
����Ŀ�����У���ʱ����Ҫ��YII2�Ŀ���ṩһЩ�����Ľӿڣ�����YII2��backend�����controller����·����֤�����ʱ��ֻ������·����֤�����������ʽӿڡ�

### ��һ����
vendor/mdmsoft/yii2-admin/components/Configs.php
```
/**
* @var boolean If true then AccessControl only check if route are registered.
*/
public $onlyRegisteredRoute = true;
```

### �ڶ�����
�����޸��Ժ�MDM��ֻУ�鱻��ӵ�Ȩ��ϵͳ��URL����û����ӵ�URL�Ͳ������У����  
�ں�̨�����Ȩ�޹����У�������Ҫ��֤��URL��ע�����ɾ����

### ��������
����������ر�SCRF��֤
```
//�ر�POST�����CSRF��֤
public $enableCsrfValidation = false;
```

##### ����
���������������η������õģ�yii2-admin/components/Helper.php�еĴ������£�
```
public static function checkRoute($route, $params = [], $user = null)
{
    $config = Configs::instance();
    $r = static::normalizeRoute($route);
    if ($config->onlyRegisteredRoute && !isset(static::getRegisteredRoutes()[$r])) {
        return true;
}

```