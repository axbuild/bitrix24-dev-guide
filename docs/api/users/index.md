# Working with Users / Работа с пользователями

[English](#english) | [Русский](#russian)

## English

### Getting User List / Получение списка пользователей

Here are different approaches to get a list of users:

#### REST API
```php
$users = CRest::call('user.get', [
    'filter' => ['ACTIVE' => true],
    'select' => ['ID', 'EMAIL', 'NAME', 'LAST_NAME']
]);
```

#### D7 (Modern Core)
```php
use Bitrix\Main\UserTable;

$users = UserTable::getList([
    'select' => ['ID', 'EMAIL', 'NAME', 'LAST_NAME'],
    'filter' => ['=ACTIVE' => true]
])->fetchAll();
```

#### Legacy Core
```php
$filter = ['ACTIVE' => 'Y'];
$select = ['ID', 'EMAIL', 'NAME', 'LAST_NAME'];
$users = CUser::GetList(
    ($by = 'ID'),
    ($order = 'ASC'),
    $filter,
    $select
);
```

## Русский

### Получение списка пользователей

Различные способы получения списка пользователей:

#### REST API
```php
$users = CRest::call('user.get', [
    'filter' => ['ACTIVE' => true],
    'select' => ['ID', 'EMAIL', 'NAME', 'LAST_NAME']
]);
```

#### D7 (Современное ядро)
```php
use Bitrix\Main\UserTable;

$users = UserTable::getList([
    'select' => ['ID', 'EMAIL', 'NAME', 'LAST_NAME'],
    'filter' => ['=ACTIVE' => true]
])->fetchAll();
```

#### Старое ядро
```php
$filter = ['ACTIVE' => 'Y'];
$select = ['ID', 'EMAIL', 'NAME', 'LAST_NAME'];
$users = CUser::GetList(
    ($by = 'ID'),
    ($order = 'ASC'),
    $filter,
    $select
);
``` 