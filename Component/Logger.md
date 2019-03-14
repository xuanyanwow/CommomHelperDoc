## 快速预览
```php

$log = \Siam\Logger::getInstance();
$res = $log->log("测试log");
var_dump($res);

# 级别
$res = $log->log("测试log", 'notice');
var_dump($res);
```

```php
# log储存路径 依赖于Di注入
Di::getInstance()->set('CONFIG_LOG_DIR', "./log/");
$lognew = \Siam\Logger::getInstance();
$res    = $lognew->log("测试log", 'die');
var_dump($res);

# 自定义日志处理器
$log3 = \Siam\Logger::getInstance(new \Siam\Trace\LoggerRedis());
$log3->log('test');
```

## 自定义日志处理器

用户可以自己设置不同方式的log处理者，需要继承`Siam\AbstractInterface\LoggerAbstractInterface`

在包中提供了一个示例类 `\Siam\Trace\LoggerRedis`

```php
<?php
namespace Siam\Trace;

use Siam\AbstractInterface\LoggerAbstractInterface;

class LoggerRedis implements LoggerAbstractInterface
{

    public function log($str, $level = 'debug')
    {
        echo "this is redis logger";
    }
}
```