将数组转为xml

数组可以是多维，递归实现转换

## 快速预览
```php
<?php
use Siam\Xml;
$array = [
    ['HEAD'] => [
        'appid' => '1',
        'se'    => '2'    
    ],
    ['BODY'] => '123'
];

$res = Xml::getInstance()->arrayToXml($array);
echo $res;
```