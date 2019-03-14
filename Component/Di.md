Di注入，解决硬性传递参数变量，解耦，动态获取

## 快速预览
```php
<?php
require "../vendor/autoload.php";
# string
\Siam\Component\Di::getInstance()->set('siam', 'test');

echo \Siam\Component\Di::getInstance()->get('siam');
!> Ide会报提示 可能抛出异常 只有储存的是`类`才可能抛出异常

\Siam\Component\Di::getInstance()->set('siam2', '\Siam\Ip');
try {
    $obj = \Siam\Component\Di::getInstance()->get('siam2');
    var_dump($obj->getIp());
} catch (Throwable $e) {
}

```