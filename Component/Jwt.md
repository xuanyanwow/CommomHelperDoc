### Jwt（JSON Web Tokens）

JWT 是一个开放标准(RFC 7519)，它定义了一种用于简洁，自包含的用于通信双方之间以 JSON 对象的形式安全传递信息的方法。

一般在前后端分离项目中使用

```php
<?php
require "../vendor/autoload.php";

$jwt = \Siam\JWT::getInstance();
// 生成jwt  在登录成功时返回
$jwt = $jwt->setIss('SiamTest')
->setSecretKey('keykeykey')
->setSub('Payment')
->setWith(['username' => 'siam_name'])  // 附带数据 前端也可以解析出来的
->make();

echo $jwt;

$data = \Siam\JWT::getInstance()->setSecretKey('keykeykey')
->decode('eyJhbGciOiJBRVMiLCJ0eXAiOiJKV1QifQ_b__b_.eyJpc3MiOiJTaWFtVGVzdCIsImV4cCI6MTU1NDg2OTQ2OCwic3ViIjoiUGF5bWVudCIsImlhdCI6MTU1NDg2MjI2OCwibmJmIjoxNTU0ODYyMjY4LCJ1c2VybmFtZSI6InNpYW1fbmFtZSJ9.UHdYbFJHOGw5Qy8zMWpPVmtEdEpEb1FtbmpGK2Y0MVQrbDNDOU9ud0RzNWszVHZlVHdZcVBSbDVMZlVaWFd5ZnVIajIxSUgzR2crRTEvdzBzaDVBajY1N1lRN2FVQkFRVStnZXdGUVo3RDJKWlRxUko0ZkdLVEJUY1hlZ094TytQYzYwVll3QVVxUDlOYjFVMm5ueThEcC9jWEhBMjZKVExCa3REaTZrV0lROEY3YVRrbVF3ZnVKMWd6NlZzUC9keVFaa29DeE9QV2xhaVA5aVZERVhCR0NIdzRKU1cwUHo1VG9BUjA4ZkFPRk80ekFnZW5EenRNVHlQMHVheDl5cQ_b__b_');
var_dump($data);  // 解密  判断$data是否为数组 如果不是数组则可能是token时效 参数错误等 返回字符串
```

#### 前端解析数据
```
get: function(str){
    var token = layui.data(setter.tableName)[setter.request.tokenName];
    if (token===undefined){
        return null;
    }
    var tokenArr = token.split(".");
    var tokenData = tokenArr[1];
    tokenData = tokenData.replace(/_b_/g,"=");
    tokenData = tokenData.replace(/_a_/g,"+");
    tokenData = tokenData.replace(/_/g,"/");
    var json =window.atob(tokenData);
    var obj = JSON.parse(json);
    var timestamp = Date.parse(new Date())/1000;

    // 在此之前不可用
    if (obj.nbf !== undefined && obj.nbf > timestamp){
        return 'NOTBEFORE';
    }
    // 是否已经过期
    if (obj.exp !== undefined && obj.exp < timestamp){
        return 'EXP';
    }

    return obj[str];
}
```
