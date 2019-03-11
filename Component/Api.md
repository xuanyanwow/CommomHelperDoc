Api组件是为了更好地编写Api接口而生。

功能是统一输出json的格式，便于调试。

```php
/**
 * 通用返回json封装
 * @param string $code
 * @param array $data
 * @param string $msg
 */
Api::json($code, $data = [], $msg = '');

/**
 * 输出调试
 * @param $name string 标签名
 * @param $data mixed 值
 * @param string $field string 调用字段
 */
Api::debug($name, $data, $field = '');
```

## demo
```php
$dbRes = []; // 伪代码  常为数据库或接口调用的返回
Api::debug('name', $dbRes);

// 定义了field字段，默认是不会输出该debug内容，
// 只有通过【传参】方式(POST,GET均可) teee字段，才会触发输出  
// 便于一些业务需要真机调试 在安卓端看到运行结果
Api::debug('name', $dbRes, 'teee'); 

$res = true; // 伪代码  常为处理业务的结果

//  输出完会自动exit
if ( $res ) {
    Api::json('200', [], "请求成功");
}
Api::json('500');

```

## 传参说明
json方法的`data`字段，需要一些特定的传参方式，以维持统一的json风格，便于与其他端对接。

!> Php是弱语言，很多类型都不规范使用，但程序也正常运行，在其他语言中，如果不统一类型，经常造成程序奔溃等情况。

`data`字段的传参需要一个 `二维或者以上` 的数组，不可传递一维数组

```php
$error = [
    'name' => 'siam',
    'age'  => 20,
];
echo json_encode($error, 256);
echo "\n";
// {"name":"siam","age":20}

$right = [
    'userdata' > [
        'name' => 'siam',
        'age'  => 20,
    ],
];
echo json_encode($right, 256);
echo "\n";
// {"userdata":{"name":"siam","age":20}}

$errorList = [
    [1,'siam'],
    [2,'ming'],
];
echo json_encode($errorList, 256);
echo "\n";
// [[1,"siam"],[2,"ming"]]

$rightList = [
    'userlist'=>[
        [1,'siam'],
        [2,'ming'],
    ],
];
echo json_encode($errorList, 256);
echo "\n";
// {"userlist":[[1,"siam"],[2,"ming"]]}

```

我们可以看到在errro的结果中，最外层是对象`{}`，假设我们的逻辑代码是这样子的
```php
$res = false;
if ($res){
    Api::json('200',[
        'name' => 'siam',
        'age'  => 20,
    ], '请求成功');
    // {"code":"200","data":{"name":"siam","age":20},"msg":"请求成功"}
}else{
    Api::json('500', [], '请求失败');
    // {"code":"500","data":[],"msg":"请求失败"}
}
```

这里会出现data字段一个场景是对象，一个场景是数组，所以安卓端会解析失败。

因此，我们在Api类的json方法中强制data参数为 `object` 并且要求data参数必须是一个二维以上数组。

这样子可以保证输出json的data字段始终是一个对象，不管它传参还是不传参。

正确输出
```json
{"code":"200","data":{"userdata":{"name":"siam","age":20}},"msg":"请求成功"}
```