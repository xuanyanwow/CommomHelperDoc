快速对接接口 解析等

## 快速预览
```php
<?php
require "../../vendor/autoload.php";

use \Siam\Curl;
use \Siam\Wechat\Work;

$Work = Work::getInstance();

$MICROPAY_URL = "";

$config = [
    'mism_appid'   => '',
    'mism_mch_id'  => '',
    'sub_mch_id'   => '',
    'mism_mch_key' => '1',
];

$data     = array(
    'appid'            => $config['mism_appid'],
    'mch_id'           => $config['mism_mch_id'],
    'sub_mch_id'       => $config['sub_mch_id'],
    'spbill_create_ip' => '8.8.8.8',
    'nonce_str'        => md5(time()),
    'body'             => "wechat Pay", // 商品名称
    'out_trade_no'     => md5(time()),
    'total_fee'        => 100,
    'fee_type'         => "CNY",
    'auth_code'        => "11111"
);
# 排序
$sign           = $Work->makeSign($data, $config['mism_mch_key']);
$data['sign'] = $sign;

$xmlData = $Work->arrayToXml($data);

try {
    $res = Curl::getInstance()->send($MICROPAY_URL, $xmlData);
} catch (Exception $e) {
}

$res_    = $Work->xmlToOjb($res);

var_dump($res);
```
# 方法列表

## makeSign($data, $key)
快速计算接口签名
$data 原始数据
$key  商户秘钥

## arrayToXml($arr)
数组转xml字符

## arrayToUrl($arr)
数组转url拼接
> 会过滤 sign字段 和 空数据字段
xx=xx&xx=xx

## arrayAllToUrl($arr)
所有字段拼接
xx=xx&xx=xx

## xmlToOjb($xml)
xml转对象
解析微信接口返回

## xmlParser($xml)
xml解析另一方法

## objToArray($obj)
对象转数组

## getOpenid($config)
不多说 获取openid
$config['appid'];
$config['secret'];

> 应该在入口最开始获取，因为获取openid需要重定向，前面执行一半的逻辑也没用

```php
$openid = $work->getOpenid($config);
```

## decryption($data)
退款解密
$data['req_info'] = '解密字段';
$data['key'] = 'key';

## checkFeeType($total_fee, $fee_type, $type = 'set')
* 根据货币检查单位
* 调用set一般场景【接口(以分为单位)拿到的金额转换真实最低单位货币提交给微信】 刷卡100分=1元  转成日元 要除以100
* 调用get一般场景【微信回调拿到的金额转换为分单位存到数据库】  微信回调1日元 = 100分 转成分单位 乘以100