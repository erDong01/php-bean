# php-bean 

[![Php Version](https://img.shields.io/badge/php-%3E=7.1-brightgreen.svg?maxAge=2592000)](https://secure.php.net/)

###安装：
```
composer require marstm/bean
```

可以做强类型语言功能

在使用类里面直接引入Marstm\Bean
```php
namespace Marstm\Test;

use Marstm\Bean;

class TestJBean
{
    use Bean;
}
```

### 功能方法:

#### new

实例对象

```php
$userBean = UserBean::new();
```

#### bind

属性绑定数据

```php
$userBean = UserBean::bind(["user_id" => 12, "user_name" => "new"]);

```
#### setField

设置映射属性字段名，在也不用担心字段名写错，频繁去数据库查询表下有什么字段。
 
```php
# user. 表前缀，不设置为空
$userBean = UserBean::new()->setField("user.");

//示例一
\DB::table("user")->select($userBean->toArray())->get();

//示例二
\DB::table("user")->select($userBean->getUserName())->where($userBean->getUserId(),"10086")->get();
```

#### toArray

输出数组
 
```php
$userArr = UserBean::new()->toArray();
```


### phpStorm 编辑器使用 

生成get和set：类名右击->选择Generate->Getters and Setters->选择class 属性->ok 就可以生产了

快捷键 alt + insert

```php
use Marstm\Bean;

class UserBean
{
    /**
     * @return int
     */
    public function getUserId(): int
    {
        return $this->user_id;
    }

    /**
     * @param int $user_id
     */
    public function setUserId(int $user_id): void
    {
        $this->user_id = $user_id;
    }

    /**
     * @return string
     */
    public function getUserName(): string
    {
        return $this->user_name;
    }

    /**
     * @param string $user_name
     */
    public function setUserName(string $user_name): void
    {
        $this->user_name = $user_name;
    }
    use Bean;

    /**
     * 用户id
     * @var int #整型
     */
    private $user_id;
    /**
     * 用户名
     * @var string #字符串类型
     */
    private $user_name;

}
```

### 简单代替数组

```php

$userBean = UserBean::new();
$userBean->setUserName("teset");
$userBean->setUserId(111);
\DB::table("user")->insert($userBean->toArray());

```
