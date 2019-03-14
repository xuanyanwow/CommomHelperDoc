## 快速预览
```php
<?php
require "../vendor/autoload.php";

$cryption = \Siam\Cryption::getInstance();

# 每次加密的结果都不一样 可以设置过期时间 300s
$res = $cryption->encode("My name is siam", "siam", 300);
echo $res;

echo "<br/>\n";

# 解码 有设置过期时间，过期之后解码会返回失败
$deRes = $cryption->decode("7c80mR4b0tRG4fNB86pwJfDNz8ZLNzTZqfLYTpiO2w6liPyY5qWN2vD4Udc", "siam");
echo $deRes;
```