日期相关的一些快速操作组件

## 命名空间
```php
use siam\DateTool;
```

## 两个日期跨越区间

返回格式：差距的天数 可能有小数

```php
$diffDay = DateTool::dateSection('2019-10-01 00:11:22', '2019-10-11 00:11:22');
```


## 获取时间当月的第一天日期

$time 为null  默认取本月的第一天
```php
getMonthFirst($time = null, $format = 'Y-m-01')
```

使用
```php
$first = DateTool::getMonthFirst(time());
```

## 获取月份最后一天的日期

```php
$first = DateTool::getMonthFirst(time());
$end   = DateTool::getMonthEnd($first);
```