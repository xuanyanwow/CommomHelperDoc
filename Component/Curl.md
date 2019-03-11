
Curl组件可以快速简洁地发起网络请求，并得到内容，避免重复地编写原生Curl代码。

简单预览 更多demo看下方
```php
<?php
/**
 * Created by PhpStorm.
 * User: Siam
 * Date: 2019/3/8
 * Time: 16:00
 */
require "../vendor/autoload.php";
$curl = \Siam\Curl::getInstance();
try {
    $res = $curl->send("http://pay.xxx.com/payment/public/index.php/api/pay",['sign' => '123']);
    echo($res);
} catch (Exception $e) {
    # 在这里捕捉异常
    echo "error" . $e;die;
}
```

## 实现功能

```php
/**
 * 设置Heard头
 * @Curl
 */
$curl->setsetHead($data);

/**
 * 设置超时
 * @Curl
 */
$curl->setTimeout($s);

/**
 * 发送curl请求
 * @param string $url 目标url
 * @param mixed $data 发送data
 * @param array $cert 证书文件绝对路径，一维数组，键名cert、key、ca
 * @param bool $post post还是get
 * @return mixed
 * @throws \Exception
 */
$curl->send($url, $data = null, $cert = [], $post = true);

// $curl->send()后可取返回head头
$curl->responseHead;
```

## 更多demo
```php
// 请求证书
$cert = [
    'ca'   => $adminConfig['pem_url'],   // ca证书
    'cert' => '',                        // cert证书
    'key'  => '',                        // key证书
];
$url  = "http://yancoo.cn";

$data = [
    'text' => 'test'
];

$curl = Curl::getInstance();
$curl->setHead([
    'Authorization: Basic ' . base64_encode(self::$APPID . ":" . self::$SERCETKEY),
    'Content-Type: application/json',
]);

$res  = $curl->send($url, $data, $cert);

echo "结果" . $res;

echo "\n";

echo "head头" ;
var_dump($curl->responseHead);
```