快速实现单例

本包其他的组件，大部分都依赖该组件实现单例模式调用

## 快速预览
```php
<?php
namespace Siam\Component;

class Di
{
    use Singleton;
    public function test()
    {

    }
}

$Di = Di::getInstance()->test();
```