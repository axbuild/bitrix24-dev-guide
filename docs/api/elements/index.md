# Working with Elements / Работа с элементами

[English](#english) | [Русский](#russian)

## English

### Getting Elements List / Получение списка элементов

Here are different approaches to get a list of elements:

#### REST API
```php
$elements = CRest::call('crm.lead.list', [
    'filter' => ['ASSIGNED_BY_ID' => 1],
    'select' => ['ID', 'TITLE', 'NAME', 'STATUS_ID']
]);
```

#### D7 (Modern Core)
```php
use Bitrix\Crm\LeadTable;

$elements = LeadTable::getList([
    'select' => ['ID', 'TITLE', 'NAME', 'STATUS_ID'],
    'filter' => ['=ASSIGNED_BY_ID' => 1]
])->fetchAll();
```

#### Legacy Core
```php
$filter = ['ASSIGNED_BY_ID' => 1];
$select = ['ID', 'TITLE', 'NAME', 'STATUS_ID'];
$elements = CCrmLead::GetList(
    ['ID' => 'ASC'],
    $filter,
    $select
);
```

## Русский

### Получение списка элементов

Различные способы получения списка элементов:

#### REST API
```php
$elements = CRest::call('crm.lead.list', [
    'filter' => ['ASSIGNED_BY_ID' => 1],
    'select' => ['ID', 'TITLE', 'NAME', 'STATUS_ID']
]);
```

#### D7 (Современное ядро)
```php
use Bitrix\Crm\LeadTable;

$elements = LeadTable::getList([
    'select' => ['ID', 'TITLE', 'NAME', 'STATUS_ID'],
    'filter' => ['=ASSIGNED_BY_ID' => 1]
])->fetchAll();
```

#### Старое ядро
```php
$filter = ['ASSIGNED_BY_ID' => 1];
$select = ['ID', 'TITLE', 'NAME', 'STATUS_ID'];
$elements = CCrmLead::GetList(
    ['ID' => 'ASC'],
    $filter,
    $select
);
``` 