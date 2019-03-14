获取Token 

## setAppid
## setAppsecret
## setEcho
## getToken
```php
<?php
$AccessToken = AccessToken::getInstance();
$AccessToken->setAppid('wxa50xx5919');
$AccessToken->setAppsecret('524ee05efdb2ef7xxx9b7ed189');
$AccessToken->setEcho(false); // 不设置则获取到echo就输出json 并且后续不会再执行

$token = $AccessToken->getToken();
```