Ip组件提供了两个功能：获取客户端Ip、验证Ip

```php
$ipClass = \Siam\Ip::getInstance();

echo $ipClass->getIp();
echo "<br/>";


# 判断获取的ip是否在数组中，支持 * 通配符
$res = $ipClass->checkIp([
    '127.0.0.*',
    '127.0.0.2'
], $ipClass->getIp());

var_dump($res);
```