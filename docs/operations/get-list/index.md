# Получение списка / Get List

[English](#english) | [Русский](#russian)

## English

### CRM Module

#### REST API
```php
$leads = CRest::call('crm.lead.list', [
    'filter' => ['ASSIGNED_BY_ID' => 1],
    'select' => ['ID', 'TITLE', 'NAME', 'STATUS_ID']
]);
```

#### D7
```php
use Bitrix\Crm\LeadTable;

$leads = LeadTable::getList([
    'select' => ['ID', 'TITLE', 'NAME', 'STATUS_ID'],
    'filter' => ['=ASSIGNED_BY_ID' => 1]
])->fetchAll();
```

#### Legacy
```php
$filter = ['ASSIGNED_BY_ID' => 1];
$select = ['ID', 'TITLE', 'NAME', 'STATUS_ID'];
$leads = CCrmLead::GetList(
    ['ID' => 'ASC'],
    $filter,
    $select
);
```

### Information Blocks

#### REST API
```php
$elements = CRest::call('crm.lead.list', [
    'filter' => ['IBLOCK_ID' => 1],
    'select' => ['ID', 'NAME', 'PROPERTY_*']
]);
```

#### D7
```php
use Bitrix\Iblock\Elements\ElementTable;

$elements = ElementTable::getList([
    'select' => ['ID', 'NAME', 'PROPERTY_*'],
    'filter' => ['=IBLOCK_ID' => 1]
])->fetchAll();
```

#### Legacy
```php
$filter = ['IBLOCK_ID' => 1];
$select = ['ID', 'NAME', 'PROPERTY_*'];
$elements = CIBlockElement::GetList(
    ['ID' => 'ASC'],
    $filter,
    false,
    false,
    $select
);
```

## Русский

### Модуль CRM

#### REST API
```php
$leads = CRest::call('crm.lead.list', [
    'filter' => ['ASSIGNED_BY_ID' => 1],
    'select' => ['ID', 'TITLE', 'NAME', 'STATUS_ID']
]);
```

#### D7
```php
use Bitrix\Crm\LeadTable;

$leads = LeadTable::getList([
    'select' => ['ID', 'TITLE', 'NAME', 'STATUS_ID'],
    'filter' => ['=ASSIGNED_BY_ID' => 1]
])->fetchAll();
```

#### Старое ядро
```php
$filter = ['ASSIGNED_BY_ID' => 1];
$select = ['ID', 'TITLE', 'NAME', 'STATUS_ID'];
$leads = CCrmLead::GetList(
    ['ID' => 'ASC'],
    $filter,
    $select
);
```

### Информационные блоки

#### REST API
```php
$elements = CRest::call('crm.lead.list', [
    'filter' => ['IBLOCK_ID' => 1],
    'select' => ['ID', 'NAME', 'PROPERTY_*']
]);
```

#### D7
```php
use Bitrix\Iblock\Elements\ElementTable;

$elements = ElementTable::getList([
    'select' => ['ID', 'NAME', 'PROPERTY_*'],
    'filter' => ['=IBLOCK_ID' => 1]
])->fetchAll();
```

#### Старое ядро
```php
$filter = ['IBLOCK_ID' => 1];
$select = ['ID', 'NAME', 'PROPERTY_*'];
$elements = CIBlockElement::GetList(
    ['ID' => 'ASC'],
    $filter,
    false,
    false,
    $select
);
``` 