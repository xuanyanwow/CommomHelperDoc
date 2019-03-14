
获取ApiTicket JSSDK等场景需要使用
## setAppid
## setToken
## setEcho
## getToken
```php
$ApiTicket = ApiTicket::getInstance();
$ApiTicket->setAppid('wxa50xx5919');
$ApiTicket->setToken($token);
$ApiTicket->setEcho(false);

$ticket = $ApiTicket->getTicket();
```