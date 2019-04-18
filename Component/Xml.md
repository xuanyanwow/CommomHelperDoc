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

/* 第二个参数是要不要加头部<?xml version="1.0" encoding="UTF-8"?>  默认为true*/
$res = Xml::getInstance()->arrayToXml($array, true); 
echo $res;
```